# 注释
语法：

    <!--注释-->

# <head>标签
`<head></head>` 标签描述了文档的各种属性和信息，包括文档的标题。绝大多数文档头部包含的数据都不会真正作为内容显示给读者。

    <head>
      <!--该标签的内容是网页的标题信息，它会出现在浏览器的标题栏中，该标签用于告诉用户和搜索引擎这个网页的主要内容是什么，搜索引擎可以通过网页标题，迅速判断网页的主题-->
      <title>...</title>
      <!--关于 HTML 文档的元信息-->
      <meta>
      <!--文档与外部资源的关系-->
      <link>
      <!--样式信息-->
      <style>...</style>
      <!--JavaScript 代码-->
      <script>...</script>
    </head>

# <body></body>标签
网页上展示的内容一般都放在该标签中。

    <body>
      <h1>标题1</h1>
      <p>段落</p>
      ...
    </body>

# 标题
通过标签 `<h1>~<h6>` 进行定义，语法：

    <h1>一级标题</h1>
    <h2>二级标题</h2>
    <h6>六级标题</h6>
# 段落
语法：

    <p>段落</p>

# 链接
通过标签 `<a>` 进行定义，语法：

    <a href="http://www.baidu.com" title="鼠标滑过显示的文本">百度</a>
例如：<a href="http://www.baidu.com" title="鼠标滑过显示的文本">百度</a>

>* 属性 `href` 表示链接地址，分为内部链接（试着只输入www.baidu.com），外部链接，锚链接（本页面）。
>* 属性 `title` 在鼠标滑过时显示。
>* 属性 `target` 表示链接是在当前窗口还是新窗口打开。`_blank` 表示在新窗口中打开链接；`_parent` 在父窗口打开；`_self` 当前窗体中打开链接，为默认值；`_top` 在当前窗体打开链接，并替换当前整个窗体

除此之外我们还可以使用 `<a></a>` 标签链接 Email 地址，使用 `mailto` 能做很多事，如下图所示：

|功能|关键字|功能详情|示例|
|-|-|-|-|
|邮箱地址|mailto: |浏览器会自动调用默认的客户端电子邮件程序，并在收件人框中自动填上收件人的地址|&lt;a href="mailto:xxx@gmail.com"&gt;发送谷歌邮箱&lt;/a&gt;|
|抄送地址|cc=|在收件人后用 cc=地址，可以填写抄送地址|&lt;a href="mailto:xxx@gmail.com?cc=gmailAdmin@gmail.com"&gt;发送谷歌邮箱&lt;/a&gt;|
|密件抄送地址|bcc=|在收件人地址后用 bcc=地址，可以填上密件抄送地址|&lt;a href="mailto:xxx@gmail.com?bcc=pp@gmail.com"&gt;发送谷歌邮箱&lt;/a&gt;|
|多个收件人、抄送、密件抄送人|;|用分号隔开多个收件人的地址，可以实现发送给多个收件人功能|&lt;a href="mailto:xxx@gmail.com;yyy@gmail.com"&gt;发送谷歌邮箱&lt;/a&gt;|
|邮件主题|subject=|用 subject= 添加邮件主题|&lt;a href="mailto:xxx@gmail.com?subject=发送邮件"&gt;发送谷歌邮箱&lt;/a&gt;|
|邮件内容|body=|用 body= 添加邮件内容|&lt;a href="mailto:xxx@gmail.com?body=这是一封邮件"&gt;发送谷歌邮箱&lt;/a&gt;|

**注意：** 如果 `mailto` 后面同时有多个参数的话，第一个参数必须以 `?`开头，后面的参数每一个都以 `&` 分隔。

    <a href="maile:xxx@gmail.com?cc=yyy@gmail.com&bcc=zzz@gmail.com&subject=主题&body=内容">邮件发送</a>

# 图像
通过标签 `<img>` 进行定义，语法：

    <img src="xxx.jpg" title="提示文本" alt="下载失败时的替换文本" width="400" height="100">

# 加强语气
当要强调某些内容时，可以使用 `<em>或<strong>`。他们的区别是 `<em>`表示强调，用斜体表示；`<strong>` 表示更强烈的强调，用粗体表示。

    <em>斜体内容</em>
    <strong>粗体内容</strong>

