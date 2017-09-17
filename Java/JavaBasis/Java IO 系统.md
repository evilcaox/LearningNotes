# 1 File 类
当我们需要获取磁盘上文件的有关信息或在磁盘上创建新的文件等，就需要使用 File 类。File 类主要用来获取文件本身的一些信息。例如：文件所在的目录，文件长度，文件的读取权限等，不涉及对文件的读写操作。

该类在 `java.io.File`。

    public class File extends Object implements Serializable,Comparable<File>

## 1.1 构造方法
1. public File(String pathname)

  参数：
  pathname -路径名字符串
  异常：
  当 pathname 为 null 时出现 NullPointerException 异常。
  通过将给定的路径名字符串转换为抽象路径名来创建新的 File 实例。如果给定的字符串是空字符串，则结果为空的抽象路径名。使用该方法进行创建文件时，默认与当前应用程序在同一个目录中。

2. public File(String parent,String child)

  参数：
  parent -父路径名字符串（文件路径）
  child -子路径名字符串（文件名字)
  异常：
  当 child 为 null 时出现 NullPointerException。
  从父路径名字符串和子路径名字符串创建新的 File 实例。若 parent 是 null 则创建新的 File 实例，就像在给定的 chile 路径名字字符串上调用单参数 File 构造函数一样。否则，将使用 parent 路径名字符串来表示目录，并将 chile 路径名字符串用于表示目录或文件。如果 child 路径名字符串是绝对的，那么它将以系统相关的方式转换为相对路径名。如果 parent 是空字符串则通过将 child 转换为抽象路径名并根据系统相关的默认目录解析结果来创建新的 File 实例。否则，每个路径名字符串将转换为抽象路径名，并且子抽象路径名将针对父亲对象进行解析。

3. public File(File parent,String child)

  参数：
  parent -父抽象路径名（目录）
  child -子路径名字符串（文件名字）
  异常：
  当 child 为 null 时出现 NullPointerException。

## 1.2 文件创建与删除
当使用 File 类的构造方法生成一个对象后，例如：

    File file=new File("E://workspace","Java.txt");
若在 E://workspace 目录中没有名字为 Java.txt 文件，文件对象 file 调用方法：

    public boolean createNewFile() throws IOException;
可以在 E://workspace 目录中创建 Java.txt 文件。当想删除该文件时，调用方法：

    public boolean delete();//删除成功返回 true,失败返回 false。
可以删除当前文件。

## 1.3 获取文件属性
可以使用 File 类的下列方法来获取文件本身的一些信息：

    public String getName()//获取文件名
    public boolean canRead()//判断文件是否可读
    public boolean canWrite()//判断文件是否可写
    public boolean exists()//判断文件是否存在
    public long length()//获取文件的长度
    public String getAbsolutepath()//获取文件的绝对路径
    public String getParent()//获取文件的父目录
    public boolean isFile()//判断一个文件是否为一个普通文件，而不是目录
    public boolean isDirectory()//判断文件是否是一个目录
    public boolean isHidden()//判断文件是否是隐藏文件
    public long lastModified()//获取文件最后修改的时间（时间是从 1970 年 00:00:00 至文件最后修改时刻的毫秒数）

## 1.4 目录
1. 创建目录

  File 对象调用方法 `public boolean mkdir()` 创建一个目录如果创建成功返回 true。否则返回 false（目录存在同样返回 false）。

