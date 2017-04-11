# 记录搭建Webpack自用框架所遇到的问题

#### 1.如何解决使用基于express框架搭建的node前端服务器调用接口时的跨域问题？

> 使用npm提供的 http-proxy-middleware 插件可以很方便的处理跨域请求。比如某个api文件夹下的接口全部重定向到 "[http://xxx.com](http://xxx.com/)" 的域名下。具体使用方法如下：

```
var express = require('express');
var proxy = require('http-proxy-middleware');

const app = express();

app.use(express.static(__dirname + '../api'),proxy({
    target: 'http://xxx.com',
    changeOrigin: true
}));
```

#### 2.如何打包jquery、jquery插件、以及其他的一些第三方类库？

> 打包jquery不能像其他第三方类库一样打包进vendor，因为某些jquery插件依赖于jquery，所以在引用的时候会导致"$ is undefined"这类情况。较好的做法是通过引用[expose-loader](https://github.com/webpack-contrib/expose-loader)去解决问题。具体代码如下：

```
module: {
    rules: [
        {
           test: require.resolve('jquery'),
           use: 'expose-loader?jQuery!expose-loader?$'
        }
    ]
}
```

> js直接引用jquery及相应的jquery插件，即可使用

```
import $ from 'expose-loader?!jquery'
import bootstrap from '../common/js/bootstrap.min.js'
```

> 而对于一些全局引用的第三方类库，建议还是打包成一个vendor.js的文件，相关配置项如下：

```
entry: {
    "vendor": ['fontSize','artTemplate']
}

resolve: {
    extensions: ['.js'],
    alias: {
        'fontSize':path.resolve(__dirname,'../src/common/js/public/fontSize.js'),
        'artTemplate':path.resolve(__dirname,'../src/common/js/public/art-template.js')
    }
}
```

> 将所有第三方类库打包到一个vendor.js并输出到预期路径，值得注意的是输出的filename带上hash的话可以让hot-middle-ware组件识别，从而达到热更新的效果，所以建议带上

```
new webpack.optimize.CommonsChunkPlugin({
    names: ['vendor'],
    filename: 'common/[name][hash].js'
})
```

#### 3.引入中文字体文件过大，导致页面加载过慢的问题

> 在我们开发的时候，实际拿到的页面很多的字体效果都不是手机默认的字体，但是由于中华文化博大精深，一个中文字体文件搞下来就好几M，打开个页面卡得是生活不能自理。解决方案是用到npm提供的一个叫[font-spider](http://font-spider.org/)的插件。原理是通过爬你的html页面将你用到的文字生成一个新的字体文件。具体使用方法可以点链接看下。

#### 4.如何将js打包到指定路径，方便阅读管理

> 这里用到一些小技巧，可以将要打包的js的文件名带上文件夹的路径，这样可以在生成js的时候自动带上相关路径。如下会在dist目录下生成app和browser两个目录，该目录下分别存放 index.js、friendlist.js 和 step1.js、step2.js 具体代码如下：

```
entry: {
    "vendor": ['fontSize','bootstrap'],
    "app/index": path.resolve(__dirname,'../src/app/index.js'),
    "app/friendlist": path.resolve(__dirname,'../src/app/friendlist.js'),
    "browser/step1": path.resolve(__dirname,'../src/browser/step1.js'),
    "browser/step2": path.resolve(__dirname,'../src/browser/step2.js')
},
output: {
    path: path.resolve(__dirname,'../dist'),
    publicPath : '/',
    filename: '[name].js',
    chunkFilename: '[id].[chunkhash].js'
}
```

#### 5.webpack对图片的处理？包括打包css文件引用到的图片和页面上直接用img标签加载的图片

> file-loader和url-loader都可以用来打包css所引用的img文件，但是如果要用到image-webpack-loader对图片进行压缩的话，就使用file-loader。具体代码如下：

```
module: {
    rules: [
        {
            test: /\.(jpeg|jpg|png|svg|gif)(\?[a-z0-9]+)?$/,
            use: [
            'file-loader?limit=10000&name=styles/images/[name].[ext]',
            'image-webpack-loader?progressive:true&opimizationLevel=4'
        ]

        }
    ]
}
```

**值得注意的一点的是，使用image-webpack-loader进行压缩图片，如果是win7系统下的话，需要配置一个环境变量。不然会报"unable to verify the first certificate"的错误。这个有点坑。环境变量配置：NODE_TLS_REJECT_UNAUTHORIZED=0**

> 而页面上的img文件，可以通过'html-withimg-loader'进行打包，在生成html页面时带上即可。代码如下：

```
new HtmlWebpackPlugin({
    chunks: ['app/index','vendor'],
    filename: 'index.html',
    template:'html-withimg-loader!'+path.resolve(__dirname,'../src/common/tmpl/app/index.html'),
    inject: true
})
```

#### 6.webpack图片问题解决方案

总结下在react中用到图片的情景

从简单到复杂

- 普通的background-image引用，小图居多，大图有限情况

  > 只使用url-loader就ok
  > {test: /.png$/, loader: "urllimit=8192"}

将小图全部转换为base64格式内联到js里

- background-image引用，小图，大图都有较多

  > 需要url-loader和file-loader搭配使用
  > 小图转换成base64内联，大图使用file-loader发布成一个image文件夹，可以放到cdn或者本地
  > **注意** *发布时路径问题output.publicPath决定*

- jsx里 img标签图片

  > 如果此类图片较少可以提前直接放到cdn上确保能访问到，在标签内直接写cdn的引用。
  > 如果开发环境时需要在本地有这些图片，jsx中img图片的引用方式
  > `<img src={require('./img/ssq.png')} alt=""/>`
  > 此处为图片的真实相对路径
  > 在webapack.config中要对此配置
  > `{test:/\.png$/,loader:"urllimit=8192&name=img/[name].[ext]"}`

> 此处是本地server的图片引用
> `<img src="/img/ssq.png" alt="" data-reactid=".0.0.1.0">`
> 此处是编译后的代码
> `n.p+"img/ssq.png"`

/*注*/
`{test:/\.png$/,loader:"urllimit=8192&name=img/[name].[ext]"}`
可以处理绝大多数图片问题 依赖url-loader&file-loader



#### 7.webpack如何将css文件抽离出来，添加前缀，以及压缩你的css文件？

> 个人不怎么建议将css跟js一起打包进一个文件，页面样式少还好，多的话不保证随时出现样式冲突的可能。而且全部打包在一起也会让整个js文件变得臃肿。这里用到'extract-text-webpack-plugin'来抽离你项目里的css文件，用'postcss-loader'添加样式前缀代码如下：

```
`var ExtractTextPlugin = require('extract-text-webpack-plugin');

module: {
    rules: [
        {
            test: /\.css$/,
            use: ExtractTextPlugin.extract({
            fallback: 'style-loader',
            use: [
            {
                loader: 'css-loader',
                options: {
                    importLoaders: 1
                }
            },
            'postcss-loader'
            ]
            })
        }
    ]
}

new ExtractTextPlugin({
    filename: "styles/css/[name].[contenthash:6].css",
    allChunks: false
})

new webpack.LoaderOptionsPlugin({
    options: {
        postcss: () => {
            return [
                require('autoprefixer')({
                    browsers: ['last 5 versions']
                })
            ]
        }
    }
})
```

> 压缩css的话用到的是'optimize-css-assets-webpack-plugin'

```
var OptmizeCssAssetsPlugin = require('optimize-css-assets-webpack-plugin');

new OptmizeCssAssetsPlugin({
    assetNameRegExp: /\.css$/g,
    cssProcessor: require('cssnano'),
    cssProcessorOptions: {discardComments:{removeAll: true}},
    canPrint: true
})
```

#### 8.webpack如何切换开发环境和生产环境？

> 生产环境跟开发环境的区别无非就是调用的接口地址、资源存放路径、线上的资源是否需要压缩等等这些方面。目前的做法是通过在packge.json通过设置node的一个全局变量然后在webpack.config.js文件里面进行生产环境与开发环境的配置切换。后续有好的方案再进行改善。

```
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "webpack": "set NODE_ENV=dev&& webpack --display-modules --display-chunks --config build/webpack.dev.conf.js",
    "build": "set NODE_ENV=prod&& webpack --display-modules --display-chunks --config build/webpack.dev.conf.js",
    "server": "set NODE_ENV=dev&& node build/dev-server.js"
  }
```

> 通过设置NODE_ENV的值，这样执行npm run webpack 和 npm run build命令就可以实现打包两个不同环境的项目 ，配置文件中的代码如下：

```
//针对开发环境与生产环境做不同的配置
if(process.env.NODE_ENV == 'dev'){

    console.log("**********开发环境打包中**********");
    //开发环境下项目的输出路径
    config.output.publicPath = "/";

    //开发环境下启动页面监听 动态向入口配置中注入 webpack-hot-middleware/client
    var devClient = './build/dev-client';
    Object.keys(config.entry).forEach(function(name,i){
        var extras = [devClient];
        config.entry[name] = extras.concat(config.entry[name]);
    })

}else if(process.env.NODE_ENV === 'prod'){

    console.log("**********生产环境打包中**********");
    //生产环境下项目的输出路径
    config.output.publicPath = "http://xxx.com/app/events/yqm/";

    //生产环境下进行的Plugins扩展
    var ext_plugins = [
        new webpack.optimize.UglifyJsPlugin({
            compress: {
                warnings: false
            }
        }),
        new OptmizeCssAssetsPlugin({
            assetNameRegExp: /\.css$/g,
            cssProcessor: require('cssnano'),
            cssProcessorOptions: {discardComments:{removeAll: true}},
            canPrint: true
        })
    ];
    config.plugins = config.plugins.concat(ext_plugins);

}
```

### 总结

整个框架基本还是可以满足基本的前端开发，包括前后端分离、文件打包处理、第三方类库使用、页面热更新等等。这些都能大大提高前端开发的效率。在搭建过程中一些常见的问题并没有在这里列举出来，比如热更新的配置，js压缩，html页面自动生成等。还有一些功能没有加进来或者是还没完善，如结合模板引擎的html页面片段的引用、自动化压缩字体文件、生产环境与开发环境下的处理不够规范等等。