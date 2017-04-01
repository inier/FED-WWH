
# SASS用法指南
Sass属于css预处理器中的一种,还有两款他们分别是Less和 Stylus,SASS是一种CSS预处理器， 本文主要介绍SASS的主要用法。
> Css预处理器（css preprocessor）定义了一种新的语言将Css作为目标生成文件，然后开发者就只要使用这种语言进行编码工作了。预处理器通常可以实现浏览器兼容，变量，结构体等功能，代码更加简洁易于维护。

## Sass 与 Css
* ncss算不上一门真正的编程语言,无法完成嵌套,继承,设置变量等工作.
* Sass是对css进行预处理的“中间语言”,为了弥补css的不足

## .scss 和 .sass
* .sass [缩进语法]
最初它是为了配合haml而设计，所以和haml有着一样的缩进式风格,它使用 行缩进 的方式来指定css 块.在缩进语法的文件以 `.sass` 为拓展名。
* .scss [Sassy CSS( 时髦的css)]
从 Sass 3开始支持,它是css3语法的的拓展级，每一个语法正确的CSS3文件也是合法的SCSS文件，SCSS文件使用`.scss`作为拓展名。

## 什么是 Compass
Compass是Sass的工具库,详情请点击[这里](http://compass-style.org/)
### Sass与Compass 
Sass与Compass的关系,类似于JavaScript和JQuery的关系.
***

## **-- 安装 --**
SASS是Ruby语言写的，但是两者的语法没有关系。不懂Ruby，照样使用。只是必须先安装Ruby，然后再安装SASS。
假定你已经安装好了Ruby，接着在命令行输入下面的命令：
```
　　gem install sass
```
然后，就可以使用了。

### Sass与Compass的安装 
国内需要FQ,没钱FQ的可以使用淘宝的镜像,改变source 就可以了 
```
$ gem sources --add https://ruby.taobao.org/ --remove https://rubygems.org/
gem install compass //来安装compass,安装compass的时候,也会把sass一起装上.
compass -v //查看是否安装成功,安装成功会在控制台输出版本号.
sass -v //查看是否安装sass成功,安装成功会在控制台输出版本号.
```
***

## **-- 编译 --**
SASS文件就是普通的文本文件，里面可以直接使用CSS语法。文件后缀名是.scss，意思为Sassy CSS。

### **- 命令模式 -**
执行`sass <sass file> <css file>`命令，可以在屏幕上显示.scss文件转化的css代码。（假设文件名为test。）
```
　　sass test.scss
```
如果要将显示结果保存成文件，后面再跟一个.css文件名。
```
　　sass test.scss test.css
```

- 单文件转换：sass style.scss style.css
- 单文件监听：sass --watch style.scss style.css
- 文件夹监听：sass --watch sassFileDir:cssFileDir

- css文件转换成sass/scss文件：
```
    sass-convert style.css style.sass
    sass-convert style.css style.scss
```
#### 配置项
运行命令行帮助文档，可以获得所有的配置选项： sass -h

一般常用的有--style，--sourcemap，--debug-info等：
```
    sass --watch style.scss:style.css --style compact
    sass --watch style.scss:style.css --sourcemap
    sass --watch style.scss:style.css --style expanded --sourcemap
    sass --watch style.scss:style.css --debug-info
```
- --style表示解析后的css是什么格式，有四种取值分别为：nested，expanded，compact，compressed。
- --sourcemap表示开启sourcemap调试。开启sourcemap调试后，会生成一个后缀名为.css.map文件。
- --debug-info表示开启debug信息

#### 输出风格
SASS提供四个编译风格的选项：
* nested：嵌套缩进的css代码，它是默认值。
```
    body {
        background-color: #f00; }

    .person, .son {
        height: 100px; }
```
* expanded：没有缩进的、扩展的css代码。
```
    /* line 1, ../sass/demo1.scss */
    body {
        background-color: #f00;
    }

    /* line 4, ../sass/demo1.scss */
    .person, .son, .banner {
        height: 100px;
    }
```
* compact：简洁格式的css代码。
```
    /* line 1, ../sass/demo1.scss */
    body { background-color: #f00; }

    /* line 4, ../sass/demo1.scss */
    .person, .son, .banner { height: 100px; }
```
* compressed：压缩后的css代码。
```
    body{background-color:red}.person,.son,.banner{height:100px}
```

生产环境当中，一般使用`compressed`选项。
```
　　sass --style compressed test.sass test.css
```
#### 利用sass命令来监视文件和文件夹
你也可以让SASS监听某个文件或目录，一旦源文件有变动，就自动生成编译后的版本。
* 监视Sass文件: `sass --watch <sass file>:<css file>`
* 监视文件夹：`sass --watch <sass folder>:<css folder>`
```
　　// 监视Sass文件
　　sass --watch input.scss:output.css
　　// w监视文件夹 
　　sass --watch app/sass:public/stylesheets
```
> 注意源文件和目标文件之间是 冒号 ，与编译命令中为空格不同;生成的map文件可以查找source map文件的作用。

#### 使用compass编译sass
* 创建compass目录执行`compass create folderName`
    + 查看创建好的目录结构可以看出,该命令共创建了两个文件夹,
    + 分别是`sass`和`stylesheets`,这两个文件夹前者是用来放sass文件,后者则是用来存储编译好的css文件.

* 只需要把相关的scss放进sass文件夹内,执行`compass compile`命令就可以编译了,编译好的文件会自动放在`stylesheets`文件夹内

* 监视文件夹: 执行命令`compass watch`;如果加上后缀–force的话表示不管文件更改还是不更改都会重新编译文件`compass watch --force`

* 设置中文不报错 
    1. 在ruby的安装目录中找到`engine.rb`（每个人电脑都不一样），如 `C:\Ruby22-x64\lib\ruby\gems\2.2.0\gems\sass-3.4.20\lib\sass\engine.rb`
    2. 添加如下代码`Encoding.default_external = Encoding.find('utf-8')`

### **- 工具模式：Webpack/gulp等 -**
#### 图形化工具gui  koala
#### gulp
#### webpack
Webpack中也内置了sass-loader，通过简单的配置既可以使用。不过需要注意的是，Webpack的sass-loader还是依赖于node-sass以及sass(gem)，所以如果安装sass-loader报错可以先尝试安装sass。

### **- 在线模式 -**
SASS的官方网站，提供了一个在线转换器。你可以在那里，试运行下面的各种例子。
***

## **-- 调试 --**
sass调试需要开启编译时输出调试信息和浏览器调试功能，两者缺一不可。详情请见[这里](http://www.cnblogs.com/Iona/p/5302476.html).

## **-- 基本用法 --**

### **- 设置文件编码 -**

编码`@charset "encoding-name";` , 若需要支持中文注释,在SCSS文件的顶部写上`@charset "UTF-8";`。

***

### **- 样式导入 -**
有时网页的不同部分会分成多个文件来写样式，或者引用通用的一些样式，那么可以使用 `@import`。

`@import` 命令的注意点： 
- 可以使用相对路径 
- 导入的文件可以.scss后缀名 
- 可以引入线上的scss文件 
- 支持括入引入的写法
- 支持引入**带下划线**和**不带下划线**的文件;比如(navbar和_navbar) ，在同一个目录不能同时存在带下划线和不带下划线的同名文件。例如，`_navbar.scss` 不能与 `navbar.scss` 并存。
    + 若是文件命名**带下划线**则不编译该文件,但却可以正常把样式导入其他文件用(如index.scss引入_navbar,只产生index.css) 
    + 若是文件命名**不带下划线**,两者皆会编译,产生CSS文件((如index.scss引入navbar,会产生index.css和navbar.css`)) 
- 支持在CSS 规则 和 @media 规则内引入样式
```
    @import "path/filename.scss";     //直观的引入单一文件                
    @import "footer" ;
    @import "http://test.xx/sidebarbar";
    @import url(foo);
    @import "navbar","sidebar","header","footer";   //直接导入多个文件

    .test{
        @import "widget";
    }
```
####　部分文件
部分文件是指分隔成多个片段的文件，其名称约定以下划线`_`开头, 如`_reset.scss`。以下划线打头的文件`不会被编译`，适用于存放通用变量集、mixin、占位片段、函数等。

#### 原生css导入 
因为原生导入css的方式和sass使用的关键词一致,为了区分使用了一些约定。以下三种情况会直接生成css,不作任何变化,会被当做原生的css导入。
* 如果导入的文件名称以css结尾
* 如果被导入的文件的名称是一个URL地址
* 被导入的文件的名字是css的url()的值
```
// scss
    @import "css.css";
    @import "http://xxx";
    @import url(css.css);
    // 生成的css
    @import url(css.css);
    @import "http://xxx";
    @import url(css.css);
```
##### link & @import
link就是把外部CSS与网页连接起来。@import文字上与link的区别就是它可以把在一个CSS文件中引入其它几个CSS文件。
* 大部分使用@import方式的人是因为旧的浏览器是不支持@import方式的,这意味着我们可以使用@import来引入只让现代浏览器解析的CSS样式.
另一个主要的原因就是当你的网页需要引入几个外部CSS文件时.你可以使用link引入一个CSS,然后在这个CSS文件中用@import方式引入其它几个CSS文件.这样看起来更容易管理.
* 使用link方式一个最主要的原因就是你可以让用户切换CSS样式.现代浏览器如Firefox,Opera,Safari都支持rel="alternate stylesheet"属性(即可在浏览器上选择不同的风格),当然你还可以使用Javascript使得IE也支持用户更换样式.
> 如果你网页head标签里面十分简单,只有@import属性的话,当用户浏览的网速较慢时,他会看到一个没有风格样式的页面,然后随着CSS文件被下载完成才可以看到应有的风格.要避免这样的问题,你需要确保head里至少有一个script或是link标签.@import会使得CSS整体载入时间变长.并且在IE中会导致文件下载次序被更改,例如放置在@import后面的script文件会在CSS之前被下载. "css.css"会降低加载性能，并且部分浏览器不支持这种引入方式。

#### scss文件导入
举例说明，这里新建了一个文件名称叫做`_part1.scss`,该文件的样式:
```
    $fontFamily: '微软雅黑';
    .body {
        font-family: $fontFamily;
    }
```
在demo1.scss中导入
```
    @import "part1"; // 这样直接写,就会导入`_part1.scss`中的样式,这是约定.
```
demo1文件生成了以下的css
```
    /* line 2, ../sass/_part1.scss */
    .body { font-family: "微软雅黑"; }
```

***

### **- 注释 -**
sass中的注释有三种形式：

1. // 单行注释：该注释只是在.scss源文件中有，编译后的css文件中没有。eg: 
```
    .html{
        font-size:14px;    // 这是标准字号，1rem = 14px
    }
``` 

2. /* */范围注释, 该注释在`compressed`的style的css中没有，其他style的css文件都会含有。 eg:
```
    /*
        什么功能;
        做什么用的;
    */
    .xxx{xxx:xxx}
    .xxx{xxx:xxx}
    .xxx{xxx:xxx}
```

3. /*! */：重要注释，任何style的css文件中都会有，一般放置css文件版权说明等信息。
***
```
　　/*! 
　　　　重要注释！
　　*/
```
***

### **- 变量 -**

#### 变量`$`

所有变量以`$`开头,其他命名规则类似于其他编程语言。
```
　　$blue : #123456;　
　　div {
　　　color : $blue;
　　}
```
编译后：
```
    div {
        color: #123456;
    }
    /*# sourceMappingURL=test.css.map */
```
#### 多值变量

* nth: 语法`nth(variable,index);`
> index是从1开始的。
```
    $color: red;
    $maps: (borderColor: red, backgroundColor: blue);
    $paddings: 10px 20px 30px 40px;
    $padding1: 3px 20px 30px 40px;
    body {
        color: $color;  
    }

    footer {
        color: $color;
        padding: $paddings;
        padding-left: nth($padding1,1);
    }
```
```
    body { color: red; }
    footer { color: red; padding: 10px 20px 30px 40px; padding-left: 3px; }
```

* map-get: 语法map-get(variable, key)

作用是从variable字典库中取出对应的key。
- variable语法$maps: (borderColor: red, backgroundColor: blue);
> 当`variable错误`的时候,会报错; 当`key不存在`的时候,不会编译这条语句,也就是说这条css不会编译出来。
```
    $color: red;
    $paddings: 10px 20px 30px 40px;
    $padding1: 3px 20px 30px 40px;
    $maps: (borderColor: red, backgroundColor: blue);
    body {
        color: $color;  
    }

    footer {
        color: $color;
        padding: $paddings;
        padding-left: nth($padding1,1);
        border-color: map-get($maps, borderColor);
        background-color: map-get($maps, backgroundColor);
    }
```
```
    body { color: red; }
    footer { color: red; padding: 10px 20px 30px 40px; padding-left: 3px; border-color: red; background-color: blue; }
```
***

#### 变量插值`#{}`——变量用在属性或者选择器上

如果变量需要镶嵌在属性或者选择器（字符串）上，就必须需要写在`#{}`之中。
* 当变量挡住属性来使用的时候#{变量名}
* 当变量当做类名来使用的时候’.#{变量名}{}’
```
    $side : left;
　　.rounded {
　　　　border-#{$side}-radius: 5px;
　　}    

    $test:(margin,border);
    @mixin t($t1, $t2){
        @each $t3 in $test{
            #{$t3}-#{$t1}:$t2;
        }
    }

    .btn{
        @include t(right,5px);
    }
```
```
    /*（表示编译后的结果）
    .rounded {
　　　　border-left-radius: 5px;
　　} 
    .btn {
        margin-right: 5px;
        border-right: 5px;
    }
    */
```

#### 变量的命名
变量的使用中横线还是下划线,都是`同一个`变量 怎么用取决于你的爱好。
```
    $font-size: 19px;
    .font-size {
        font-size: $font_size;
    }

    // .font-size { font-size: 19px; }
```

#### 变量默认值`!default`
在变量后面,分号前面加上`!default`。
作用: 如果首先定义了一个变量$color: red,那么第二次继续赋值为$color: green,此时$color的值为green, 如果第二次赋值的时候在变量后面加上一个!default标识的话,就不会覆盖上次的赋值.这说明,`加上!default标识的语句会被优先编译和赋值`.
```
    //调用默认值
    $fs:12px !default;
    p{
        font-size: $fs;   //css: font-size:12px;
    }

    //覆盖默认值
    $fs:15px;
    $fs:12px !default;
    p{
        font-size: $fs;   //css: font-size:15px;
    }
```

#### 变量的作用域（variable default scope）
SASS使用块级作用域.
```
@mixin foo {
    $val: 'red' !default // defined locally
    .bar{
        color: $val;
    }
}
@include foo; // $val in mixin foo look for global $val. no global $val found, then 'red'

.class1{
    $val: 'green';
    @include foo; // $val in mixin foo look for global $val. no global $val found, then 'red'
    color: $val;  // local $val 'green'
    .class11{
        @include foo; // $val in mixin foo look for global $val. no global $val found, then 'red'
    }
}
$val: 'black'; // defined globally at the first time

.class2 {
    @include foo; // $val in mixin foo look for global $val. $val found, 'black'
}
.class3{
    $val: 'blue' // change the gobal $val
    @include foo; // $val in mixin foo look for global $val. $val found, 'blue'
}
.class4{
    @include foo; // $val in mixin foo look for global $val. $val found, 'blue'
}
```
* 全局变量：
全局变量定义在所有嵌套选择器之外，可以在各处被调用。
```
    $fs:12px;   //在元素内部外或者mixin外部定义皆可理解为全局
    p{
        font-size: $fs;   //css: font-size:12px;
    }
```
如果希望某个在子选择器中定义的变量能够成为全局变量，可以使用`!global`关键字：
```
    #main {
        $width: 5em !global;
        width: $width;
    }

    #sidebar {
        width: $width;
    }
```
> 如果在一个块级作用域里面声明一个变量,要在另一个块级作用域使用的话必须加上`!global`,否则如果在另一个块级作用域使用此变量会报错.
```
    body {
        /*$color: red;
        color: $color;  局部变量,下面访问不到, 所以编译会报错,如果想要下面能够访问到的话. 只需要后面加上!global就可以了*/
        $color: red !global; /*这样就可以吧局部变量变为全局变量*/
        color: $color;
    }

    footer {
        color: $color;// 这里也不会报错
    }
```

* 局部变量：
```
    $fs:12px;
    p{
        $fs : 20px;        //在元素内部定义的变量为局部变量,若是外部全局变量和局部变量命名一致,全局会被局部变量
        font-size: $fs;   //css: font-size:20px;
    }
```

***

### **- 样式嵌套 -**
SASS中，除了个别选择符，基本和CSS一样，就是写法是内嵌格式。
#### 选择器嵌套
SASS允许选择器嵌套:
```
    #main{
        p{ font-size:15px}     //css : #main p{};
        >a{
            span{font-size:10px;} //css: #main>a span{font-size:10px;}                     
        }
    }
```
#### 属性嵌套
属性也可以嵌套:
```
    #main{
        border:{
            top:1px solid #ccc;
            left:2px solid #ddd;
        }
    }
 ```
 ```   
    /*（表示编译后的结果）
    #main {
        border-top: 1px solid #ccc;
        border-left: 2px solid #ddd;
    }
    */
```
> 注意，border后面必须加上冒号。

#### 父类选择符`&`
&相当于JS中的this。在嵌套的代码块内，可以使用`&`引用父元素：
```
　　#main{
        p{ font-size:15px}         //css: #main p{};
        >a{                        //css: #main>a{}
            &:link,
            &:visited{}           //css: #main>a:link,#main>a:link{}
            &:hover{};            // &在SCSS内嵌中代表父类,css: #main>a:hover{};
            &:active{};
        }
    }

    .bar {
        .foo & {
            color: gray;      // .foo .bar {color: gray;}
        }
    }
```

#### 跳出嵌套`@at-root`
从字面上解释就是跳出根元素。当你选择器嵌套多层之后，想让某个选择器跳出，此时就可以使用 `@at-root`。
* 默认的`@at-root`只能跳出选择器嵌套,不能跳出`@media`和`@support`
* 如果需要跳出这两个嵌套的话需要设置`@at-root(without: media)`和`@at-root(without: support)`
这个语法关键词有四个:
- `all`表示所有的
- `rule`表示常规的
- `media`表示`media`
- `support`表示`support`,目前`@support`还无法广泛的使用
> 默认的`@at-root`,其实就是`@at-root(without: rule)`; 需要分清 `@media`和`@support`， `media`和`support`，前两个是css的规则关键字，后两个是与之对应的 `@at-root(without：value)`中的`value`。
```
    body {
        a {
            height: 100px;
            &:hover {
                background-color: green;
            }
            // 跳出常规样式,对应着下面的行号 8
            @at-root .container {
                height: 100px;
            }
            @media(min-width: 768px) {
                // 跳出media和常规样式
                @at-root(without: media rule) {
                    .container { // 这里对应下面的行号14
                        height: 100px;
                }
                }
                // 下面的样式只跳出了media 没有跳出常规样式,如果需要跳出常规样式的话需要设置,rule
                @at-root(without: media) {
                    .container { // 这里对应行号20
                        width: 1000px;
                    }
                }
            }
        }
        @media(max-width: 1000px) {
            // 默认是跳出 rule
            @at-root .container{ // 对应行号28
                height: 1000px;
            }
            // 下面这句跳出media
            @at-root(without: media rule) {
                .container { // 对应行号33
                    width: 500px;
                }
            }
        }
    }
```
```
    /* line 2, ../sass/demo2.scss */
    body a { height: 100px; }
    /* line 4, ../sass/demo2.scss */
    body a:hover { background-color: green; }
    /* line 8, ../sass/demo2.scss */
    .container { height: 100px; }
    /* line 14, ../sass/demo2.scss */
    .container { height: 100px; }
    /* line 20, ../sass/demo2.scss */
    body a .container { width: 1000px; }

    @media (max-width: 1000px) { /* line 28, ../sass/demo2.scss */
        .container { height: 1000px; } }
    /* line 33, ../sass/demo2.scss */
    .container { width: 500px; }
```
#### & 和 @at-root的嵌套用法
```
    @at-root .container {
        color: red;
        @at-root nav & {
            color: blue; 
        }
    }
```
```
    .container { color: red; }
    nav .container { color: blue; }
```

#### @at-root在BEM命名方式中的使用
[BEM命名方式](http://www.tuicool.com/articles/IrUbq2m)规则如下：
> BEM命名方式关注的点：B(Block)：表示模块，最小的可复用单元，功能独立，可以嵌套、组合使用；E(Element)：B的组成部分；M（Modifier）：表示E的状态（不同状态下的E有不同的功能和外观），也是B的组成部分。
```

.block {}  //模块
.block__element{}    //模块的组成部分
.block--modifier{}   //不同状态
```
试想在SASS中是否可以通过插值 `#{}` 方式来实现上面样式代码：`#{&}_element{}`。不仿来验证一下：

```
    .block {
        color: red;

        #{&}__element {
            color:blue;
        }

        #{&}--modifier {
            color: orange;
        }
    }
```
但是，编译出来的CSS并不是我们想要的代码：
```
    .block {
        color: red; 
    }
    .block .block__element {
        color: blue; 
    }
    .block .block--modifier {
        color: orange; 
    }
 ```
而在LESS和Stylus中，能很好的实现BEM类名的形式。那么SASS就无法实现这样的效果么？非也，SASS3.3起新增的@at-root特性，能实现上面BEM的特性：
 ```
    .block {
        color: red;
        @at-root #{&}__element {
            color: blue;
        }

        @at-root #{&}--modifier {
            color:orange;
        }
    }
```
> 在SCSS中嵌套，使用@at-root内联选择器模式，编译出来的CSS无任何嵌套，让代码更加的简单。回到SCSS中的嵌套中，如果不使用@at-root内联选择器模式，将会按代码的层级关系一层一层往下嵌套。
***

### **- @media指令 -**
sass 中的 @media 指令和 CSS 的使用规则一样的简单，但它有另外一个功能，可以嵌套在 CSS 规则中。有点类似 JS 的冒泡功能一样，如果在样式中使用 @media 指令，它将冒泡到外面
```
    .sidebar {
        width: 300px;
        @media screen and (max-width: 1920px) {
            width: 600px;
        }
    }
```
```
    /*
    .sidebar {
        width: 300px;
    }
    @media screen and (max-width: 1920px) {
        .sidebar {
            width: 600px;
        }
    }
    */
```
***

## **-- 代码重用 --**

### **- @extend继承 -**

#### 简单继承
一个选择器，继承另一个选择器。使用关键字`@extend <selector>`。
```
　　.alert {
        height: 30px;
    }
　　.alert-info {
        @extend .alert;
        color: #D9EDF7;
    }
```
```
    .alert, .alert-info { height: 30px; }
    .alert-info { color: #D9EDF7; }
```
注意：如果在`.alert-info`后面有设置了`.alert`的属性，那么也会影响`.alert-info`，如下：
```
    .alert {
        height: 30px;
    }
　　.alert-info {
        @extend .alert;
        color: #D9EDF7;
    }
    .alert{
        font-weight:bold;    
    }    
```
由此可以看出SASS也是递归编译的。

#### 多继承
同简单继承类似,语法: @extend selector1, selector2…………
```
    .alert {
        height: 30px;
    }
    .bgc {
        background-color: #f5f5f5;
    }
    .alert-info {
        @extend .alert, .bgc;    //多继承
        color: #D9EDF7;
    }
```
```
    .alert, .alert-info { height: 30px; }
    .bgc, .alert-info { background-color: #f5f5f5; }
    .alert-info { color: #D9EDF7; }
```

#### 链型继承
什么是链式继承呢,按照自己的理解为,假如c继承b,b继承a,那么c同时拥有b和a 的属性.这看起来像一条链条
```
    .one {
        border: 1px solid red;
    }
    .two {
        @extend .one;
        color: red;
    }
    .three {
        @extend .two;
        background-color: #f5f5f5;
    }
```
```
    .one, .two, .three { border: 1px solid red; }
    .two, .three { color: red; }
    .three { background-color: #f5f5f5; }
```

#### %占位选择器
`%` 表示占位选择器, 不会生成到架构里面,只有用到它的时候才会生成占位符,减少CSS无用的样式的好方法。
```
    %mr5{
        margin-right:5px;
    }      
    body{
        @extend %mr5;
    }
    %message {
        height: 30px;
    }
    .message-danger {
        @extend %message;
        color: red;
        font-size: 18px;
        height: 30px;
    }
```
```
    body {
        margin-right: 5px; 
    }
    .message-danger {
        height: 30px; 
    }
    .message-danger {
        color: red;
        font-size: 18px;
        height: 30px; 
    }
```

#### 继承局限性
+ 无法继承
    - 兄弟选择器是无法继承的(.one + .two)
    - 包含选择器也是无法继承的(.one .two {})
+ 多余继承 
    - 如果有hover属性,那么同样的hover属性也会被继承下来

#### 继承交叉合并
同时继承两个选择器,但是,这两个选择器在同一条语句上面,就形成了交叉继承. 这种用法不太容易控制,应当避免这种用法。
```
    a span{
        height: 100px;
    }
    div .container {
        @extend a, span; 
    }
```
```
    a span, div .container span, a div .container, div a .container, div .container .container { height: 100px; }
```

#### 继承作用域
假如你在media里面定义了一个样式,那么此样式不能继承media之外的选择器.
```
    .three1 {width: 100px;} // 将media写在这里将会出错
    @media screen and (min-width:320px) and (max-width:639px){
        .three1 {width: 100px;} // 写在这里下面的才可以继承
        .container {
            @extend .three1;
            height: 100px;
        }  
    }
```
> 在@media中暂时不能@extend @media外的代码片段，以后将会可以。
***

### **- Mixin & Include -**
Mixin有点像C语言的宏（macro），是可以重用的代码块。
> @mixin通过@include调用后解析出来的样式是以拷贝形式存在的，而下面的继承则是以联合声明的方式存在的，所以从3.2.0版本以后，建议传递参数的用@mixin，而非传递参数类的使用下面的继承%。
#### 不带参数混合宏
使用`@mixin`命令，定义一个代码块。
```
　　@mixin ul-unstyle{
        list-style:none;
    }
```
使用`@include`命令，调用这个mixin。
```
    ul {
　　　　@include ul-unstyle;
　　}
```
#### 带参数混合宏
mixin的强大之处，在于可以指定参数。
```
    $width:50px;
    $display:inline-block;

    @mixin li-unstyle($width,$display){
        list-style:none;
        width:$width;
        display:$display;
    }    
```
使用的时候，根据需要加入参数：
```
　　ul{
        @include li-unstyle($width,$display);
    }
```
```
    /*（表示编译后的结果）
    ul {
    list-style: none;
    width: 50px;
    display: inline-block;
    }
    */
```
#### 带默认值参数混合宏
```
    @mixin li-unstyle($width:5px, $display:block){
        list-style:none;
        width:$width;
        display:$display;
    } 

    li{  
        @include li-unstyle;
    }
    li.sec2{
        @include li-unstyle(20px);
    }    
```
```
    /*
    li {
    list-style: none;
    width: 5px;
    display: block;
    }

    li.sec2 {
    list-style: none;
    width: 20px;
    display: block;
    }
    */
```
#### 混合宏的参数–传一个不同值的参数
```
    $width:50px;
    $display:inline-block;

    @mixin li-unstyle($width,$display){
        list-style:none;
        width:$width;
        display:$display;
    } 

    ul{
        // 直接传值, 不可以打乱顺序
        @include li-unstyle(500px,block);

        // 通过键值对的方式,可以打乱传值的顺序
        @include li-unstyle($display:inline-block, $width:20px);
    }   
```
```
    /*
    ul {
    list-style: none;
    width: 500px;
    display: block;
    }
    */
```
> 多个参数的mixin: 调用时可直接传入值，如@include传入参数的个数小于@mixin定义参数的个数，则按照顺序表示，后面不足的使用默认值，如不足的没有默认值则报错。除此之外还可以选择性的传入参数，使用参数名与值同时传入。

#### 多组值参数mixin:
如果一个参数可以有多组值，如box-shadow、transition等，那么参数则需要在变量后加三个点表示，如$variables...。
```
    $shadow:0 0 3px rgba(#000,.5);
    @mixin sw($shadow...){
        text-shadow:$shadow;
    }

    p{
        @include sw($shadow);
    }
```
```
    /*
    p {
        text-shadow: 0 0 3px rgba(0, 0, 0, 0.5);
    }
    */
```
#### 用`@content`传递内容
@content在sass3.2.0中引入，可以用来解决css3的@media等带来的问题。它可以使@mixin接受一整块样式，接受的样式从@content开始。传递内容就好比在方法中弄了个占位符, 当你调用的时候,所写的内容会直接放在占位符那里;
```
    @mixin style-for-iphone {
        @media only screen and (min-width:320px) and (max-width:568px){
            @content;
        }
    }
    @include style-for-iphone {
        height: 100px;
        font-size: 12px;
    }
```
```
    @media only screen and (min-width: 320px) and (max-width: 568px) {
        height: 100px; 
        font-size: 12px; 
    }
```
***

### **- 数据类型 -**
SASS有以下这么多数据类型数字,字符串,颜色,布尔值,空值,值列表：

- 数字: 1、 2、 13、 10px； 
- 字符串：有引号字符串或无引号字符串，如，”foo”、 ‘bar’、 baz； 
- 颜色：blue、 #04a3f9、 rgba(255,0,0,0.5)； 
- 布尔型：true、 false； 
- 空值： null； 
- 值列表：1.5em 1em 0 2em Helvetica, Arial, sans-serif。[用空格或者逗号分开]

#### Number
数字类型,小数类型,带有像素单位的数字类型,全部都属于Number类型, 详情请点击[这里](http://sass-lang.com/documentation/Sass/Script/Functions.html#number_functions)。
```
    $n1: 1.2;
    $n2: 12;
    $n3: 14px;
    $n4: 1em;
```

#### String
不加双引号的,加双引号的,加单引号的全部都属于String类型, 详细内容请点击[这里](http://sass-lang.com/documentation/Sass/Script/Functions.html#string_functions).
```
    $s1: container;
    $s2: 'container';
    $s3: "container";
```

#### List
List类型的取值,语法nth(list, index),第一个参数表示要取谁的,也就是list类型的变量的名称,第二个表示索引,这里的索引和JavaScript略有不同,JavaScript索引基本上都是从零开始,而这里是从一开始的. 详细内容请点击[这里](http://sass-lang.com/documentation/Sass/Script/Functions.html#list-functions).
```
    $padding: 1px 5px 10px 15px;
    .container {
        padding: nth($padding,2) nth($padding,4);
    }
    // .container { padding: 5px 15px; }
```

#### Map
Map类型取值,语法map-get(map, key),第一个参数表示要取谁的,也就是map类型的变量的名称,第二个参数表示要取的key. 详情请点击[这里](http://sass-lang.com/documentation/Sass/Script/Functions.html#map-functions);
```
    $map: (color: red,background-color: #f00);
    body {
        color: map-get($map, color);
    }
    // body { color: red; }
```

#### Color
```
    /*! 颜色类型*/
    $c1: blue;
    $c2: #fff;
    $c3: rgba(255,255,0,0.5);
    body {
        color: $c3;
    }
    // body { color: rgba(255, 255, 0, 0.5); }
```

#### Boolean
布尔类型分为两种true和false
```
    $bt: true;
    $bf: false;
```

#### Null
null的应用场景如下:
```
$null: null;
body {
    @if $null == null{
        color: red;
    }
}
// body { color: red; }
```
***

### **- 计算 -**
SASS中支持简单的计算。

#### ==, !=
支持所有的类型

#### <,>,<=,>=
只支持Number类型

#### +,-,*,/,%
进行计算的时候最好用空格进行隔开,例如减号如果不隔开,会把两个变量当成一个变量来处理。比如除法,因为CSS有双参数斜杆隔开的写法: 50px/30px , SCSS是无法识别的位除法的,加了括号即可。

> 对于复杂的运算，建议用`（）`括号包起来；只要单位相同,都可以做运算;不同单位,少数会报错。 

#### 颜色也可以做运算; 
```
    $left:20px;
    .div1{
        margin-left:$left + 12px;
    }
```
变量可以支持计算的类型，还是比较多的：
```
    p {
        font: 10px / 8px;             // Plain CSS, no division
        $width: 1000px;
        width: $width / 2;            // Uses a variable, does division
        width: round(1.5) / 2;        // Uses a function, does division
        height: (500px / 2);          // Uses parentheses, does division
        margin-left: 5px + 8px / 2px; // Uses +, does division
        font: (italic bold 10px/8px); // In a list, parentheses don't count
    }
```
***

### **- 条件语句 -**
#### @if判断：
```
　　p {
　　　　@if 1 + 1 == 2 { border: 1px solid; }
　　　　@if 5 < 3 { border: 2px dotted; }
　　}
```
配套的还有@else命令：
```
　　@if lightness($color) > 30% {
　　　　background-color: #000;
　　} @else {
　　　　background-color: #fff;
　　}
```

#### 三目判断

语法为：if($condition, $if_true, $if_false) 。三个参数分别表示：条件，条件为真的值，条件为假的值
```
    $width:900
    body {
    // 跟三目运算符类似
        color: if($width > 800, blue, red);   // blue
    }
    if(true, 1px, 2px)  //1px
    if(false, 1px, 2px) //2px
```
***

### **- 循环语句 -**
#### @for循环
@for循环有两种方式：
* @for $i from <start> through <end>  -  `through 包含 end`
* @for $i from <start> to <end>       -  `to 不包含 end`    
    - $i 表示变量
    - start 表示起始值
    - end 表示结束值
```
　　@for $i from 1 to 3 {
　　　　.border-#{$i} {
　　　　　　border: #{$i}px solid blue;
　　　　}
　　}
    @for $i from 1 through 3 {
        .item-#{$i} { 
            width: 2em * $i; 
        }
    }
```
```
    /*
    .border-1 {
        border: 1px solid blue; 
    }
    .border-2 {
        border: 2px solid blue; 
    }
    .item-1 {
        width: 2em;
    }
    .item-2 {
        width: 4em;
    }
    .item-3 {
        width: 6em;
    }
    */
```
#### @while循环
使用while 需要注意以下几点:
* 第一: 变量要提前声明
* 第二: while里面可以设置步长
```
    $i: 4;
　　@while $i > 0 {
　　　　.item-#{$i} { width: 2em * $i; }
　　　　$i: $i - 2;
　　}    
```
```
    /*
    .item-4 {
        width: 8em; 
    }
    .item-2 {
        width: 4em; 
    }    
    */
```
#### @each遍历

##### 常规遍历
@each 循环就是去遍历一个列表，然后从列表中取出对应的值,指令的形式：`@each $var in <list>`
```
    @each $member in a, b {
　　　　.#{$member} {
　　　　　　background-image: url("/image/#{$member}.jpg");
　　　　}
　　}

    $k: 1;  //可以加入步长控制，默认会自增1
    $test:top,right,bottom,left;
    @mixin btn-extend{
        @each $i in  $test{
            border-#{$i}:5px;
            $k: $k + 1;    //可以加入步长控制，默认会自增1
        }
    }

    .btn{
    @include btn-extend;
    }
```
```
    /*
    .a{
        background-image: url("/image/a.jpg");
    }
    .b{
        background-image: url("/image/b.jpg");
    }    
    .btn {
        border-top: 5px;
        border-right: 5px;
        border-bottom: 5px;
        border-left: 5px;
    }
    */
```
##### 遍历list

这里list出现的方式是以`key:value`的形式出现的($key表示键值,$color表示值)；如果是单数据的变量,那么可以在外边定一个索引,内部执行加1 操作,也可以得到相应的效果.
```
    @each $key, $color in (default, green), (dange,blue), (error, red) {
        .aler-#{$key} {
            color: $color;
        }
    }
```
```
    .aler-default { color: green; }
    .aler-dange { color: blue; }
    .aler-error { color: red; }
```

##### 遍历map

遍历map $key表示键值, $val表示值
```
    @each $key, $val in (default: green, dange: blue, error: red) {
        .alert-#{$key} {
            color: $val;
        }
    }
```
```
    .aler-default { color: green; }
    .aler-dange { color: blue; }
    .aler-error { color: red; }
```
> map的示例
```
    @function buildContainer($num: 5) {
        $map: (defaultValue: 0);
        $rate: percentage(1 / $num); // percentage 求出百分比
        @for $i from 1 through 5 {
            $tempMap: (col#{$i} : $rate * $i);
            $map: map-merge($map, $tempMap);
        }
        $map: map-remove($map, defaultValue);

        @return $map;
    }
    @mixin buildContainer($num: 5) {
        $map: buildContainer($num);
        @each $key, $val in $map {
            .#{$key} {
                width: $val;
            }
        }
    }

    @include buildContainer();
```
```
    .col1 { width: 20%; }
    .col2 { width: 40%; }
    .col3 { width: 60%; }
    .col4 { width: 80%; }
    .col5 { width: 100%; }
```
***

### **- 函数 -**

#### 内置函数
内置函数是系统给我们定义好了的一些函数,详情请点击[这里](http://sass-lang.com/documentation/Sass/Script/Functions.html)

##### 字符串与数字函数
* unquote()函数 : 只会去除最外层的字符串,不处理中间的字符串,没有字符串符号则不处理。
```
    p:before{
        content:unquote("sss");
    }

    p:before{
        content:unquote('"sss"');
    }
```
```
    /*
    p:before {
        content: sss;
    }

    p:before {
        content: "sss";
    }
    */
```
* to-upper-case(),to-lower-case() : 转换大小写
```
    .test {
        text: to-upper-case(aaaaa);
        text: to-upper-case(aA-aAAA-aaa);
    }

    .test2{
        text: to-lower-case(AAAZDc)
    }
```
```
    /*
    .test {
        text: AAAAA;
        text: AA-AAAA-AAA;
    }

    .test2 {
        text: aaazdc;
    }
    */
```

##### 数字函数
* percentage($value)：将一个不带单位的数转换成百分比值；
* round($value)：将数值四舍五入，转换成一个最接近的整数；
* ceil($value)：将大于自己的小数转换成下一位整数；
* floor($value)：将一个数去除他的小数部分；
* abs($value)：返回一个数的绝对值；
* min($numbers…)：找出几个数值之间的最小值；
* max($numbers…)：找出几个数值之间的最大值；
* random(): 获取随机数
```
    $fs:5.3;
    $t:10 99 1 2 3 4 5 6;
    .test{
        height:percentage($fs);
        width:round($fs);
        width:ceil($fs);
        width:floor($fs);
        width:abs($fs);
        width:min($t...);
        width:max($t...);
        border-radius:random();
    }
```
```
    /*
    .test {
        height: 530%;
        width: 5;
        width: 6;
        width: 5;
        width: 5.3;
        width: 1;
        width: 99;
        border-radius: 0.28517;
    }
    */
```
##### 列表函数
* length($list)：返回一个列表的长度值； 
```
    inputlength(10px) print 1 ,input length(border 1px solid) print3;
```
* nth(list,n)：返回一个列表中指定的某个标签值;
```
    inputnth(10px 20px 30px,2),print 20px;
```
* join(list1,list2, [$separator])：将两个列给连接在一起，变成一个列表(最多只能两个)。
```
    input:join((blue,red),(#abc #def)) ,print (#0000ff, #ff0000, #aabbcc, #ddeeff)；
```
* append(list1,val, [$separator])：将某个值放在列表的最后；
```
    input: append(10px 20px ,30px) , print (10px 20px 30px);
```
* zip($lists…)：将几个列表结合成一个多维的列表；
```
    input:zip(1px 2px 3px,solid dashed dotted,green blue red) , print ((1px "solid" #008000), (2px "dashed"
 #0000ff), (3px "dotted" #ff0000));
```
* index(list,value)：返回一个值在列表中的位置值; 
```
    input : index(1px solid red, solid) , print 2;
```

##### 颜色函数
SASS提供了一些内置的颜色函数，以便生成系列颜色。
```
　　lighten(#cc3, 10%) // #d6d65c
　　darken(#cc3, 10%) // #a3a329
　　grayscale(#cc3) // #808080
　　complement(#cc3) // #33c
```
***

### **- 自定义函数 -**
SASS允许用户编写自己的函数,Sass需要在function和return前面加一个@符号,例如:
```
　　@function double($n) {
　　　　@return $n * 2;
　　}
　　#sidebar {
　　　　width: double(5px);
　　}
```
***

### **- 编译输出 -**

#### @debug
`@debug` 在 SASS 中是用来调试的，当你的在 SASS 的源码中使用了 `@debug` 指令之后

在命令终端会输出你设置的提示 Bug: 
```
    @debug 10em + 12em; 
```
会输出： 
`Line 1 DEBUG: 22em`
***

#### @warn 和 @error
这两个也是方便调试用的,显示警告信息和错误信息…..类似JS的`console.log()`;
```
@warn "这里的内容会在控制台输出"
```
***

未完待续...