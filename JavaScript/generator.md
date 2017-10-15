# generator
generator (生成器)是 ES6 标准引入的新的数据类型。一个 generator 看上去想一个函数，但可以返回多次。

如下是函数的定义：

    function foo(x){
      return x+x;
    }
    var r=foo(1);//调用 foo 函数

函数在执行过程中
