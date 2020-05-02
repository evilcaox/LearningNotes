# ServletConfig 接口
在 Servlet 初始化时，容器将调用 init(ServletConfig config),并为其传递一个 ServletConfig 对象，该对象称为 Servlet 配置对象，使用该对象可以获得 Servlet 初始化参数、Servlet 名称、ServletContext 对象等。

要得到 ServletConfig 接口对象有两种方法：
<ol>
<li>
覆盖 Servlet 的 init(ServletConfig config)，然后把容器创建的 ServletConfig 对象保存到一个成员变量中。如下所示：
<pre>
 ServletConfig config=null;
 public void init(ServletConfig config){
   super.init(config);//必须调用父类的 init()
   this.config=config;
 }
</pre>
</li>
<li>
在 Servlet 中直接使用 <code>getServletConfig()</code> 获得 ServletConfig 对象，如下所示：
<pre>
ServletConfig config=getServletConfig();
</pre>
</li>
</ol>

ServletConfig 接口定义了下面 4 个方法：
<ol>
<li>public String getInitParameter(String name)
<p>
返回指定名称的初始化参数值。若 该参数不存在，则返回 null。初始化参数是在 Servlet 初始化化时容器从 DD 文件中取出，然后把它包装到 ServletConfig 对象中。
</p>
</li>
<li>
public Enumeration getInitParameterNames()
<p>
返回一个包含所有初始化参数名的 Enumeration 对象。若 Servlet 没有初始化参数，则返回一个空的 Enumeration 对象。
</p>
</li>
<li>
public String getServletName()
<p>
返回 DD 文件中 <servlet-namne> 元素指定的 Servlet 名称。
</p>
</li>
<li>
public ServletContext getServletContext()
<p>
返回该 Servlet 所在的上下文对象
</p>
</li>
</ol>

由于 HttpServlet 类实现了 ServletConfig 接口，因此可以在 HttpServlet 中直接调用上述方法获得初始化参数和其他信息。
