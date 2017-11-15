# Servlet API
Servlet 规范提供了一个标准的，平台独立的框架以实现在 Servlet 和容器之间的通信。该框架是由一组 Java 接口和类组成的，它们称为 Servlet API。

Servlet 3.0 API 由下面 4 个包组成：
1. javax.servlet 包，定义了开发独立与协议的服务器小程序的接口和类。
2. javax.servlet.http 包，定义了开发采用 HTTP 通信的服务器小程序的接口和类。
3. javax.servlet.annotation 包，定义了 9 个注解类型和两个枚举类型。
4. javax.servlet.descriptor 包，定义了以编程方式访问 Web 应用程序配置信息的类型。

## javax.servlet 包
下表介绍 javax.servlet 包中的接口。<br/>

|接口名|说明|
|-|-|
|Filter|在请求和响应之间执行过滤任务的过滤器对象|
|FilterChain|Servlet 容器向开发人员提供的一个过滤器对象|
|FilterConfig|Servlet 容器使用的过滤器配置对象|
|RequestDispatcher|将请求转发到其他资源的对象|
|Servlet|所有 Servlet 的根接口|
|ServletConfig|Servlet 容器使用的 Servlet 配置对象，用来向 Servlet 转递信息|
|ServletContext|该接口定义了一些方法，Servlet 可以与 Servlet 容器通信|
|ServletRequest|提供客户请求的对象|
|ServletResponse|提供服务器响应的对象|
|ServletContextListener|用于接听 Web 应用程序的监听接口|
|ServletContextAttributeListener|用于监听 Web 应用程序属性的监听器接口|
|ServletRequestListener|用于监听请求对象的监听器接口|
|ServletRequestAttributeListener|用于监听请求对象属性的监听接口|
|SingleThreadModel|实现单线程的接口，已不推荐使用|

下表列出 javax.servlet 包中常用的类。
<br/>

|类名|说明|
|-|-|
|GenericServlet|定义了一般的、独立于协议的 Servlet|
|ServletContextAttributeEvent|Servlet 环境属性的事件类|
|ServletContextEvent|Servlet 环境的事件类|
|ServletInputStream|从客户请求读取二进制数据的类|
|ServletOutputStream|向客户端发送二进制数据的类|
|ServletRequestAttributeEvent|请求属性事件类|
|ServletRequestEvent|请求事件类|
|ServletRequestWrapper|请求对象包装类|
|ServletResponseWrapper|相应对象包装类|
|ServletException|当 Servlet 遇到一般错误时抛出异常|
|UnavailableException|Servlet 或过滤器在其永久或临时不可用时抛出异常|

简介 javax.servlet 包中几个重要的接口和类。

1. Servlet 接口

  Servlet 接口是 Servlet API 中的核心接口，每个 Servlet 必须直接或间接实现该接口。该接口定义了如下五个方法。
  >1. `public void init(ServletConfig config)` 该方法由容器调用，完成 Servlet 初始化并准备提供服务。容器转递给该方法一个 ServletConfig 类型的参数。
  >2. `public void service(ServletRequest req,ServletResponse res) throws ServletException,IOException` 对每个用户请求容器调用一次该方法，它允许 Servlet 为请求提供响应。
  >3. `public void destory()` 该方法由容器调用，指示 Servlet 清除本身、释放请求的资源并准备结束服务。
  >4. `public ServletConfig getServletConfig()` 返回关于 Servlet 的配置信息，如转递给 `init()` 的参数。
  >5. `public String getServletInfo()`  返回关于 Servlet 的信息，如作者、版本及版权信息。

2. ServletConfig 接口

  ServletConfig 接口为用户提供了有关 Servlet 的配置信息。Servlet 配置包括 Servlet 名称、Servlet 上下文对象、Servlet 初始化参数等。

3. GenericServlet 类

  GenericServlet 抽象类实现了 Servlet 接口和 ServletConfig 接口，提供了 Servlet 接口中除了 `service()` 外的所有方法的实现，同时增加了几个支持日志的方法。可以扩展该类并实现 `service()` 来创建任何类型的 Servlet。

4. ServletRequest 接口

  ServletRequest 接口是独立于任何协议的请求对象，定义了获取客户请求信息的方法，如：`getParameter()、getProtocal()、getRemoteHost()` 等。

5. ServletResponse 接口

  ServletResponse 接口是独立于任何协议的的响应对象，定义了向客户发送响应的方法，如：`setContentType()、sendRedirect()、getWritet()` 等。

## javax.servlet.http 包
该包提供创建使用 HTTP 的 Servlet 所需要的接口和类。该包工定义 8 个接口和 7 个类，其中某些接口和类扩展了 javax.servlet 包中对应的接口和类来实现对 HTTP 的支持。

javax.servlet.http 包中常用的接口。<br/>

|接口名|说明|
|-|-|
|HttpServletRequest|该接口提供了有关 HTTP 请求的信息|
|HttpServletResponse|该接口提供了有关 HTTP 响应的信息|
|HttpSession|实现会话管理的接口，也用来存储用户信息|
|HttpSessionActivationListener|HTTP 会话启动监听器接口|
|HttpSessionAttributeLister|HTTP 会话属性监听接口|
|HttpSessionBindingListener|HTTP 会话绑定监听器接口|
|HttpSessionListener|HTTP 会话监听器接口|
|HttpSessionContext|该接口不推荐使用|
|Part|客户上传到服务器的内容，可以是文件或表单数据|

javax.servlet.http 包中所有的类。<br/>

|类名|说明|
|-|-|
|HttpServlet|用于创建 HTTP Servlet 的抽象类|
|Cookie|创建 Cookie 对象的一个实现类|
|HttpServletRequestWrapper|HttpServletRequest 接口的实现类|
|HttpServletresponseWrapper|HttpServletResponse 接口的实现类|
|HttpSessionEvent|会话事件类|
|HttpSessionBindingEvent|会话绑定事件或会话属性事件类|
|HttpUtils|一个工具类，已不推荐使用|

简介该包中几个重要的接口和类：
1. HttpServlet 类

  HttpServlet 抽象类用来实现针对 HTTP 的 Servlet，它扩展了 GenericServlet 类。

  在 HttpServlet 类中增加了一个新的 `service()`，格式如下：`protected void service(HttpServletRequest,HttpServletResponse) throws ServletException,IOException`。该方法是 Servlet 向客户请求提供服务的一个方法，我们编写的 Servlet 可以覆盖该方法，此外，在 HttpServlet 中针对不同的 HTTP 请求方法定义了不同的处理方法，如处理 GET 请求的 doGet() 格式如下：`protected void doGet(HttpServletRequest,HttpServletResponse) throws ServletException,IOException`。通常，我们编写的 Servlet 覆盖 `doGet()` 或 `doPost()`。

2. HttpServletRequest 接口

  HttpServletRequest 接口扩展了 ServletRequest 接口并提供了针对 HTTP 请求操作方法，如定义了从请求对象中获取 HTTP 请求头、Cookie 等信息的方法。

3. HttpServletResponse 接口

  HttpServletResponse 接口扩展了 ServletResponse 接口并提供了针对 HTTP 的发送响应方法。它定义了为响应设置的如 HTTP 头，Cookie 信息的方法。