# 设置单独样式
1. `<em></em>` 和 `<strong></strong>` 是为了强调一段话中的关键字时使用。语义是强调。
2. `<span>` 标签没有语义，它的作用是为了设置<span style="color:blue">单独的样式</span>。

        <span style="color:blue">蓝色字体</span>

# 短文本引用
使用 `<q></q>` 标签的文字会自动加上双引号，表示该部分属于引用至其他作者。例如：
<q>这是引用</q>，代码为 `<q>这是引用</q>`。

    <q>引用</q>

# 长文本引用
使用 `<blockquote></blockquote>` 可以引用一段长文本。例如：<blockquote>今夕何夕兮，搴舟中流。
今日何日兮，得与王子同舟。
蒙羞被好兮，不訾诟耻。
心几烦而不绝兮，得知王子。
山有木兮木有枝，心悦君兮君不知。</blockquote>

浏览器对`<blockquote></blockquote>` 的解析是缩进样式。

    <blockquote>今夕何夕兮，搴舟中流。
                今日何日兮，得与王子同舟。
                蒙羞被好兮，不訾诟耻。
                心几烦而不绝兮，得知王子。
                山有木兮木有枝，心悦君兮君不知。
    </blockquote>

# 换行
可以使用 `<br/>` 标签来进行换行，该标签相当于<strong>回车</strong>。例如：<blockquote>今夕何夕兮，搴舟中流。<br/>
今日何日兮，得与王子同舟。<br/>
蒙羞被好兮，不訾诟耻。<br/>
心几烦而不绝兮，得知王子。<br/>
山有木兮木有枝，心悦君兮君不知。</blockquote>

    <blockquote>今夕何夕兮，搴舟中流。<br/>
                今日何日兮，得与王子同舟。<br>
                蒙羞被好兮，不訾诟耻。<br/>
                心几烦而不绝兮，得知王子。<br/>
                山有木兮木有枝，心悦君兮君不知。
    </blockquote>

