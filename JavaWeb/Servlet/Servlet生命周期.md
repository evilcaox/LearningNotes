# Servlet 生命周期
Servlet 作为一种容器中运行的组件，有一个从创建到销毁的过程，这个过程被称为 Servlet 生命周期。

Servlet 生命周期包括以下几个阶段：
1. 加载和实例化 Servlet 类。
2. 调用 `init()` 初始化 Servlet 实例。
3. 调用 `service()` 提供服务。
4. 调用 `destroy()` 销毁状态。

## 加载和实例化 Servlet
对一个 Servlet，可能在 Web 容器启动时或第一次被访问时加载到容器中，对每个 Servlet，容器使用 `Class.forName();` 对其加载并实例化。因此，要求 Servlet 类有一个不带参数的 public 构造方法。通常，不在 Servlet 类中定义任何构造方法，而让 Java 编译器添加默认构造方法。

容器创建了 Servlet 实例后就进入生命周期阶段，Servlet 生命周期方法包括 `init()`、`service()` 和 `destroy()`。

## 初始化 Servlet
容器创建 Servlet 实例后，将调用 `init(ServletConfig config)` 初始化 Servlet。该方法的参数 ServletConfig 对象包含在 Web 应用程序的初始化参数。调用 `init(ServletConfig config)` 后，容器将调用无参数的 `init()`，之后 Servlet 就完成初始化。在 Servlet 生命周期中 `init()` 仅被调用一次。

有时，不在容器启动时对 Servlet 初始化，而是当容器接收到对该 Servlet 第一次请求时才对它初始化，这称为延迟加载。这种初始化的优点是可以大大提高容器的启动时间。缺点是如果在 Servlet 初始化要完成很多任务时，则发送第一个请求的客户等待时间会很长。在很多情况下，这是不可接受的。为此，可以使用 `@WebServlet` 注解的 loadOnStartup 元素或 web.xml 文件的 `<load-on-startup>` 元素指定当容器启动时加载并初始化 Servlet。在 Servlet 被请求之前被加载和初始化的过程称为预加载或初始化。

## 为客户提供服务
在 Servlet 实例正常初始化后。用户就可以通过单击超链接或提交表单容器请求访问 Servlet。当容器接收到对 Servlet 的请求时，容器根据请求中的 URL 找到正确的 Servlet，首先创建两个对象，一个是 HttpServletRequest 请求对象，一个是 HttpServletResponse 响应对象。然后创建一个新的线程，在该线程中调用 `service()`，同时将请求对象和响应对象作为参数传递给该方法。显然，有多少个请求，容器将创建多少个线程。接下来 `servlet()` 将检查 HTTP 请求的类型（GET，POST 等）来决定调用 Servlet 的 `doGet()` 或 `doPost()`。

Servlet 使用响应对象（response）获得输出流对象，调用有关方法将响应发送给客户浏览器。之后，线程将被销毁或者返回到容器管理的线程池。请求和响应对象已经离开其作用域，也将被销毁。最后客户得到响应。

##  Servlet 的销毁和卸载
当容器简单不再需要 Servlet 实例时，它将在 Servlet 实例上调用 `destroy()`，Servlet 在该方法中释放资源，如它在 `init()` 中获得的数据库连接。一旦该方法被调用，Servlet 实例不能再提供服务。Servlet 实例从该状态仅能进入卸载状态。在调用 `destroy()` 之前，容器会等待其他执行 Servlet 的 `service()` 的线程结束。

一旦 Servlet 实例被销毁，他将作为垃圾被回收。如果 Web 容器关闭，Servlet 也将被销毁和卸载。
