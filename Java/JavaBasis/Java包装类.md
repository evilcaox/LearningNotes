# 包装类
Java 中的数据类型包括基本数据类型和引用数据类型。基本数据类型不具备对象的特性，比如基本
数据类型不能调用方法、功能简单等。为了让基本数据类型也具备对象的特性，Java为每个基本数据
类型提供一个包装类，这样就能像操作对象那样来操作基本数据类型。

基本数据类型和包装类之间的对应关系：

|基本类型|对应包装类|
|-|-|
|byte|Byte|
|short|SHort|
|int|Integer|
|long|Long|
|float|Float|
|double|Double|
|char|Character|
|boolean|Boolean|
包装类主要提供两大类方法：
1. 将本类型和其他基本类型进行转换的方法
2. 将字符串和本类型及包装类型互相转换的方法

## Java 中基本类型和包装类之间的转换
基本类型和包装类之间需要互相转换，以 Integer 为例(其他基本类型与包装类操作相似)：

    Integer a=new Integer(3);//定义 Integer 包装类对象
    int b=a+5;//将对象和基本类型进行运算
在 JDK1.5 引入自动装箱和拆箱的机制。

装箱：把基本类型转换成包装类，使其具有对象的性质，分为手动装箱和自动装箱。

    int i=10;//定义一个 int 基本类型值
    Integer x=new Integer(i);//手动装箱
    Integer y=i;//自动装箱
拆箱：和装箱相反，把包装类对象转换成基本类型的值，又可分为手动拆箱和自动拆箱。

    Integer j=new Integer(8);//定义一个Integer 包装类对象。
    int m=j.intValue();//手动拆箱为 int 类型
    int n=j;//自动拆箱

# Java 中基本类型和字符串之间的转换
## 基本数据类型转换为字符串
基本数据类型转换为字符串有三种方法：
1. 使用包装类的 toString() 方法
2. 使用 String 类的 valueOf() 方法
3. 用一个空字符加上基本类型，得到的就是基本类型数据对应的字符串

        int s=10;
        String str1=Integer.toString(c);//利用包装类
        String str2=String.valueOf(c);//使用 valueOf
        String str3=s+"";//空字符加基本类型

## 字符串转换为基本类型
将字符串转换成基本类型有两种方法：
1. 调用基本数据类型的包装类的 parseXxx 静态方法
2. 调用基本数据类型的包装类的 valueOf 方法转换

    String str="1001";
    int a=Integer.parseInt(str);
    int b=Integer.valueOf(str);