2. 列出目录中的文件

  若 File 对象是一个目录，那么该对象可以调用下列方法列出该目录下的文件和目录。

        public String[] list()//用字符串形式返回目录下的全部文件
        public File[] listFiles()//用 File 对象形式返回目录下的全部文件

  当我们想要列出目录下指定类型的文件，例如：“.java”、“.txt” 等扩展名的文件，可以使用以下两个方法：

        public String[] list(FilenameFilter obj)//用字符串形式返回目录下指定类型的所有文件
        public File[] listFiles(FilenameFilter obj)//用 File 对象返回目录下指定类型的所有文件

  上述两个方法的参数 FilenameFilter 是一个接口，该接口有一个方法：

        public boolean accept(File dir,String name);

  使用 list() 方法时，需要该方法传递一个实现 FileInputStream 接口的对象，执行 list() 方法时，参数 obj 不断回调接口方法 accept(File dir,String name),该方法中的参数 dir 为调用 list 的当前目录，参数 name 为实例化目录中的一个文件名，若 name 文件名满足条件，则返回 true,list() 就将该文件放入目标数组中，最后将该数组返回。

  例如：

    import java.io.File;
    import java.io.FilenameFilter;

    public class Example {

    public static void main(String[] args) {
      File file=new File("E://java");
      boolean b=file.mkdir();
      if(b==true){
        System.out.print("创建成功！");
      }else{
        System.out.println("创建失败！");
      }
      String a[]=file.list();
      for(String t:a){
        System.out.println(t);
      }
      File f[]=file.listFiles();
      for(File list:f){
        System.out.println(list);
      }
      Filename fileNmae=new Filename();
      fileNmae.setExtendName("java");//设置文件后缀为java
      String b1[]=file.list(fileNmae);
      for(String t:b1){
        System.out.println(t);
      }
    }

    }
    class Filename implements FilenameFilter{
      private String extendName;//文件后缀
      //设置返回的文件类型
      public void setExtendName(String s){
        extendName="."+s;
      }
      public boolean accept(File dir, String name) {
        return name.endsWith(extendName);
      }

    }

## 1.5 运行可执行文件
当要执行一个本地上的可执行文件时，可以使用 `java.lang` 包中的 Runtime 类，首先声明一个对象：

    Runtime runTime;

然后使用该类的静态方法 getRuntime() 得到一个 Runtime 对象。

    rumTime=Runtime.getRuntime();

最后使用对象 runTime 调用 exec(String command) 方法打开本地的可执行文件，参数 command 表示可执行文件的绝对路径。

# 2 字节流和字符流
Java 把 InputStream 抽象类的子类创建的流对象称为字节输入流，OutputStream 抽象类的子类创建的流对象称为字节输出流；Java 把 Reader 抽象类的子类创建的流对象称为字符输入流，Writer 抽象类的子类创建的流对象称为字符输出流。
## 2.1 InputStream 和 OutputStream
### 2.1.1 InputStream
    public abstract class InputStream extends Object implements Closeable{}

接口 `Closeable` 内有一个 `void close()` 方法，该方法关闭此流并释放与它相关联的任何系
统资源。

InputStream 抽象类是所有表示字节输入流的父类，其中一些直接子类有 `AudioInputStream,By
teArrayInputStream,FileInputStream,FilterInputStream`

InputStream 的主要方法摘要:

1. 构造方法

       public InputStream()

2. read() 方法

       public abstract int read() throws IOException

 从输入流读取下一个数据字节。字节的范围在 0~255。若没有字节可读，则返回 -1。

3. read(byte[] b) 方法

        public int read(byte[] b) throws IOException
        参数：
        b 缓冲区读取数据

  从输入流中读取一定数量的字节并保存在字节数组 b 中，实际读取的数作为该方法的返回值。若
  b的长度为 0，那么没有字节可读返回 0。否则，若读到至少一个字节。在文件末尾不再有字节可
  读时，返回 -1。第一个字节存在 b[0],接下来存在 b[1]……。读取的字节数，最多等于 b 的长度。

4. read(byte[] b,int off,int len) 方法

        public int read(byte[] b,int off,int len) throws IOException
        参数：
        b 缓冲区中读取数据
        off 偏移量，表示从字节数组中的那一个位置开始存入数据
        len 可以读取的最大字节数

  与其他 read 方法相似，返回读取的实际字节数。若 len 为0，则返回 0，否则只要读到至少一
  个字节，在文件尾没有数据可读，则返回 -1。读到的第一个字节放在 b[off],下一个放在 b[off+1]。