该标签属于空标签，所有我们可以直接在开始时标签中加入 `\` 来结束。

# 空格
在 HTML 中，输入的换行、空格（只显示一个空格）都是没有作用的。当要输入空格时使用 `&nbsp;`。

    &nbsp;

<hr/>
# 水平横线
效果如上。

    <hr/>

# 地址信息
一般网页中会有一些网站的联系地址信息需要在网页中展现出来，可以使用 `<adress></adress>` 标签。默认样式为斜体。

    <adress>北京东路</adress>

# 插入代码
一般插入单行代码使用 `<code></code>` 标签。

插入多汗代码使用 `<pre></pre>`

    <code>int i=1;</code>
    <pre>int i=1;
         int j=++i;
    </pre>
# 无序列表
语法：

    <ul>
      <li>足球</li>
      <li>篮球</li>
      <li>乒乓球</li>
    </ul>

效果如下：
<ul>
  <li>足球</li>
  <li>篮球</li>
</ul>

# 有序列表
语法：

    <ol>
      <li>第一</li>
      <li>第二</li>
    </ol>

效果：
<ol>
  <li>第一</li>
  <li>第二</li>
</ol>

# <div></div>排版的使用
<div style="color:yellow">
语法：`<div>...</div>`
<br/>    
例如：
    `<div style="color:yellow">...</div>`
<br/>
效果：
当然是变黄了啊
</div>
在网页制作中，可以把一些独立的逻辑部分划分出来，放在一个 `<div></div>` 中，这个 `<div></div>` 就相当于一个容器。<strong>逻辑部分:</strong>他是页面上相互关联的逻辑部分。

# 表格
创建一个表格需要四个元素：
<pre>
  <ol>
    <li>table</li>
    <li>tbody</li>
    <li>th</li>
    <li>tr</li>
    <li>td</li>
  </ol>
</pre>

说明：
<ol>
 <li><code>&lt;table&gt;...&lt;/table&gt;</code>该标签声明这是表格。</li>
 <li><code>&lt;tbody&gt;...&lt;/tbody&gt;</code>一般表格都是加载完成才进行显示，使用该标签后，可以一部分一部分显示，每部分为该标签下的内容。</li>
 <li><code>&lt;th&gt;...&lt;/th&gt;</code>该标签表示表格的表头。</li>
 <li><code>&lt;tr&gt;...&lt;/tr&gt;</code>该标签表示表格的一行。</li>
 <li><code>&lt;td&gt;...&lt;/td&gt;</code>该标签表示一行中每一列的内容。</li>
</ol>
<strong>注意：</strong>在没用为表格添加 CSS 样式之前，在浏览器中显示是没有表格线的。<br/>

其他常用标签：
<ur>
  <li><code>&lt;caption&gt;...&lt;/caption&gt;</code>该标签用于显示表格标题。</li>
</ur>
<br/>

其他常用属性：
<ur>
  <li><code>&lt;table summary="表格简介文本"&gt;...&lt;/table&gt;</code>该标签用于显示表格标题。</li>
</ur>

<table summary="测试表格">
  <caption>货物表</caption>
  <tr>
    <th>名称</th>
    <th>单价（元）</th>
  </tr>
  <tr>
    <td>铅笔</td>
    <td>0.5</td>
  </tr>
  <tr>
    <td>钢笔</td>
    <td>5</td>
  </tr>
</table>

上述表代码如下：

    <table summary="测试表格">
      <caption>货物表</caption>
      <tr>
        <th>名称</th>
        <th>单价（元）</th>
      </tr>
      <tr>
        <td>铅笔</td>
        <td>0.5</td>
      </tr>
      <tr>
        <td>钢笔</td>
        <td>5</td>
      </tr>
    </table>

# 表单
网站与用户交互是使用 HTML 表单(form)。表单是可以把浏览者输入的数据传送到服务器端，这样服务器端程序就可以处理表单传过来的数据。

语法：

    <form method="post/get" action="服务器文件">...</form>

属性说明：
* `action`浏览者输入的数据被传送到的地方，比如一个 PHP 页面。
* `method` 数据传送方式。

所有表单控件（文本框、文本域、按钮、单选框、复选框等）都必须放在`<form></form>`中。

# 文本(密码)输入框
语法：

    <form>
      <input type="text/password" name="名称" value="输入框默认值"/>
    </form>

1. `type` 当值为 `text` 时，输入框为文本输入框。值为 `password` 时，输入框为密码输入框。
2. `name` 为文本框命名，以备后台程序 ASP、PHP 使用。
3. `value` 为文本输入框设置默认值。

例如：

    <form>
      <label>文本框</label><input type="text" name="用户名" value="请输入用户名"/>
      <label>密码框</label><input type="password" name="密码"/>
    </form>

效果如下：
<form>
  <label>文本框</label><input type="text" name="用户名" value="请输入用户名"/>
  <label>密码框</label><input type="password" name="密码"/>
</form>

# 文本域


当用户需要输入大段文字时，需要用到文本域。

语法：

    <textarea rows="行数" cols="列数">文本</textarea>

属性说明：
1. `rows` 多行输入域的行数。
2. `cols` 多行输入域的列数。
3. 在标签 `<textarea>...</textarea>` 之间可以输入默认值。

例如：

    <textarea rows="5" cols="10">多行文本框</textarea>

效果如下：
<textarea rows="5" cols="10">多行文本框</textarea>

# 单选框、复选框
语法：

    <input type="radio/checkbox" value="值" name="名称" checked="checked"/>

属性说明：
1. `type` 当值为 `radio` 时为单选框。为 `checkbox` 为复选框。
2. `value` 提交数据到服务器的值。
3. `name` 为控件命名，以备后台 ASP、PHP 使用。
4. `checked` 当设置 `checked=checked` 时，该选项被默认选中。

**注意：** 在单选框中，同一组的单选按钮名字必须一致，也就是 `name` 的值必须一样。这样同一组中的单选框才有单选作用。

例如：

    <form>
      <label>男</label><input type="radio" value="男" name="男单选框" checked="checked"/><br/>
      <label>女</label><input type="radio" value="女" name="女单选框"/><br/>
      <label>你喜欢 HTML吗？</label><br/>
      <input type="radio" value="喜欢" name="radiolike" checked="checked">喜欢
      <input type="radio" value="不喜欢" name="boring">不喜欢<br/>
      <label>你的爱好是：</label><br/>
      <input type="checkbox" value="guitar" name="吉他" checked="checked">吉他
      <input type="checkbox" value="football" name="足球" cheecked="cheecked">足球
      <input type="checkbox" value="read" name="看书">看书
    </form>

效果为：
<form>
  <label>男</label><input type="radio" value="男" name="性别单选框" checked="checked"/>
  <label>女</label><input type="radio" value="女" name="性别单选框"/><br/>
  <label>你喜欢 HTML吗？</label><br/>
  <input type="radio" value="喜欢" name="html" checked="checked">喜欢
  <input type="radio" value="不喜欢" name="html">不喜欢<br/>
  <label>你的爱好是：</label><br/>
  <input type="checkbox" value="guitar" name="吉他" checked="checked">吉他
  <input type="checkbox" value="football" name="足球" checked="checked">足球
  <input type="checkbox" value="read" name="看书">看书
</form>

# 下拉列表框
语法：

    <form>
      <label>爱好</label>
      <select multiple="multiple">
        <option value="看书">看书</option>
        <option value="音乐">音乐</option>
        <option value="电影" selected="selected">电影</option>
        <option value="游戏">游戏</option>
      </select>
    </form>

属性说明：
1. `<select>...</select>` 内包含下拉列表框选项，每个选项由 `<option></option>` 声明。
2. `multiple=multiple` 设置下拉列表多选功能。在 windows
2. `value` 该属性的值为向服务器提交的值。
3. `<option>...</option>` 中间的值为显示的可选值。
4. 设置了 `selected="selected"` 的默认被选中。

效果：
<form>
  <label>爱好</label>
  <select>
    <option value="看书">看书</option>
    <option value="音乐">音乐</option>
    <option value="电影" selected="selected">电影</option>
    <option value="游戏">游戏</option>
  </select>
</form>

<form>
  <label>爱好</label>
  <select multiple="multiple">
    <option value="看书">看书</option>
    <option value="音乐">音乐</option>
    <option value="电影" selected="selected">电影</option>
    <option value="游戏">游戏</option>
  </select>
</form>

# 提交/重置按钮
在表单中有两种按钮可以使用，分别是**提交按钮**和**重置按钮**。

语法：

    <input type="submit/reset" value="提交"/>

相关说明：
1. `type`  值为 `submit` 时为提交按钮并且才有提交作用；值为 `reset` 为重置按钮且有重置作用。
2. `value` 按钮上显示的文字。

例如:

    <form>
      <input type="text" value="请输入内容"/>
      <input type="submit" value="登录"/>
      <input type="reset" value="重置"/>
    </form>

效果：
<form>
  <input type="text" value="请输入内容"/>
  <input type="submit" value="登录"/>
  <input type="reset" value="重置"/>
</form>

# label标签
label 标签不会向用户呈现任何特殊效果，它的作用是为鼠标用户改进了可用性。如果你在 label 标签内点击文本，就会触发此控件。就是说，当用户单击选中该 label 标签时，浏览器就会自动将焦点转到和标签相关的表单控件上。

不加label的话鼠标一定要点击小圆点才能激活条目,加了label可以直接点击对应的文字来激活条目。

label的作用就是获得焦点，在列子中，把鼠标移动到文字上（男、女、输入你的邮箱地址），同样可以激活控件进行选择，输入。但是如果不加label的话，鼠标就必须移动到控件上面。

语法：

    <label for="控件id名称">名字</label>

**注意：** 标签的 `for` 属性值要与对应控件的 `id` 属性值相同。

例如：

    <form>
      <label>你的性别？</label><br/>
      <label for="male">男</label>
      <input type="radio" name="radiomale" id="male"/>
      <label for="female">女</label>
      <input type="radio" name="radiofemale" id="female"/>
    </form>

效果：
<form>
  <label>你的性别？</label><br/>
  <label for="male">男</label>
  <input type="radio" name="radio" id="male"/>
  <label for="female">女</label>
  <input type="radio" name="radio" id="female" checked="checked"/>
</form>
