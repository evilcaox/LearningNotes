# String 类
## Java 中的字符串
在 Java 中，字符串被作为 String 类型的对象处理，String 类位于 java.lang 包中。默认情况下该包自动导入所有程序。

创建字符串的方法：

    String s1="abc";
    String s2=new String();
    String s3=new String("abc");

## Java 中字符的不变性
String 对象创建后就不能被更改，是不可变的，所谓的修改其实是创建了新的对象，所指向的内存空间不同。

    String str1="abc";
    String str2="abc";
    String str3=new String("abc");
    String str4=new String("abc");
    //多次出现的字符常量，Java 编译程序只创建一个，所以返回true
    System.out.println(str1==str2);
    //new String("abc") 新创建一个对象，即使内容相同，他们在堆中的位置也不同，故返回false
    System.out.println(str1==str3);
    //同上
    System.out.println(str3==str4);
    str1="def";
    //更改str1，指向新的内存空间，返回false
    System.out.println(str1==str2);

## String 类中的常用方法
String 类常用方法：

|方法|说明|
|-|-|
|int length()|返回当前字符串的长度|
|int indexOf(int ch)|查找 ch 字符在该字符串中第一次出现的位置|
|int indexOf(String str)|查找 str 子字符串在该字符串中第一次出现的位置|
|int lastIndexOf(int ch)|查找 ch 字符在该字符串中出现的最后一次的位置|
|int lastIndexOf(String str)|查找 str 子字符串在该字符串中出现的最后一次的位置|
|String substring(int beginIndex)|获取从 beginIndex 位置开始到结束的子字符串|
|String substring(int beginIndex,int endIndex)|获取从 beginIndex 开始到 endIndex 结束的子字符串|
|String trim()|返回去除了前后空格的字符串|
|boolean equals(Object obj)|将该字符串与指定对象相比，返回 true 或 false|
|String toLowerCase()|将字符串转换为小写|
|String toUpperCase()|将字符串转换为大写|
|char charAt(int index)|获取字符串中指定位置的字符|
|String[] split(String regex,int limit)|根据 regex 将字符串分割，limit 表示 regex 运用次数|
|byte[] getByte()|将字符串转换为 byte 数组|

**注意：**
1. 字符串的索引从 0 开始。
2. 使用 indexOf 进行字符或字符串查找时，如果匹配返回位置索引；如果没有匹配结果，返回 -1。
3. 使用 substring(beginIndex,endIndex) 进行字符串截取时，包括 beginIndex 位置的字符，不包括 endIndex 位置的字符。

# StringBuilder 类
使用 String 对象频繁操作字符串时，会额外产生很多临时变量。使用 StringBuilder 或 StringBuffer
就可以避免这个问题。StringBuilder 和 StringBuffer 基本相似，不同之处是 StringBuffer
是线程安全的，StringBuilder 没有实现线程安全功能，所以性能比较高。

创建 StringBuilder 类对象：

    StringBuilder str1=new StringBuilder();//空的 StringBuilder 对象
    StringBuilder str2=new StringBuilder("abc");//创建一个字符串 "abc"

## StringBuilder 类的常用方法
|方法|说明|
|-|-|
|StringBuilder append(参数)|追加内容到当前 StringBuilder 对象的末尾|
|StringBuilder insert(位置,参数)|将内容插入到 StringBuilder 对象的指定位置|
|int length()|获取字符串的长度|
