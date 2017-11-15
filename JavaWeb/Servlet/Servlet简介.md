# Servlet 简介
Servlet 可翻译为服务器端小程序，他是使用 Servlet API 以及相关的类编写的 Java 程序，这种程序运行在 Web 容器中，主要用来扩展 Web 服务器的功能。

Servlet 作为 Web 应用程序的组件需要部署到容器中才能运行。

## Web 容器
Web 服务器使用一个单独的模块装载和运行 Servlet 与 JSP 页面，这个模块称为 Servlet 容器或 Web 容器。

![完整的 Web 组件示意图](http://oyoxq8ute.bkt.clouddn.com/%E5%AE%8C%E6%95%B4%E7%9A%84%20Web%20%E7%BB%84%E4%BB%B6%E7%A4%BA%E6%84%8F%E5%9B%BE.jpg "完整的 Web 组件示意图")

Tomcat 就是一个 Web 容器，他在整个 Web 应用系统中处于中间层的地位。如上图所示。

浏览器向 Web 服务器发送请求，若请求的目标是 HTML 文件，Web 服务器可以直接处理。若请求的是 Servlet 或 JSP 页面，Web 服务器将请求转发给 Web 容器，容器将查找并执行该 Servlet 或 JSP 页面。Servlet 和 JSP 页面都可以产生动态输出。

Tomcat 作为一个 Web 容器可以有三种运行方式：独立运行的，进程内运行的和进程外运行的。