5. close() 方法

        public void close() throws IOException

  关闭此输入流并释放与流相关联的任何系统资源。

#### 2.1.1.1 FileInputStream
    public class FileInputStream extends InputStream

FileInputStream 是 InputStream 的一个直接子类，可以从一个文件系统中的文件获得输入的字
节。FileInputStream 是读取原始字节的字节流。若想读字符流，则使用 FileReader。

FileInputStream 中的主要方法摘要：
1. 构造方法
  * FileInputStream(File file)

         public FileInputStream(File file) throws FileNotFoundException
         参数：
         file 文件路径，打开文件并阅读

  * FileInputStream(FileDescriptor fdObj)

         public FileInputStream(FileDescriptor fdObj)
         参数：
         fdObj 文件描述符被打开阅读

  * FileInputStream(String name)

         public FileInputStream(String name) throws FileNotFoundException
         参数：
         name 系统相关的文件名称

2. read 方法
  继承 InputStream 的 read 方法并重写。基本与 InputStream 相同。

3. close 方法
        public void close() throws IOException

  关闭此文件输入流并释放与流相关的任何系统资源。

例如：

    import java.io.*;
    class TestByte{
      public static void main(String[] args) {
      FileInputStream file=null;
      try{
        file=new FileInputStream("E:/workspace/java/byte.txt");
        byte[] b=new byte[100];
        file.read(b,0,20);
        for(int i=0;i<b.length;i++){
          System.out.println(b[i]);
        }
      }catch(Exception e){
        System.out.println(e);
       }finally{
         try{
           file.close();
         }catch(Exception e){
           System.out.println(e);
         }
       }

      }
    }
    执行结果:
    由 E:/workspace/java/byte.txt 中的内容决定，输出为 ASCII 码。例如该 Txt文件里只
    有一个 a ,则输出为 97 0 0 ……  后面的  0 在不同系统中有不同表示。表示的是空子符。因
    为只读到一个 a，所以其他位置为空子符。

### 2.1.2 OutputStream
    public abstract class OutputStream extends Object implements Closeable,Flushable

该抽象类是所有类的字节输出流的父类，输出流接受输出字节，并将他们发送到一些接收器。

OutputStream 常用方法摘要；
1.  构造方法
        public OutputStream()

2. write(byte[] b) 方法
        public void write(byte[] b) throws IOException
        参数：
        b 需要写入的字节数组


3. write(byte[] b,int off,int len)
        public void write(byte[] b,int off,int len) throws IOException
        参数：
        b 字节数组
        off 偏移量，表示从数组的那一位开始写
        len 字节数，表示写入多少位

#### 2.1.2.1 FileOutputStream
    public class FileOutputStream extends OutputStream

文件输出流是一个 File 或一个 FileDescriptor 数据写入输出流。书写字节流，若使用字符流，
考虑使用 FileWriter。

FileOutputStream 常用方法摘要：
1. 构造方法
        public FileOutputStream(File file)//创建一个文件输出流写入指定的 File 对象表示的文件。
        public FileOutputStream(File file,boolean append)//file:要打开写入的文件，append 若为 true，字节写在文末而不是开头
        public FileOutputStream(FileDescriptor fdObj)//创建一个文件输出流，写入指定的文件描述符，它表示在文件系统中的实际文件的现有连接
        public FileOutputStream(String name)//创建一个文件输出流，用指定的名称写入文件,name 为系统依赖的文件名
        public FileOutputStream(String name,boolean append)//name 为系统相关文件名称，append 若为 true,字节被写入到文件末尾而不是开头。

2. Write 方法
  从 OutputStream 继承重写，作用大致相同。

3. close 方法
        public void close() throws IOException
  关闭此文件并释放与流相关联的任何系统资源。


