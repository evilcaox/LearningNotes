# Tomcat 下载与安装
Tomcat 是 Apache 软件基金会得开源产品，是 Servlet 和 JSP（Java Server Pages）技术的实现。

我们可以通过在 http://tomcat.apache.org/ 网站下载各个版本的 Tomcat 服务器。

此处我们安装的环境为 Windows。要安装 Tomact 必须先安装 Java 运行环境（Java Runtime Environment,JRE）。

我们下载 Tomcat 服务器的免安装版，通过如下步骤安装：
* 下载得到 Tomcat 服务器的免安装压缩包。并解压。
* 配置环境变量，与 Java 安装时配置 JDK 时相似，我们新建一个环境变量并将 Tomcat 所在路径添加即可完成。

我们可以通过 Tomcat 包下的 bin 文件夹下的 startup.bat 来启动服务器，通过shutdown.bat 来关闭服务器。若点击出现闪退按照下面方法配置:
* 打开并编辑 startup.bat,在最前面两行： `SET JAVA_HOME=[Java JDK 的位置]`与`SET TOMCAT_HOME=[TOMCAT所在的位置]`
* 在 shutdown.bat 同样加入上面两行内容。

启动 Tomcat 服务器，打开浏览器，输入 http://localhost:8080./ 可访问即安装完成。

# Tomcat 安装目录
|目录|说明|
|-|-|
|/bin|存放启动和关闭 Tomcat 的脚本文件|
|/conf|存放 Tomcat 服务器的各种配置文件，其中包括 servler.xml、tomcat-user.xml和web.xml 等文件|
|/lib|存放 Tomcat 服务器及所有 Web 应用程序都可以访问的库文件|
|/logs|存放日志文件|
|/temp|存放 Tomcat 运行时产生的临时文件|
|/webapps|存放所有 Web 应用程序的根目录|
|/work|存放 JSP 页面生成的 Servlet 源文件和字节码文件|

因为 /webapps 目录下放着 Tomcat 服务器中所有的 Web 应用程序，所有算是比较重要的一个文件。下面对该目录中的文件逐一说明：

# 配置 Tomcat 的服务端口
Tomcat 默认端口为 8080，在访问服务器资源时需要在 URL 中给出端口号。为了方便我们可以将端口号修改为简单的，比如 80。

修改步骤：
* 打开 Tomcat 服务器所在位置下的 conf 文件夹。
* 找到 server.xml。
* 修改 Connector 元素的 port 属性。如下 `<Connector port="8080" protocol="HTTP/1.1" connectionTimeout="20000" redirectPort="8443" />`。将 `port="8080"` 中的 8080 修改为想修改的端口号就可以了。
