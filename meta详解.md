## meta标签的组成

meta标签共有两个属性，它们分别是http-equiv属性和name属性，不同的属性又有不同的参数值，这些不同的参数值就实现了不同的网页功能。

name属性主要用于描述网页，与之对应的属性值为content，content中的内容主要是便于搜索引擎机器人查找信息和分类信息用的。

meat标签的name属性语法格式是：<meta name="参数" content="具体的参数值">。

其中name属性主要有以下几种参数：

### Keywords(关键字)

说明：keywords用来告诉搜索引擎你网页的关键字是什么。

举例：<meta name ="keywords" content="science, education,culture,politics,ecnomics，relationships, entertaiment, human">

### description(网站内容描述)

说明：description用来告诉搜索引擎你的网站主要内容。

举例：<meta name="description" content="This page is about the meaning of science, education,culture.">

### robots(机器人向导)

说明：robots用来告诉搜索机器人哪些页面需要索引，哪些页面不需要索引。

content的参数有all,none,index,noindex,follow,nofollow。默认是all。

举例：<meta name="robots" content="none">

### author(作者)

说明：标注网页的作者

举例：<meta name="author" content="zys666,zys666@21cn.com">

### http-equiv

顾名思义，相当于http的文件头作用，它可以向浏览器传回一些有用的信息，以帮助正确和精确地显示网页内容，与之对应的属性值为content，content中的内容其实就是各个参数的变量值。

meat标签的http-equiv属性语法格式是：<meta http-equiv="参数" content="参数变量值">；其中http-equiv属性主要有以下几种参数：

#### Expires(期限)

说明：可以用于设定网页的到期时间。一旦网页过期，必须到服务器上重新传输。

用法：<meta http-equiv="expires" content="Fri, 12 Jan 2001 18:18:18 GMT">

注意：必须使用GMT的时间格式。

#### Pragma(cache模式)

说明：禁止浏览器从本地计算机的缓存中访问页面内容。

用法：<meta http-equiv="Pragma" content="no-cache">

注意：这样设定，访问者将无法脱机浏览。

#### Refresh(刷新)

说明：自动刷新并指向新页面。

用法：<meta http-equiv="Refresh" content="2；URL=http://www.chinayancheng.net">

注意：其中的2是指停留2秒钟后自动刷新到URL网址。

#### Set-Cookie(cookie设定)

说明：如果网页过期，那么存盘的cookie将被删除。

用法：<meta http-equiv="Set-Cookie" content="cookievalue=xxx; expires=Friday, 12-Jan-2001 18:18:18 GMT； path=/">

注意：必须使用GMT的时间格式。

#### Window-target(显示窗口的设定)

说明：强制页面在当前窗口以独立页面显示。

用法：<meta http-equiv="Window-target" content="_top">

注意：用来防止别人在框架里调用自己的页面。

#### content-Type(显示字符集的设定)

说明：设定页面使用的字符集。

用法：<meta http-equiv="content-Type" content="text/html; charset=gb2312">


## meta标签的功能

上面我们介绍了meta标签的一些基本组成，接着我们再来一起看看meta标签的常见功能：

### 帮助主页被各大搜索引擎登录

meta标签的一个很重要的功能就是设置关键字，来帮助你的主页被各大搜索引擎登录，提高网站的访问量。在这个功能中，最重要的就是对Keywords和description的设置。因为按照搜索引擎的工作原理,搜索引擎首先派出机器人自动检索页面中的keywords和decription，并将其加入到自己的数据库，然后再根据关键词的密度将网站排序。因此，我们必须设置好关键字，来提高页面的搜索点击率。下面我们来举一个例子供大家参考：
```
<**meta** name="keywords" content="政治,经济, 科技,文化, 卫生, 情感，心灵，娱乐，生活，社会，企业，交通">

<**meta** name="description" content="政治,经济, 科技,文化, 卫生, 情感，心灵，娱乐，生活，社会，企业，交通">
```
设置好这些关键字后，搜索引擎将会自动把这些关键字添加到数据库中，并根据这些关键字的密度来进行合适的排序。

### 定义页面的使用语言

这是meta标签最常见的功能,在制作网页时,我们在纯HTML代码下都会看到它,它起的作用是定义你网页的语言,当浏览者访问你的网页时,浏览器会自动识别并设置网页中的语言,如果你网页设置的是GB码,而浏览者没有安装GB码,这时网页只会呈现浏览者所设置的浏览器默认语言。同样的,如果该网页是英语,那么charset=en。下面就是一个具有代表性的例子：
```
<meta http-equiv="content－Type" content="text/html; charset=gb2312">
```
该代码就表示将网页的语言设置成国标码。

### 自动刷新并指向新的页面

如果你想使您的网页在无人控制的情况下，能自动在指定的时间内去访问指定的网页，就可以使用meta标签的自动刷新网页的功能。下面我们来看一段代码：
```
<meta http-equiv="refresh" content="2; URL=http://www.yeah.net">
```
这段代码可以使当前某一个网页在2秒后自动转到http://www.yeah.net页面中去,这就是meta的刷新作用,在content中,2代表设置的时间（单位为秒）,而URL就是在指定的时间后自动连接的网页地址。

### 实现网页转换时的动画效果

使用meta标签，我们还可以在进入网页或者离开网页的一刹那实现动画效果，我们只要在页面的html代码中的<head> </head>标签之间添加如下代码就可以了：
```
<**meta** http-equiv="Page-Enter" content="revealTrans(duration=5.0, transition=20)">

<**meta** http-equiv="Page-Exit" content="revealTrans(duration=5.0, transition=20)">
```
一旦上述代码被加到一个网页中后，我们再进出页面时就会看到一些特殊效果，这个功能其实与FrontPage2000中的Format/Page Transition一样，但我们要注意的是所加网页不能是一个Frame页;

### 网页定级评价

IE4.0以上版本的浏览器可以防止浏览一些受限制的网站,而之所以浏览器会自动识别某些网站是否受限制,就是因为在网站meta标签中已经设置好了该网站的级别,而该级别的评定是由美国RSAC,即娱乐委员会的评级机构评定的,如果你需要评价自己的网站,可以连接到网站http://www.rsac.org/,按要求提交表格,那么RSAC会提供一段meta代码给你,复制到自己网页里就可以了。下面就是一段代码的样例：
```
<**meta** http-equiv="PICS－Label"  content=′(PICS－1.1 "[http://www.rsac.org/ratingsv01.html](http://www.rsac.org/ratingsv01.html)";  l gen true comment "RSACi North America Server"; for "[http://www.rsac.org](http://www.rsac.org/)" on "2001.08.16T08:15－0500"r (n 0 s 0 v 0 l 0))′> >0500"
```
### 控制页面缓冲

meta标签可以设置网页到期的时间,也就是说,当你在Internet Explorer 浏览器中设置浏览网页时首先查看本地缓冲里的页面,那么当浏览某一网页,而本地缓冲又有时,那么浏览器会自动浏览缓冲区里的页面,直到meta中设置的时间到期,这时候,浏览器才会去取得新页面。例如下面这段代码就表示网页的到期时间是2001年1月12日18时18分18秒。

```
<meta http-equiv="expires" content="Friday, 12-Jan-2001 18:18:18 GMT">
```

### 控制网页显示的窗口

我们还可以使用meta标签来控制网页显示的窗口，只要在网页中加入下面的代码就可以了：<metahttp-equiv="window-target" content="_top">，这段代码可以防止网页被别人作为一个Frame调用。