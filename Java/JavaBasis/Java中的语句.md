# 语句概述
Java 中的语句可分为以下六种：

1. 方法调用语句 `eg:System.out.println("Hello!")`
2. 表达式语句
 > 由一个表达式构成一个语句，即表达式尾加上分号。`eg：x=5;`
3. 符合语句
>可以用{}把一些语句括起来构成符合语句。
4. 空语句
>一个分号也是一条语句，称为空语句。
5. 控制语句
> 控制语句分为条件分支语句、开关语句和循环语句。
6. package 语句和 import 语句
>package 语句和 import 语句与类、对象有关。

# 控制语句
1. if 条件分支语句
>条件分支语句按语法可分为三种形式，分别为：`if`、`if-else`、`if-else if-else`。

 1.1 if 语句
 >语法:
       if(boolean型表达式){
         若干语句
       }

  说明：`boolean型表达式`的意思为该表达式运算结果的值必须为`boolean型`。`当`boolean型表达式`值为 true 时，则紧跟着执行复合语句，结束当前 if 语句的执行；若值为 false，结束当前 if 语句的执行。若复合语句中只有一条语句，可以省略{}。

 1.2 if-else 语句
 >语法：
       if(boolean型表达式){
        若干语句
       }else{
        若干语句
        }

  说明：当`boolean型表达式`的值为 true 时，执行紧跟着的复合语句，结束`if-else`语句；若值为 false ，则执行`else`后面的复合语句，结束当前`if-else`语句。

  执行过程如图：
  ![if-else](http://opshmdbwb.bkt.clouddn.com/if-else.jpg)

  1.3 if-else if-else 语句
  >语法：
       if(boolean表达式){
         若干语句
       }else if(boolean表达式){
         若干语句
       }
       ……
       else{
         若干语句
       }

 说明：当第一个`boolean表达式`值为 true 时，执行紧跟着的语句，结束当前`if-else if-else`。若值为 false,则执行`else`后面的`if`中的第二个`boolean表达式`，若值为 true 则执紧跟着的复合语句，结束`if-else if-else`。若值为 false，则执行`else`后面的`if`中的第三个`boolean表达式`，若值为 true 则执紧跟着的复合语句，结束`if-else if-else`。……假设最后一个`boolean表达式`之前的`boolean表达式`都为false，则此时判断最后一个`boolean表达式`,若值为 true，执行紧跟着的复合语句，若值为 false，则执行最后一个 else 后紧跟着的复合语句。

 执行过程如图：
 ![if-elsetwo](http://opshmdbwb.bkt.clouddn.com/if-elsetwo.jpg)

 1.4 if 嵌套
 >语法：
       if(boolean表达式1){
         if(boolean表达式2){
           if(boolean表达式3){
             ……
           }else{
             若干语句3;
           }
         }else{
           若干语句2;
         }
       }else{
         若干语句1;
       }

 执行过程如图：
 ![ifqt](http://opshmdbwb.bkt.clouddn.com/ifqt.jpg)

# switch 语句

语法：

    switch (表达式) {
      case 常量值 1:
        若干语句;
      break;
      case 常量值 2:
        若干语句;
      break;
      ……
      case 常量值 n:
        若干语句;
      break;
      default:
        若干语句;
    }

注意：
>1. 表达式中的值可以是`byte`、`short`、`String`、`int`或`char`型;
2. `常量值 1`、`常量值 2`……`常量值 n`必须也是`byte`、`short`、`int`或`char`型，而且要互不相同,其中`常量值`可以是常量数值，也可以是一个常量表达式，但不能是变量或带有变量的表达式；
3. 可以把功能相同的`case`语句合并起来，如：
       case 1:
       case 2:
        System.out.pringt("功能相同！");
       break;
4. `defaule块`可以出现在任意位置，也可以省略。

执行过程：
>switch 语句首先就算表达式的值，当表达式的值和`case`语句后的值相同时，从该位置开始向下执行，直到遇到`break`语句或者`switch语句块结束`；若没有匹配的`case`语句,则执行`defaule`块的代码。

# while 循环

语法：

    while(判断条件){
     循环操作
    }

执行过程：
>1. 判断`while`后面的条件是否成立（true/false).
2. 条件成立，执行循环内的操作代码，然后重复执行 1、2，直到条件不满足。

特点：先判断，再执行。

# do while 循环

语法：

    do{
      循环操作;
    }while(判断条件);

执行过程：
>1. 先执行一边循环操作，然后判断循环条件是否满足；
2. 如果条件满足，继续执行 1、2 直到条件不满足。

特点：先执行，再判断。保证循环至少被执行了一次。

# for 循环

语法：

    for(循环变量初始化;循环条件;循环变量变化){
      循环操作;
    }

执行过程：
>1. 执行循环变量初始化部分，设置循环的初始状态，此部分在整个循环中只执行一次。
2. 进行循环条件的判断，如果条件为 true,则执行循环体内代码。若为 false，则结束 for 循环。
3. 执行循环变量变化部分，改变循环变量的值，以便进行下一次条件判断。
4. 依次执行 2、3、4，直到不满足条件退出循环。

注意：
>1. for 关键字后面的括号中的三个表达式必须用“;”隔开，三个表达式都可以省略，但";"不能省略。
2. for 循环变量初始化和循环变量变化部分，可以使用“,”同时初始化或改变多个循环变量的值。
3. 循环条件部分可以使用逻辑运算符组合的表达式，表示复杂判断条件，注意运算优先级。

# 多重循环

循环中包含循环语句的结构称为多重循环。三种循环语句都可以自身嵌套，也可以相互嵌套，最常见的就是二重循环。在二重循环中，外层没循环一次，内层循环要执行完一整个循环。

eg:

    while(循环条件1){
      循环操作1;
      while(循环条件2){
        循环操作2;
      }
    }

    do{
      循环操作1;
      do{
        循环操作2;
      }while(循环条件2);
    }while(循环条件1);

    for(;循环条件1;){
      循环操作1;
      for(;循环条件2;){
        循环操作2;
      }
    }

    while(循环条件1){
      循环操作1;
      for(;循环条件2;){
        循环操作2;
      }
    }

eg:打印一个正方形

    for(int a=0;a<4;a++){
      for(int b=0;b<4;b++){
        System.out.print("*");
    }
      System.out.println();
    }

# break 和 continue

>`break`的作用是跳出循环，执行循环后的语句。

>`continue`的作用是跳过循环体中剩余语句执行下一次循环。
