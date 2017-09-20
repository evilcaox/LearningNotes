# 1 Java 网络编程
## 1.1 URL 类
URL 类的实例封装着一个统一资源定位符，使用 URL 类创建对象的应用程序称为客户端程序。一个 URL 对象封装着一个具体的资源的引用，表明客户要访问 URL 中的资源，客户利用 URL 对象可以获取 URL 中的资源。

一个 URL 对象通常包括三部分信息：协议、地址、资源。**协议** 必须是 URL 对象所在的 Java 虚拟机支持的协议，许多协议并不为用户所常用，而常用的 HTTP、FTP 和 File 协议都是虚拟机支持的协议；**地址** 必须是能连接的有效 IP 地址或域名；**资源** 可以是主机上的任何一个文件。

该类位于 `java.net` 包。

    public final class URL extends Object implements Serializable

### 1.1.1 URL 的构造方法
1. public URl(String spec) throws MalformedURLException

  参数：
  spec -要解析为 URL 的字符串。

2. public URL(URL context,String spec) throws MalformedURLException

  参数：
  context -解析规范上下文
  spec -要解析为 URL 的字符串
  通过在指定的上下文中解析给定的规范来创建一个 URL。

3. public URL(String protocol,String host,String file) throws MalformedURLException

  参数：
  protocol -要使用的协议的名称
  host -主机名
  file -主机上的文件

### 1.1.2 读取 URL 中的资源
使用 URL 类的 `public InputStream openStream() throws IOException` 方法可以返回一个输入流，该输入流指向 URL 对象所包含的资源。通过该输入流可以将服务器上的资源信息读入到客户端。

## 1.2 InetAddress 类
### 1.2.1 地址的表示
Internet 上的主机有域名和 IP 地址两种方式表示地址。域名易记，在连接网络时输入一个主机域名后，域名服务器（DNS）负责将域名转化为 IP 地址。这样才能和主机建立连接。
1. 域名

  例如：www.baidu.com
2. IP 地址

  例如：180.97.33.108 对应 www.baidu.com。windows 下可通过 nslookup + 域名查看。

### 1.2.2 获取地址
1. 获取 Internet 上主机的地址

  可以使用 InetAddress 类的静态方法 `static InetAddress getByName(String s)` 将一个域名或 IP 地址传递给该方法的参数 s，并返回一个 InetAddress 对象。该对象含有主机地址的域名和 IP 地址，该对象用如下格式表示它包含的信息：`www.baidu.com/180.97.33.108`。

  InetAddress 类还有两个实例方法：

          public String getHostName()//获取 InetAddress 对象所含的域名。
          public String getHostAddress()//获取 InetAddress 对象所含的 IP 地址

### 1.2.3 获取本地机的地址
使用 InetAddress 类的静态方法 `static InetAddress getLocalHost()` 获得一个 InetAddress 对象，该对象含有本地机的域名和 IP 地址。

## 1.3 套接字
### 1.3.1 套接字
网络通信使用 IP 地址标识 Internet 上的计算机，使用端口号标识服务器上的进程（程序）。若服务器上的一个程序不占用一个端口号，用户程序就无法找到它，也就无法和该程序交互信息。端口号被规定为一个 16 位的 0~65535 之间的整数，其中，0~1023 被预先定义的服务通信占用（如 HTTP 占用 80），除非我们需要访问这些特定服务；否则，就应该使用端口号为 1024~65535 的这些端口中的某一个进行通信，以免端口冲突。当两个程序需要通信时，它们可以通过使用 Socket 类建立套接字对象并连接在一起（端口号与 IP 地址的组合得出一个网络套接字）。


### 1.3.2 客户端套接字
客户端的程序使用 Socket 类建立负责连接到服务器的套接字对象。位于 `java.net` 包

    public class Socket extends Object implements Closeable

Socket 类构造方法：

    public Socket()//创建一个未连接的套接字，并使用系统默认类型的SocketImpl
    public Socket(InetAddress address,int port) throws IOException//address -ip地址，port 端口号。创建套接字并将其连接到指定 IP 地址的指定端口号
    public Socket(String host,int port) throws UnknownHostException IOException//host -服务器的 IP 地址，或 null 的环回地址，port -端口号。

Socket 类常用方法：

    pulic InputStream getInputStream() throws IOException//获得一个输入流，这个输入流的源和服务器的一个输出流的目的地刚好相同，因此客户端用输入流可以读取服务器写入到输出流中的数据
    public OutputStream getOutputStream() throws IOException//获得一个输出流，这个输出流的目的地和服务器端的一个输入流的源刚好相同，因此服务器用输入流可以读取客服端写入到输出流中的数据。
    public void connect(SocketAddress endpoint) throws IOException//将此套接字连接到服务器
    public void connect(SocketAddress endpoint,int timeout) throws IOException//将此套接字连接到具有指定超时值 timeout 的服务器。超时为零被介绍为无限超时。然后，连接将阻塞，直到建立或发生错误。

