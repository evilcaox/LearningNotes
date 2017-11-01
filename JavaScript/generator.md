# generator
generator (生成器)是 ES6 标准引入的新的数据类型。一个 generator 看上去想一个函数，但可以返回多次。

如下是函数的定义：

    function foo(x){
      return x+x;
    }
    var r=foo(1);//调用 foo 函数

函数在执行过程中，如果没有遇到 `return` 语句（函数末尾如果没有 `return`,就是隐含的 `return undefined;`），控制权无法交回被调用的代码。

generator 跟函数很像，定义如下：

    function* foo(x){
      yield x+1;
      yield x+2;
      return x+3;
    }

generator 和函数不同的是，generator 由 `function*` 定义，并且，除了 `return` 语句，还可以用 `yield` 返回多次。

例如斐波那契数列（0，1，1，2，3，5，8……）：

    function fib(max){
      var t,a=0,b=1,arr=[0,1];
      while(arr.length<max){
        t=a+b;
        a=b;
        b=t;
        arr.push(t);
      }
      return arr;
    }

函数只能返回一次，所以必须返回一个 Array。但是，如果换成 generator，就可以一次返回一个数，不断返回多次。如：

    function* fib(max){
      var t,a=0,b=1,n=1;
      while(n<max){
        yield a;
        t=a+b;
        a=b;
        b=t;
        n++;
      }
      return a;
    }
    fib(5);//fib{[[GeneratorStatus]]:"suspended",[[GeneratorReceiver]]:Window}

直接调用一个 generator 和调用函数不一样，`fib(5)` 仅仅是创建了一个 generator 对象，还没有去执行它。

调用 generator 对象有两个方法，一是不断地调用 generator 对象的 `next()` :

    var f=fib(5);
    f.next();//{value:0,done:false}
    f.next();//{value:1,done:false}
    f.next();//{value:1,done:false}
    f.next();//{value:2,done:false}

`next()` 方法会执行 generator 的代码，然后，每次遇到 `yield x;`就返回一个对象{value:x,done:true/false},然后‘暂停’。返回的 value 就是 `yield` 的返回值，`done` 表示这个 generator 是否已经执行结束。如果 `done` 为 `true`，则 `value` 就是 `return` 的返回值.

当执行到 `done` 为 `true`，这个 generator 对象就已经全部执行完毕，不要再继续调用 `next()` 了。

第二个方法是直接用 'for...of' 循环迭代 generator 对象，这种方法不需要我们自己判断done:

    for(var x of fib(5)){
      console.log(x);//依次输出0,1,1,2,3
    }

generator 和普通函数相比，有什么用？

因为 generator 可以在执行过程中多次返回，所以它看上去就像一个可以记住执行状态的函数，利用这一点，写一个 generator 就可以实现需要用面向对象才能实现的功能。例如，用一个对象来保存状态：

    var fib={
      a:0,
      b:1,
      n:0,
      max:5,
      next:function(){
        var r=this.a,t=this.a+this.b;
        this.a=this.b;
        this.b=t;
        if(this.n<this.max){
          this.n ++;
          return r;
        }else{
          return undefined;
        }
      }
    };

用对象的属性来保存状态，相当繁琐。

generator 还有另一个巨大的好处，就是把异步回调代码变成 “同步” 代码。这个好处在 AJAX 中才能体会。

没有 generator 之前，用 AJAX 时需要这么写代码：

    ajax('http://url-1',data1,function(err,result){
      if(err){
        return handle(err);
      }
      ajax('http://url-2',data2,function(err,result){
        if(err){
          return handle(err);
        }
        ajax('http://url-3',data3,function(err,result){
          if(err){
            return handle(err);
          }
          return success(result);
          });
        });
      });

回调越多，代码越难看。

有了 generator 后，可以这么写：

    try{
      r1=yield ajax('http://url-1',data1);
      r2=yield ajax('http://url-2',data2);
      r3=yield ajax('http://url-3',data3);
      sucess(r3);
    }catch(err){
      handle(err);
    }
