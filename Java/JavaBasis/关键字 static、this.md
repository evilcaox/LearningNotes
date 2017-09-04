# 关键字 static
我们可以基于一个类创建多个该类的对象，每个对象都在堆中拥有一个独立的单元，它们之间相互独
立，都拥有自己的成员。在某些时候，我们希望该类所有的对象共享同一个成员。就需要使用 static
 关键字。

## 静态成员变量
语法：

    访问修饰符 static 变量类型 变量名;

被 static 修饰的成员变量称为静态成员或类成员。它属于整个类所有，而不是某个对象所有，即被
类的所有对象所共享。简单说就是无论哪一个对象修改了该静态成员变量，其他对象使用该成员变量
都是同一个(前一对象修改后的结果)。静态成员可以使用类名直接访问，也可以使用对象名进行访问。
一般使用类名访问。

## 静态函数
语法：

    访问修饰符 static 返回值类型 方法名(){
        方法体;
    }

**注意**
>* 静态方法中可以直接调用同类中的静态成员，但不能直接调用非静态成员。**若希望在静态方法
中调用非静态变量，可以通过对象来访问非静态变量。**
        public class Person{
          String name="李四";
          static String love="爱";
          public static void show(){
            System.out.println("名字是："+name);//错误，不能直接调用该静态变量
            System.out.println("对世界："+love);//可直接调用静态变量
            Person person=new Person();
            System.out.println("名字是："+person.name)
          }
        }
* 在普通成员方法中，则可以直接访问同类的非静态变量和静态变量。
* 静态方法中不能直接调用非静态方法，需要通过对象来访问非静态方法。

## 静态代码块
语法：

    public class Person{
      String name;
      static String love;
      //初始化块
      {
        name="李四";
        System.out.println("同一个世界同一个家园！");
      }
      //静态代码块
      {
        love="爱"；
      }
    }

**注意：**在类的声明中可以包含多个初始代码块，当创建类的实例时，就会依次执行这些代码块。
如果使用 static 修饰初始化块，就称为静态初始化块。静态初始化块只在类加载时执行，且只会
执行一次，并且静态初始化块只能给静态变量赋值，不能初始化普通的成员变量。

例：

    public class Number{
      int num1;
      int num2;
      static int num3;
      Number(){
        num1=1;
        System.out.println("使用构造方法为num1赋值！");
      }
      {
        num2=2;
        System.out.println("使用初始化代码块为num2赋值！");
      }
      static{
        num3=3;
        System.out.println("使用静态初始化代码块为num3赋值！");
      }
      public static void main(String arg[]){
        Number number=new Number();
        System.out.println("num1:"+number.num1);
        System.out.println("num2:"+number.num2);
        System.out.println("num3:"+number.num3);
        Number number1=new Number();
        System.out.println(t2.num1);
		    System.out.println(t2.num2);
		    System.out.println(t2.num3);
      }
    }

    运行结果为：
    使用静态初始化代码块为num3赋值！
    使用初始化代码块为num2赋值！
    使用构造方法为num1赋值！
    num1:1
    num2:2
    num3:3
    使用初始化代码块为num2赋值！
    使用构造方法为num1赋值！

程序在运行时静态初始化块最先被执行，然后执行普通初始化块，最后才执行构造方法。静态初始化
块只在类加载时执行一次。而初始化代码块和构造方法则创建一个对象就会被执行一次。

# 关键字 this
## 使用 this 关键字调用成员变量
当成员变量与局部变量或者形参名字相同时，根据就近原则，会自动屏蔽成员变量，要想使用成员变
量就需要使用 this 关键字。

例如：

    public class Test{
      String name;
      int age;
      public void show(int age){
        String name="李四";
        System.out.println("我的名字是："+name+"；我的年龄是："+age);
      }
      public static void main(String age){
        Test test=new Test();
        test.name="张三";
        test.age="15";
        test.show(20);
      }
    }
    执行结果为：
    我的名字是：李四；我的年龄是：20

    如果我们想输出名字为张三，年龄为15，只需更改show()方法即可，如：
    public void show(int age){
      String name="李四";
      System.out.println("我的名字是："+this.name+"；我的年龄是："+this.age);
    }
    执行结果就可改变为：
    我的名字是：张三；我的年龄是：15

## 使用 this 关键字调用成员函数
调用方法如同调用成员变量，this 表示当前对象。

## 使用 this 关键字调用构造函数
语法：

    this(参数);

例如：

    public class Test{
      String name;
      int age;

      Test(String name){
        this.name=name;
        System.out.println("一个参数的构造函数！");
      }

      Test(String name,int age){
        this(name);//相当于构造函数 Test(String name),必须放在第一行
        this.age=age;
        System.out.println("两个参数的构造函数！");
      }

      public static void main(String arg[]){
        Test test=new Test("张三"，15);
      }
    }

    执行结果：
    一个参数的构造函数！
    两个参数的构造函数！

使用 this(参数) 代替构造函数可以减少程序代码。而面向对象的一点就是减少冗余代码。
