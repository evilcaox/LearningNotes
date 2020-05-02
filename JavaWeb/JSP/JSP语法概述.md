# JSP 语法概述
一般来说，在JSP 页面可以包含的元素如下表。

|JSP 页面元素|简要说明|标签语法|
|-|-|-|
|声明|声明变量与定义方法|<%! Java 声明%>|
|小脚本|执行业务逻辑的 Java 代码|<% Java 代码 %>|
|表达式|用于在 JSP 页面输出表达式的值|<%=表达式%>|
|指令|指定转换时向容器发出的指令|<%@ 指令%>|
|动作|向容器提供请求时的指令|<jsp:动作名>|
|EL 表达式|JSP 2.0 引进的表达式语言|${applicationScope.email}|
|注释|用于文档注释|<%--任意文本--%>|
|模板文本|HTML 标签和文本|同 HTML 规则|

## 1. JSP 脚本元素
在 JSP 页面中有三种脚本元素：声明、小脚本和表达式。
<ol>
<li>JSP 声明
</li>
<p>声明用来在 JSP 页面中声明变量和定义方法。声明的语法为:
<pre>&lt;%! 声明部分 %>
</pre>
例如：<code>&lt;%! int count=0; %&gt;</code><br/>
声明的变量仅在页面第一次载入时由容器初始化一次，初始化后在后面的请求中一直保持该值。<br/>
<strong>注意:</strong>由于声明包含的是声明语句，所以每个变量的声明语句必须以分号结束。
<p/>
<li>JSP 小脚本
</li>
<p>小脚本是嵌入在 JSP 页面的 Java 代码。以 <code>&lt;%</code> 开头，以 <code>%&gt;</code>结尾的标签。小脚本在每次访问页面都被执行一次。小脚本里的 Java 代码需要是正确的 Java 代码，以分号结束。
</p>
<li>JSP 表达式
</li>
<p>表达式是以 <code>&lt;%=</code> 开始，以 <code>%&gt;</code> 结束的标签。它作为 Java 表达式的占位符，与变量声明不同，表达式不能以分号结束。在页面每次被访问时都要计算表达式，然后将其值嵌入到 HTML 的输出中。使用表达式可以向输出流中输出任何对象或任何基本类型。
</p>
</ol>

## 1.2 JSP 指令
指令向容器提供关于 JSP 页面的总体信息。在 JSP 页面中，指令是以 <code>&lt;%@</code>开头，以 <code>%&gt;</code> 结束的标签。指令有三种类型：page 指令、include 指令和 taglib 指令。语法格式如下：
<pre>
&lt;%--attribute-list 表示一个或多个针对指令的属性/值对，多个属性之间用空格隔开 --%&gt;
&lt;%@ page attribute-list %&gt;
&lt;%@ include attribute-list %&gt;
&lt;%@ taglib attribute-list %&gt;
</pre>

<ol>
<li>page 指令
</li>
<p>page 指令通知容器关于 JSP 页面的总体特性。例如：<code>&lt;%@ page contentType="text/html;charset=UTF-8"</code> 通知容器页面输出的内容类型和使用的字符集。<br/>
具体参照 [page 指令]
</p>
<li>include 指令
</li>
<p>include 指令实现把另一个文件（HTML、JSP等）的内容包含到当前页面中。例如：<code>&lt;%@ include file="copyright.html" %&gt;</code><br/>
具体参照 [include 指令]
</p>
<li>taglib 指令
</li>
<p>taglib 指令用来指定在 JSP 页面中使用标准标签或自定义标签的前缀与标签库的 URL。<br/>
<strong>注意：</strong><br/>
<ul>
<li>标签名、属性名及属性值对大小写敏感。
</li>
<li>属性值必须使用一对单引号或双引号括起来。
</li>
<li>在等号与值之间不能有空格。
</li>
</ul>
参照 [标签开发]
</p>
</ol>

## JSP 动作
动作是页面发给容器的命令，它指示容器在页面执行期间完成某种任务。语法一般为：
<pre>
&lt;%-- prefix 为前缀名，actionName 为动作名，attribute-list 表示针对该动作的一个或多个属性/值对 --%&gt;
&lt;prefix:actionName attribute-list /&gt;
</pre>

JSP 页面中可以使用三种动作：JSP 标准动作，标准标签库（JSTL）中的动作和用户自定义动作。例如：<code>&lt;include page="copyright.jsp" /&gt;</code>

下面是常用的 JSP 标准动作：
<ul>
<li>jsp:include，在当前页面中包含另一个页面的输出。
</li>
<li>jsp:forward，将请求转发到指定页面。
</li>
<li>jsp:useBean，查找或创建一个 JavaBeans 对象。
</li>
<li>jsp:setProperty，设置 JavaBeans 对象的属性值。
</li>
<li>jsp:getProperty，返回 JavaBeans 对象的属性值。
</li>
<li>jsp:plugin，在 JSP 页面中嵌入一个插件。
</li>
</ul>

具体参照 [JSP 动作]

## 1.4 表达式语言
表达式语言（EL，Expression Language）是 JSP 2.0 新增加的特性，它是一种可以在页面中使用简洁的数据访问语言。格式为<code>${expression}</code>。该结构可以出现在 JSP 页面的模板文本中，也可以出现在 JSP 标签的属性中。

具体参考 [表达式语言]

## 1.5 JSP 注释
JSP 注释是以 <code>&lt;%--</code> 开头，以 <code>--%></code> 结束的标签。注释不影响 JSP 页面的输出且 JSP 注释内不能再嵌套一个 JSP 注释。

还可以在小脚本或声明中使用一般的 Java 风格的注释，也可以在页面的 HTML 部分使用 HTML 风格的注释，如下：
<pre>
&lt;% //这里是 Java 注释 %&gt;
&lt;!--这里是 HTML 注释 --&gt;
</pre>
