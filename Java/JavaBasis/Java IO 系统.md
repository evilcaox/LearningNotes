# InputStream 和 OutputStream
## InputStream
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

### FileInputStream
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

# OutputStream
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

## FileOutputStream
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

# FileReader
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

# FileWriter
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

# BufferedReader
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

# BufferedWriter
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