### 1.3.3 服务器端套接字
使用 ServerSocket 对象可以将服务器端的套接字和服务器端的一个套接字对象连接起来，从而实现连接的目的。位于 `java.net` 包。

    public class ServerSocket extends Object implements Closeable

这个类实现服务器套接字。服务器套接字等待通过网络进入请求。它根据请求执行一些操作，然后可能将结果返回请求者。服务器套接字的实际工作由 SocketImpl 类的实例执行。应用程序可以更改创建套接字实现的套接字工厂，以配置自己创建适合本地防火墙的套接字。

ServerSocket 构造方法：

1. public ServerSocket(int port) throws IOException

  参数：
  port -端口号，若设为 0 则自动分配
  创建绑定到指定端口的服务器套接字。当设置为 0 时端口号是自动分配的，通常从短暂的端口范围选择。

2. public ServerSocket(int port,int backlog) throws IOException

  参数：
  port -端口号，设置为 0 自动分配
  backlog -请求加入队列的最大长度
  创建服务器套接字并将其绑定到指定的本地端口号，并指定了积压。端口号 0 表示端口号自动分配，通常是从短暂端口范围悬着。输入连接指示（连接请求）的最大队列长度设置为 backlog 参数。若连接指示在队列已满时到达，则连接被拒绝。

ServerSocket 常用方法：

1. public Socket accept() throws IOException

  侦听要连接到此的客户端套接字并接受它。该方法阻塞直到建立连接。创建一个新的 Socket s,若有安全管理器，则使用 s.getInetAddress().getHostAddress() 和 s.getPort() 作为其参数来调用安全管理器的 checkAccept 方法，以确保允许操作。

2. public void bind(SocketAddress endpoint) throws IOException

  参数：
  endpoint -绑定到的 IP 地址和端口号
  将 ServerSocket 绑定到特定地址（IP 地址和端口号）。若地址为 null，则系统将接受临时端口和有效的本地地址来绑定套接字。

3. public void bind(SocketAddress endpoint,int backlog) throws IOException

  参数：
  endpoint -绑定到的 IP 地址和端口号
  backlog -请求进入连接队列的最大长度

4. public void close() throws IOException

  关闭此套接字。受阻于任何线程的 accept() 都将抛出一个异常。

5. public InetAddress getInetAddress()

  返回此服务器套接字的本地地址。

### 1.3.4 使用多线程技术
在使用套接字连接时读取数据，可能一端数据发送出来之前就已经开始试着读取了，这时，就会堵塞本线程，直到读取方法成功读取到信息，本线程才继续执行后续的操作。因此，服务器端收到一个客户的套接字后，就应该启动一个专门为该客户服务的线程。

可以使用 Socket 类不带参数的构造方法 Socket() 来创建一个套接字对象，该对象再调用 `public void connect(SocketAddress endpoint) throws IOException`,请求和参数 SocketAddress 指定地址的服务器端的套接字建立连接。为了使用 connect() 方法，可以使用 SocketAddress 的子类 InetSocketAddress 来创建一个对象，InetSocketAddress 的构造方法是 `public InetSocketAddress(InetAddress addr,int port)`。

## 1.4 UDP 数据报
基于 UDP 通信的基本模式是：
1. 将数据打包，称为数据包，然后将数据包发往目的地。
2. 接受别人发来的数据包，然后查看数据包中的内容。

### 1.4.1 发送数据包
1. 用 DatagramPacket 类将数据打包，即用 DatagramPacket 类创建一个对象，称为数据包。用 DatagramPacket 的以下两个构造方法创建待发送的数据包：

    DatagramPacket(byte data[],int length,InetAddress address,int port)//使用该构造方法创建的数据包对象具有下列两个性质：含有 data 数组指定的数据；该数据包将发送到的地址是 address,端口号在 port 的主机上。我们称 address 是它的目标地址，port 是这个数据包的目标端口。
    DatagramPacket(byte data[],int offset,int length,InetAddress address,int port)//使用该构造方法创建的数据包对象含有数组 data 中从 offset 开始后的 length 个字节，该数据包将发送到地址是 address，端口号在 port 的主机上。

2. 用DatagramSocket 类不带参数的构造方法 DatagramSocket() 创建一个对象，该对象负责发送数据包。

### 1.4.2 接收数据包
首先用 DatagramSocket 的另一个构造方法 DatagramSocket(int port) 创建一个对象，其中的参数必须和待接收的数据包的端口号相同。例如，如果发送方发送的数据包的端口是 3000，那么如下创建 DatagramSocket 对象：DatagramSocket datagramSocket=new DatagramSocket(3000);

然后对象 datagramSocket 使用 receive(DatagramSocket pack) 方法接收数据包。该方法有一个数据包参数 pack,方法 receive() 把收到的数据包传递给该参数。因此我们必须预备一个数据包以便收取数据包。这时需要使用 DatagramPacket 类的另外一个构造方法 DatagramPacket(byte data[],int length)创建一个数据包，用于接收数据包。
