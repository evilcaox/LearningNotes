# Object 类
Object 类是所有类的父类，如果一个类没有使用 extends 关键字明确标识继承另一个类，那么这
个类默认继承 Object 类。

# Object 类中的方法
Object 类中的方法，适合所有子类。

几个常用的 Object 类中的方法：
1. toString()方法
>在 Object 类里面定义 toString() 方法的时候返回对象的哈希 code 码(对象地址字符串),可
以通过重写 toString() 方法表示出对象的属性。
       class StringTest{
         String s="Hello";
       }
       class Test{
         public static void main(String[] args){
         StringTest st=new StringTest();
         System.out.println(st);
         }
       }
       执行结果：
       StringTest@6d06d69c
       给 StringTest 类重写 toString() 方法,不改变 Test 类。
       class StringTest{
         String s="Hello";
         pbulic String toSting(){
           return "String[s="+s+"]"
         }
       }
       执行结果：
       StringTest[s=Hello]

2. equals() 方法
在 Object 类中的 equals() 方法比较的是对象的引用是否指向同一块内存地址。代码如下：
    public boolean equals(Object obj) {
        return (this == obj);
    }
这与 `==` 的作用是一样的。但是一般情况下我们通过重写 equals() 方法来比较两个对象内容是
否相等。一般情况下，对象的内容相等需要符合两个条件：`对象的类型相同(使用 instanceof 操作符比较)；两个对象的成员变量的值完全相同。`如下：

    public class User extends Object{
        int age;
        String name;
        User(int age,String name){
          this.age=age;
          this.name=name;
        }
        public boolean equals(Object obj){
          //如果两个对象指向同一个引用，返回true
          if(this==obj){
            return true;
          }
          boolean b=obj instanceof User;//判断Obj 对象是否是  User 类型
          if(b){
            User u=(User)obj;//将对象向下转型为 User 类型，我觉得之前它上转型为 Object 类型了
            if(this.age==u.age&&this.name.equals(u.name)){//String 类型属于引用类型，所以不能直接用 == 判断相等而应该用 equals() 方法
              return true;
              }else{
                return false;
              }
              }else{
                return false;
              }
            }
          }
          public class TestHashSet {
            public static void main(String args []){
	             User u1=new User(12,"zhangsan");
	             User u2=new User(12,"lisi");
	             User u3=new User(12,"zhangsan");
	             System.out.println(u1.equals(u2));
	             System.out.println(u1.equals(u3));
	             System.out.println(u2.equals(u3));
            }
          }
          执行结果：
          false
          true
          false
