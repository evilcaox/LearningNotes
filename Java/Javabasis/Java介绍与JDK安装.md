#  Java入门
1. 安装 JDK
Java要实现“一处编写，处处运行”的目标，就必须提供相应的运行环境，即运行 Java 的平台。目
 Java 的平台主要有 3 个版本：
> * Java SE(曾称为 J2SE)称为 Java 标准版或 Java 标准平台。Java SE 提供了标准的 JDK
（Java Development Kit）。该平台可以开发 Java 桌面应用程序和低端的服务器应用程序。
 * Java EE（曾称为 J2EE）称为 Java 企业版或 Java 企业平台。能构建企业级服务应用，Java
 EE 平台包括 Java SE 平台，并增加了附加类库，以便支持目录管理、交易管理和企业级消息处理
 等功能。
 * Java ME（曾称为J2ME）称为 Java 微型版或 Java 小型平台。是一种很微小的运行环境，用于
 嵌入式的消费产品中。

2. 安装 Java SE 平台
>步骤：
 * 下载 JDK：登录 http://java.sun.com ,下载 JDK。
 * 配置环境变量：此处需要配置三个环境变量 JAVA_HOME、path 和 classpath。设置 JAVA_HO
 ME是为了方便引用，例如：JDK 安装在 D:\Java1.8\jdk1.8.0_60 目录里，则设置 JAVA_HOME
 为该路径，那么以后在使用这个路径的时候，只需要输入 %JAVA_HOME% 即可，避免每次使用输入
 很长的路径。classpath 是为了程序能找到相应的 .class 文件。设置 path 是为了能在任何目
 录中使用编译器和解释器。设置方法：在 win7、win8 系统中，鼠标右击“计算机-属性-高级系统
 设置-环境变量”。其中 path 是存在的，找到 path 变量并在后面加上 %JAVA_HOME%\bin;新建
 JAVA_HOME 变量并输入 JDK的安装目录：新建 classpath 变量并输入 .:%JAVA_HOME%\lib;

3. Java 程序的开发步骤
 * 编写源文件
         使用一个文本编辑器（如记事本），不可使用 Word 编辑器，因为文档不是纯文本，含有
         不可见字符。或者使用其他编辑器，如 Atom 等；或者使用 Eclipse 
         进行开发。
 * 编译 Java 源程序
         使用 Java 编译器（javac.exe)编译源文件，可得到字节码文件。
 * 运行 Java 程序
         使用 Java SE 平台中的 Java 解释器（ java.exe)来执行字节码文件。

4. 一个简单的 Java 应用程序

 打开记事本，输入下面代码。
         public class Hello{
           public static void main(String args[]){
             System.out.println("Hello word！");
           }
        }
 将该文件另存为，选择所有文件，命名为“Hello.java”,若还不是java文件，可用双引号将名字括起来。**注意：** 文件名与类名要一致，而且区分大小写。

 接着打开 MS—DOS 命令行窗口（按下windows+R输入cmd）。进入到前面保存 Hello.java 的文件目录下。例如若保存在 E 盘的 workspace 目录下，则先输入“E：”进入 E 盘，然后输入“cd workspace”进入 workspace 目录下。接着输入“javac Hello.java”，点击回车，若代码没有错误，则会在该目录（Hello.java所在目录）中生成“Hello.class”文件。最后在 DOS 命令窗口中输入“java Hello”(此处不需要加后缀)点击回车即可运行。