例如(我们更改 FileInputStream 中的例子)：

    import java.io.*;
    class TestByte{
      public static void main(String[] args) {
        FileInputStream file=null;
        FileOutputStream file2=null;
        try{
          file=new FileInputStream("E:/workspace/java/byte.txt");
          byte[] b=new byte[100];
          file.read(b,0,20);
          for(int i=0;i<b.length;i++){
            System.out.println(b[i]);
          }
          file2=new FileOutputStream("E:/workspace/java/bytein.txt");
          file2.write(b,0,20);
        }catch(Exception e){
          System.out.println(e);
         }finally{
            try{
              file.close();
              file2.close();
            }catch(Exception e){
              System.out.println(e);
             }
           }

      }
    }
    执行结果：
    除了与 FileInputStream 中例子相同与外，还在 E:/workspace/java 目录下新建了一个bytein.txt
    文件并将 byte.txt 中的内容写入。

## 2.2 Reader 和 Writer 类
Reader 类提供的 read() 方法以字符为单位顺序地读取源中的数据，只要不关闭流，每次调用 read() 方法就顺序地读取源中的其余内容，直至源末尾或输入流被关闭。Reader 类常用方法如下：

    int read()//输入流调用该方法从源中读取一个字符，该字符返回一个整数（0~65535 之间的一个整数，Unicode 字符值），如果未读出字符，则返回 -1；
    int read(char b[])//输入流调用该方法从源中读取 b.length 个字符到字符数组 b 中，返回实际读取字符数目。若到达文件的末尾，则返回 -1；
    read(char[] cbuf,int offset,int length)//从 cbuf 数组的 offset 处开始存储 length 个字符。
    void close()//输入流调用该方法关闭输入流
Writer 流以字符为单位顺序地写文件，只要不关闭流，每次调用 write() 方法就顺序地向目的地写入内容，直到流被关闭。Writer 类有如下常用的方法：

     void write(int n)//向输出流写入一个字符
     void write(byte b[])//向输出流写入一个字符数组
     void write(byte b[],int off,int length)//从给定字符数组中的 off 处开始向输出流写入 length 个字符
     void close()//关闭输出流。
### 2.2.1 FileReader
    public class FileReader extends InputStreamReader
用于读取字符文件的方便类。该类的构造方法假定默认字符编码和默认字节缓冲区大小是适当的。

FileReader 常用方法摘要：
1. 构造方法
        public FileReader(File file)//读取 file 指定路径下的文件内容
        public FileReader(FileDescriptor fd)//fd 要读取的 FileDescriptor
        public FileReader(String fileName)//fileName 文件名读取

2. read() 方法
        public int read() throws IOException
  读取单个字符。

3. read(char[] cbuf,int offset,int length) 方法
        public int read(char[] cbuf,int offset,int length) throws IOException
        参数：
        cubt 目的缓冲区
        offset 偏移量，从 char 数组下标为 offset 处开始存储
        length 读取的字符长度

与 FileInputStream 相比较，FileInputStream 从文件中读入的数据存储在 byte 数组中，而
FileReader 从文件中读入的数据存储在 char 数组中。

例如：

    import java.io.*;
    class TestChar{
      public static void main(String[] args) {
        FileReader file=null;
        try{
          file=new FileReader("E:/workspace/java/byte.txt");
          char[] c=new char[100];
          file.read(c,0,100);
          for(int i=0;i<c.length;i++){
            System.out.println(c[i]);
          }
        }catch(Exception e){
          System.out.println(e);
        }finally{
          try{
            file.close();
          }catch(Exception e){
            System.out.println(e);
          }
        }
      }
    }
    执行结果：
    打印 E:/workspace/java/byte.txt 中的内容。

### 2.2.2 FileWriter
    public class FileWriter extends OutputStreamWriter
用于写入字符文件的方便类。该类的构造方法假定默认字符编码和默认字节缓冲区大小是可以接受的。
FileWriter 是书写字符流。

