# ServletContext 接口
Web 容器在启动时会加载每个 Web 应用程序，并为每个 Web 应用程序创建一个唯一的 ServletContext 对象，该对象一般称为 Servlet 上下文对象。
Servlet 可以使用 javax.servlet.ServletContext 对象来获得 Web 应用程序的初始化参数或 Servlet 容器的版本等信息，也可以被 Servlet 用来与其它的 Servlet 共享数据。

## 得到 ServletContext 引用
有两种方法可以得到 ServletContext 引用：
<ol>
<li>直接调用 <code>getServletContext()</code>
<pre>
例如：
ServletContext context=getServletContext();
</pre>
</li>
<li>可以先得到 <em>ServletConfig</em> 引用，再调用它的 <code>getServletContext()</code>。
<pre>
ServletContext context=getServletConfig().getServletContext();
</pre>
</li>
</ol>

## 获得应用程序的初始化参数
ServletContext 对象是在 Web 应用程序装载时初始化的。正像 Servlet 具有初始化参数一样，ServletContext 也有初始化参数。Servlet 上下文初始化参数指定应用程序范围内的信息，如开发人员的联系信息以及数据库连接信息等。

可以使用下面两个方法检索 Servlet 上下文初始化参数：
<ol>
<li><code>public String getInitParameter(String name)</code>
<p>
返回指定参数名的字符串参数值，如果参数不存在则返回 null。
</p>
</li>
<li>
<code>public Enumeration getInitParameterNames()</code>
<p>
返回一个包含所有初始化参数名的 Enumeration 对象。
</p>
</li>
</ol>

应用程序的初始化参数只能在 web.xml 文件中使用 <code>&lt;context-param&gt;</code> 元素定义，不能使用注解定义。例如：
<pre>
&lt;context-param&gt;
  &lt;param-name&gt;adminEmail&lt;/param-name&gt;
  &lt;param-value&gt;webmaster@gmail.com&lt;/param-value&gt;
&lt;/context-param&gt;
取出值代码：
ServletContext context=getServletContext();
String email=context.getInitParameter("adminEmail");
</pre>
<strong>注意：</strong><code>&lt;context-param&gt;</code> 元素是针对整个应用的，所以并不嵌套在某个 `servlet` 元素中，该元素是 `<web-app>` 元素的直接子元素。

## 通过 ServletContext 对象获取资源
<ol>
<li><code>public URL getResource(String path)</code>
<p>
返回由给定路径指定的资源的 URL 对象。这里，路径必须以 “/” 开头，他相对于该 Web 应用程序的文档根目录。
</p>
</li>
<li><code>public InputStream getResourceAsStream(String path)</code>
<p>
如果想从资源上获得一个 InputStream 对象，这是一个简捷的方法，它等价于 <code>getResource(path).openStream()</code>。
</p>
</li>
<li><code>public String getRealPath(String path)</code>
<p>
返回给定的相对路径的绝对路径。
</p>
</li>
</ol>

## 登录日志
使用 ServletContext 接口的 `log()` 可以将指定的消息写到服务器的日志文件中，该方法有下面两种格式：
<ol>
<li><code>public void log(String msg)</code>
<p>
参数 msg 为写到日志文件中的消息。默认情况下把日志信息写到 <code>tomcat安装路径\logs\localhost.日期.log</code> 文件中，文件名中的日期为写入日志的日期。
</p>
</li>
<li><code>public void log(String msg,Throwable throwable)</code>
<p>
将 msg 指定的消息和异常的栈跟踪信息写入日志中。
</p>
</li>
</ol>

## 使用 RequestDispatcher 实现请求转发
使用 ServletContext 接口的下列两个方法也可以获得 RequestDispatcher 对象，实现请求转发。
<ol>
<li><code>RequestDispatcher getRequestDispatcher(String path)</code>
<p>
参数 path 表示资源路径，它必须以 “/” 开头，表示相对于 Web 应用的文档根目录。如果不能返回一个 RequestDispatcher 对象，该方法将返回 null;
</p>
</li>
<li><code>RequestDispatcher getNamedDispatcher(String name)</code>
<p>
参数 name 为一个命名的 Servlet 对象。Servlet 和 JSP 页面都可以通过 Web 应用程序的 DD 文件指定名称。
</p>
</li>
</ol>

ServletContext 和 ServletRequest 的 `getRequestDispatcher()` 的区别是：对 ServletContext 的 `getRequestDispatcher()` 只能传递以 "/" 开头的路径，而对 ServletRequest 的 `getRequestDispatcher()`,可以传递一个相对路径。

## 使用 ServletContext 对象存储数据
除了使用请求对象存储数据外，还可以使用 ServletContext 对象存储数据。该对象也是一个作用域对象，它的作用域是整个程序。在 ServletContext 接口中也定义了 4 个处理属性的方法，如下：
<ol>
<li><code>public void setAttribute(String name,Object object)</code>
<p>
将给定名称的属性值对象绑定到上下文对象上。
</p>
</li>
<li><code>public Enumeration getAttribute(String name)</code>
<p>
返回绑定到上下文对象上的给定名称的属性值，若没有该属性，则返回 null。
</p>
</li>
<li><code>public Enumeration getAttributeNames</code>
<p>
返回绑定到上下文对象上的所有属性名的 Enumeration 对象。
</p>
</li>
<li><code>public void removeAttribute(String name)</code>
<p>
从上下文对象中删除指定名称的属性。
</p>
</li>
</ol>

尽管可以使用这些容器的任何一个共享数据，但在这些容器中的数据具有不同的作用域。简单地说，使用 HttpServletRequest 共享的对象仅在请求的生存期中可被访问，使用 HttpSession 共享的对象仅在会话的生存期中可被访问，而使用 ServletContext 共享的对象可在 Web 应用想的生存期中被访问。

## 检索 Servlet 容器的信息
检索容器有关信息的方法如下：
<ol>
<li><code>getServerInfo()</code>
<p>
返回 Servlet 所运行的容器的名称和版本。
</p>
</li>
<li><code>getMajorVersion()</code> 与 <code>getMinorVersion()</code>
<p>
可以返回容器所支持的 Servlet API 的主版本号和次版本号。
</p>
</li>
<li><code>getServletContextName()</code>
<p>
返回与该 ServletContext 对应的 Web 应用程序名称，它是在 web.xml 中使用 <code>&lt;display-name&gt;</code> 元素定义的名称。
</p>
</li>
</ol>
