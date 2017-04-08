## web前端知识体系

### HTML基础
HTML 是用来描述网页的一套标记标签，是我们在web前端开发中的基础。下面分享下HTML的基础知识，以及在自学过程中一些比较常用的和重要的HTML知识点。

#### 1. 基础标签
    创建一个HTML文档 <html></html>
    设置文档标题以及其他不在WEB网页上显示的信息 <head></head>
    将文档的题目放在标题栏中 <title></title>
    设置文档的可见部分 <body></body>
    标签定义文档与外部资源的关系 <link>
    标签用于定义客户端脚本 <script>

#### 2. 文本标签
    最大的标题 <h1></h1>
    最小的标题 <h6></h6>
    黑体字 <b></b>、<strong></strong>
    斜体字 <i></i>
    创建一个引用，通常是斜体 <cite></cite>
    加重一个单词（通常是斜体加黑体） <em></em>

#### 3. 链接
    超链接 <a href=”URL”></a>
    自动发送电子邮件的链接 `<a href=”mailto:EMAIL”>···.···</a>`
    位于文档内部的靶位 <a name=”NAME”></a>
    指向位于文档内部靶位的链接 <a href=”#NAME”></a>

#### 4. 格式排版
    可定义文档中的分区或节，常用来布局 <div>
    创建一个新的段落 <p>
    插入一个回车换行符 <br>
    加入一条水平线 <hr />
    创建一个定义列表 <dl></dl>
    放在每个定义术语词之前 <dt>
    放在每个定义之前 <dd>
    创建一个标有数字的列表 <ol></ol>
    放在每个数字列表项之前，并加上一个数字 <li>
    创建一个标有圆点的列表 <ul></ul>
    放在每个圆点列表项之前，并加上一个圆点 <li>

#### 5. 图形元素
    添加一个图像 <img src=”name” width=”” height=”” />
    表格
      创建一个表格 <table></table>
      设置表格头：一个通常使用黑体居中文字的格子 <th></th>
      开始表格中的每一行 <tr></tr>
      开始一行中的每一个格子 <td></td>

#### 6. 表单
    对于功能性的表单，HTML仅仅是产生表单的表面样子，为后台提供数据。
    创建所有表单 <form></form>
    创建一个滚动菜单，size设置在需要滚动前可以看到的表单项数目 <select multiple name=”NAME” size=</select>
    设置每个表单项的内容 <option>
    创建一个下拉菜单 <select name=”NAME”></select>
    文本框区域，列的数目设置宽度，行的数目设置高度 <textarea name=”NAME” cols=40 rows=8></textarea>
    复选框，文字在标签后面 <input type=”checkbox” name=”NAME”>
    单选框，文字在标签后面 <input type=”radio” name=”NAME” value=”x”>
    单行文本输入区域，size设置以字符计的宽度 <input type=text name=”foo” size=20>
    submit（提交）按钮 <input type=”submit” value=”NAME”>
    使用图象的submit（提交）按钮 <input type=”image” border=0 name=”NAME” src=”name.gif”>
    reset（重置）按钮 <input type=”reset”>