FileWriter 常用方法摘要：
1. 构造函数
        public FileWriter(File file)
        public FileWriter(File file,boolean append)
        public FileWriter(FileDescriptor fd)
        public FileWriter(String fileName)
        public FileWriter(String filename,boolea append)

2. write(int c) 方法
        public void write(int c) throws IOException
        参数：
        c int指定字符被写入

3. write(char[] cbuf,int off,int len) 方法
        public void write(char[] cbuf,int off,int len) throws IOException
        参数：
        cbuf 存放写入的字符的字符数组，将该数组中德内容写入指定位置
        off 偏移量
        len 写入多少字符

4. write(String str,int off,int len) 方法
        public void write(String str,int off,int len) throws IOException
        参数：
        str 一个字符串
        off 偏移量
        len 写入多少字符,len+off 若大于 str 长度会报异常。

例如(修改 FileReader 例子)：

    import java.io.*;
    class TestChar{
      public static void main(String[] args) {
        FileReader file=null;
        FileWriter file2=null;
        try{
          file=new FileReader("E:/workspace/java/byte.txt");
          char[] c=new char[20];
          file.read(c,0,20);
          for(int i=0;i<c.length;i++){
            System.out.println(c[i]);
          }
          file2=new FileWriter("E:/workspace/java/bytein.txt");
          file2.write("hello word",0,10);//将str 写入指定文件
        }catch(Exception e){
          System.out.println(e);
        }finally{
          try{
            file.close();
            file2.close();
          }catch(Exception e){
            System.out.println(e);
          }
        }
      }
    }
    执行结果：
    在 E:/workspace/java/bytein.txt 中写入 hello word

# 3 缓冲流
BufferReader 和 BufferWriter 类创建的对象称为缓冲输入/输出流，二者增强了读写文件的能力，可以一次读取一行。但是他们的源和目的地必须是字符输入/输出流。
## 3.1 BufferedReader
    public class BufferedReader extends Reader
从一个字符输入流中读取文本，缓冲字符，以便提供字符、数组和行的有效读取。

BufferedReader 常用方法摘要：
1. 构造方法
        public BufferedReader(Reader in)//创建一个使用默认大小输入缓冲区的缓冲字符输入流
        public BufferedReader(Reader in,int sz)//创建一个使用指定大小输入缓冲区的缓冲字符输入流，大小有 sz 指定。

2. readLine() 方法
        public String readLine() throws IOException
  读一行文本。判断依据是任何一个终止标识，比如回车。

3. read() 方法
        public int read() throws IOException
  读取单个字符。

4. read(char[] cbuf,int off,int len) 方法
        public int read(char[] cbuf,int off,int len) throws IOException
  读取一定长度的字符。

例如：

先在 txt 文本中写入一下内容。

张三 60

李四 50

王二 80

    import java.io.*;
    class TestBuffer{
      public static void main(String[] args) {
        BufferedReader bf=null;
        try{
          bf=new BufferedReader(new FileReader("E:/workspace/java/byte.txt"));
          while(true){
          String s=bf.readLine();
          if(s==null){
            break;
          }
          System.out.println(s);
          }
        }catch (Exception e) {
          System.out.println(e);
        }finally{
          try{
            bf.close();
          }catch (Exception e) {
            System.out.println(e);
          }
        }
      }
    }
    执行结果：
    张三 60
    李四 50
    王二 80

## 3.2 BufferedWriter
    public class BufferedWriter extends Writer
将文本写入到字符输出流中，缓冲字符，以便对单个字符、数组和字符串的有效写入/

BufferedWriter 常用方法摘要：
1. 构造方法
        public BufferedWriter(Writer out)
        public BufferedWriterW(Writer out,int sz)

2. write(int c) 方法
        public void write(int c) throws IOException

