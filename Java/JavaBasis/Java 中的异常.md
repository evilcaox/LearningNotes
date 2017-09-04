# 什么是异常
中断正常指令流的事件叫做异常。

# 异常分类
所以异常的父类都为 Throuable。Throuable 有两个子类为 Exception 和 Error。Exception
下有很多各种异常的子类。主要分为非检查异常和检查异常。比如 RuntimeException 就属于非检
查异常，需要在执行时才能出错。

# 异常捕捉
我们可以使用 `try-catch-finally` 进行异常捕捉。

例如：

    class Test{
      public static void main(String[] args){
        int i=1/0;
      }
    }

    执行结果：
    Exception in thread "main" java.lang.ArithmeticException:/by zero
             at Test.main(Test.java:3)

这就是一个隶属于 RuntimeException 的算术异常。为了让程序能执行异常后面的代码，我们必须
对异常进行处理。

# try-catch
将上面的代码修改为：

    class Test{
      public static void main(String[] args) {
        try{
          System.out.println(1);
          int i=1/0;
          System.out.println(2);
        }catch(Exception e){
          System.out.println(3);
          e.printStackTrace();//打印异常栈信息
      }
      }
    }

    执行结果为：
    1
    3
    java.lang.ArithmeticException:/by zero
             at Test.main(Test.java:4)

若 try {}中的代码没有异常，则不会执行 catch {}里的代码块。若 try 中代码出现异常，则执
行 catch {}中的代码。

      class Test{
        public static void main(String[] args) {
          try{
            System.out.println(1);
            int i=1/1;
            System.out.println(2);
          }catch(Exception e){
            System.out.println(3);
            e.printStackTrace();//打印异常栈信息
         }
        }
     }

     执行结果为：
     1
     2

# try-catch-finally

    class Test{
      public static void main(String[] args){
        try{
          System.out.println(1);
          int i=1/0;
          System.out.println(2);
        }catch(Exception e){
          System.out.println(3);
          e.printStackTrace();
        }finally{
          System.out.println(4);
        }
      }
    }

    执行结果为：
    1
    3
    4

finally {}中代码无论是否出现异常都将被执行。

# throws 与 throw
`throws`声明将要抛出何种类型的异常。`throw`将产生的异常抛出。

    class Person{
      int age;

      public void setAge(int age){
        if(age<=0){
          RuntimeException e=new RuntimeException("年龄必须大于0");
          throw e;
        }else{
          this.age=age;
      }
    }
    class Test{
      public static void main(String[] args) {
        Person p=new Person();
        p.setAge(-20);
      }
    }

    执行结果为：
    Exception in thread "main" java.lang.RuntimeException:年龄必须大于0
             at person.setAge(person.java:6)
             at Test.main(Test.java:4)

使用 throw 可以抛出 Exception 子类的异常，如果抛出 Exception 异常会发生以下状况。

    class Person{
      int age;

      public void setAge(int age){
        if(age<=0){
          Exception e=new Exception("年龄必须大于0");
          throw e;
        }else{
          this.age=age;
        }
      }
    }
    //Test类不变

    在编译时出现错误：
    Person.java:7: 错误：未报告的异常错误Exception；必须对其进行捕获或声明以便抛出
          throw e;

捕获我们可以使用`try-catch`进行，声明我们可以使用`throws`。将setAge方法该为如下所示：

    public void setAge(int age) throws Exception{
      if(age<=0){
        Exception e=new Exception("年龄必须大于0");
        throw e;
      }else{
        this.age=age;
      }
    }

    此时不对Test类作改变编译时出错：
    Test.java:4:错误：未报告的异常错误Exception；必须对其进行捕获或声明以便抛出
      p.setAge(-20);

使用`throws`抛出异常时由调用该方法的地方对异常进行处理。修改Test类如下：

    class Test{
      public static void main(String[] args) {
        Person p=new Person();
        try{
            p.setAge(-20);
        }catch(Exception e){
          e.printStackTrace();
        }
      }
    }
    执行结果为：
    java.lang.Exception:年龄必须大于0
        at Person.setAge(Person.java:7)
        at Test.main(Test.java:5)
