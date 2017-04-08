## **web前端命名规范**

前端技能汇总这个项目详细记录 了前端工程师牵涉到的各方面知识。在具备基本技能之后可以在里面找到学习 的方向，完善技能和知识面。

frontend-dev-bookmarks是老外总结的前端开发资源。覆盖面非常广。包括各种知识点、工具、技术，非常全面。

#### 前言：

以下是个人觉得入门阶段应该熟练掌握的基础技能：

1. HTML4，HTML5语法、标签、语义

2. CSS2.1，CSS3规范，与HTML结合实现各种布局、效果

3. Ecma-262定义的javascript的语言核心，原生客户端javascript，DOM操作，HTML5新增功能

4. 一个成熟的客户端javascript库，推荐jquery

5. 一门服务器端语言：如果有服务器端开发经验，使用已经会的语言即可，如果没有服务器端开发经验，熟悉Java可以选择Servlet，不熟悉的可以选PHP，能实现简单登陆注册功能就足够支持前端开发了，后续可能需要继续学习，最基本要求是实现简单的功能模拟

6. HTTP文本编辑器：推荐Sublime Text，支持各种插件、主题、设置，使用方便

7. 浏览器：推荐Google Chrome，更新快，对前端各种标准提供了非常好的支持

8. 调试工具：推荐Chrome自带的Chrome develop tools，可以轻松查看DOM结构、样式，通过控制台输出调试信息，调试javascript，查看网络等

9. 辅助工具：PhotoShop编辑图片、取色，fireworks量尺寸，AlloyDesigner对比尺寸，以及前面的到的Chrome develop tools

对于经验资深的前端er，在给web布局时，相信都会很注重标签和命名的规范。尤其是随着html5的普及发展，更是把web前端语义化推向一个新的台阶上。比如html5给我们新增的语义标签：header、nav、main、aside、footer、section、article等等。

那么对于web语义化，有什么优势呢？

一个得到广泛推崇的东西，必然有它的优势所在。web语义化：

1. 可以让人一目了然这块是什么鬼，那块是什么鬼，对于项目的维护或者优化都是非常有意义的。
2. 随着html5语义化标签的出现，我推测以后web语义化对于seo优化，还是非常有利的。也就是说，seo优化，必然也要考虑web语义化。

如：<header></header>可以很好的代替传统的<div id="header"></div>。

那怎样愉快的玩耍web语义化呢？

1. 标签语义化，如在合适的地方用合适的语义化标签，如头部可用<header>、尾部可用<footer>；

2. 命名语义化，包括html的id和class的命名，javascript相关命名；如#header{}、.footer{}、等。

下面是常见的命名参考规范：

#### 一、 主体

|      |                       |
| ---- | --------------------- |
| 头部   | header                |
| 内容   | content/container     |
| 尾部   | footer                |
| 导航   | nav                   |
| 侧栏   | sidebar               |
| 栏目   | column                |
| 整体布局 | wrapper               |
| 左右中  | left / right / center |
| 登录条  | loginbar              |
| 标志   | logo                  |
| 广告   | banner                |
| 页面主体 | main                  |
| 热点   | hot                   |
| 新闻   | news                  |
| 下载   | download              |
| 子导航  | subnav                |
| 菜单   | menu                  |
| 子菜单  | submenu               |
| 搜索   | search                |
| 友情链接 | friendlink            |
| 页脚   | footer                |
| 版权   | copyright             |
| 滚动   | scroll                |
| 标签页  | tab                   |
| 文章列表 | list                  |
| 提示信息 | msg                   |
| 小技巧  | tips                  |
| 栏目标题 | title                 |
| 加入   | join                  |
| 指南   | guild                 |
| 服务   | service               |
| 注册   | regsiter              |
| 状态   | status                |
| 投票   | vote                  |
| 合作伙伴 | partner               |

#### 二、 css注释的写法

   如内容区，Html注释的写法 ：<!--header头部-->

#### 三、 id的命名规范

| （1）页面结构      |                   |
| ------------ | ----------------- |
| 容器           | container         |
| 页头           | header            |
| 内容           | content/container |
| 页面主体         | main              |
| 页尾           | footer            |
| 导航           | nav               |
| 侧栏           | sidebar           |
| 栏目           | column            |
| 页面外围控制整体布局宽度 | wrapper           |
| 左右中          | left/right/center |

| （2）导航 |              |
| ----- | ------------ |
| 导航    | nav          |
| 主导航   | mainnav      |
| 子导航   | subnav       |
| 顶导航   | topnav       |
| 边导航   | sidebar      |
| 左导航   | leftsidebar  |
| 右导航   | rightsidebar |
| 菜单    | menu         |
| 子菜单   | submenu      |
| 标题    | title        |
| 摘要    | summary      |

| （3）功能 |           |
| ----- | --------- |
| 标志    | logo      |
| 广告    | banner    |
| 登陆    | login     |
| 登录条   | loginbar  |
| 注册    | regsiter  |
| 搜索    | search    |
| 功能区   | shop      |
| 标题    | title     |
| 加入    | joinus    |
| 状态    | status    |
| 按钮    | btn       |
| 滚动    | scroll    |
| 标签页   | tab       |
| 文章列表  | list      |
| 提示信息  | msg       |
| 当前的   | current   |
| 小技巧   | tips      |
| 图标    | icon      |
| 注释    | note      |
| 指南    | guild     |
| 服务    | service   |
| 热点    | hot       |
| 新闻    | news      |
| 下载    | download  |
| 投票    | vote      |
| 合作伙伴  | partner   |
| 友情链接  | link      |
| 版权    | copyright |

#### 四、 class的命名
（1）)颜色：使用颜色的名称或者16进制代码，如：

```
.red { color: red; }
.f60 { color: #f60; }
.ff8600 { color: #ff8600; }
```

（2）字体大小，直接使用“font+字体大小”作为名称，如：

```
.font12px { font-size: 12px; } 
.font9pt {font-size: 9pt; }
```

（3）对齐样式，使用对齐目标的英文名称，如：

```
.left { float:left; } 
.bottom { float:bottom; }
```

（4）标题栏样式，使用“类别+功能”的方式命名，如：

```
.barnews { } 
.barproduct { }
```

#### 注意事项：

1. 一律小写；
2. 尽量用英文；
3. 尽量不加中杠和下划线；
4. 尽量不缩写，除非一看就明白的单词，如：wrapper可以写成wrap。
5. css文件命名规范：
| 板块    | 命名规则        |
| ----- | ----------- |
| 主要的   | master.css  |
| 模块    | module.css  |
| 基本共用  | base.css    |
| 布局，版面 | layout.css  |
| 主题    | themes.css  |
| 专栏    | columns.css |
| 文字    | font.css    |
| 表单    | forms.css   |
| 补丁    | mend.css    |
| 打印    | print.css   |