3. write(char[] cbuf,int off,int len) 方法
        public void write(char[] cbuf,int off,int len) throws IOException

4. write(String s,int off,int len) 方法
        public void write(String s,int off,int len) throws IOException

5. newLine()
        public void newLine() throws IOException
  写行分隔符，分隔符字符串是由系统性 line.separator 定义，而不一定是一个换行符。

例如：

    import java.io.*;
    class TestBuffer{
      public static void main(String[] args) {
        BufferedReader bf=null;
        BufferedWriter bw=null;
        try{
          bf=new BufferedReader(new FileReader("E:/workspace/java/byte.txt"));
          bw=new BufferedWriter(new FileWriter("E:/workspace/java/bytein.txt"));
          bw.write("zhangsan",0,8);
          bw.newLine();
          bw.write("lisi",0,4);
          while(true){
          String s=bf.readLine();
          if(s==null){
            break;
          }
          System.out.println(s);
          }
        }catch (Exception e) {
          System.out.println(e);
        }finally{
          try{
            bf.close();
            bw.close();
          }catch (Exception e) {
            System.out.println(e);
          }
        }
      }
    }
    执行结果：
    在 E:/workspace/java/bytein.txt 文件中写入：
    zhangsan
    lisi

# 4 随机流
RandomAccessFile 类创建的流称为随机流。既可以读文件也可以写文件。该类位于 `java.io.RandomAccessFile`。

    public class RandomAccessFile extends Object implements DataInput,Closeable

## 4.1 构造方法
1. public RandomAccessFile(File file,String mode) throws FileNotFoundException

  参数：
  file -文件对象
  mode -访问模式。取值 “r”（只读）、“rw”(可读写)

2. public RandomAccessFile(String name,String mode) throws FileNotFoundException

  参数：
  name -与系统相关的文件名
  mode -访问模式

## 4.2 常用方法
|方法|描述|
|-|-|
|close()|关闭文件|
|getFilePointer()|获取当前读写位置|
|length()|获取文件的长度|
|read()|从文件中读取一个字节的数据|
|readBoolean()|从文件中读取一个布尔值，0 代表 false，其他值表示 true|
|readByte()|从文件中读取一个字节|
|readChar()|从文件中读取一个字符（2 个字节）|
|readDouble()|读取一个双精度浮点值（8字节）|
|readFloat()|读取一个单精度浮点值（4 字节）|
|readFully(byte b[])|读 b.length 字节放入数组 b|
|readInt()|读取一个 int 值（4 个字节）|
|readLine()|读取一个文本行|
|readLong()|从文件中读取一个长型值（8 字节）|
|readShort()|从文件读取一个短型值（2 个字节）|
|readUnsignedByte()|读取一个无符号字节（1 字节）|
|readUnsignedShort()|读取一个无符号短型值（2 字节）|
|readUTF()|读取一个 UTF 字符串|
|seek(long position)|定位读写位置|
|setLength(long newlength)|设置文件的长度|
|skipBytes(int n)|在文件中跳过给定数量的字节|
|write(byte b[])|写 b.length 个字节到文件|
|writeBoolean(boolean v)|把一个布尔值作为单字节值写入文件|
|writeByte(int v)|向文件写入一个字节|
|writeBytes(String s)|向文件写入一个字符串|
|writeChar(char c)|向文件写入一个字符|
|writeChars(String s)|向文件写入一个作为字符数据的字符串|
|writeDouble(double v)|向文件写入一个双精度浮点值|
|writeFloat(float v)|向文件写入一个单精度浮点值|
|writeInt(int v)|向文件写入一个int值|
|writeLong(long v)|向文件写入一个长型 int 值|
|writeShort(int v)|向文件写入一个短型 int 值|
|writeUTF(String s)|写入一个 UTF 字符串|

# 5 文件锁
经常出现几个程序处理同一个文件的情况，例如同时更新或读取文件。应对这样的问题我们可以使用文件锁。
