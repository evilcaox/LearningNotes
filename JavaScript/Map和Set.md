JavaScript 的默认对象表示方法 `{}` 可以视为其他语言中的 Map 等数据结构，即一组键值对。但是 JavaScript 的对象有个问题，就是键必须是字符串。为了解决这个问题，最新的 ES6 规范引入了新的数据类型 Map。

# Map
Map 是一组键值对的结构，具有极快的查找速度。如果用 Map 实现，只需要一个“键-值”对照表，直接根据名字查找成绩，无论这个表有多大，查找速度都不会变慢。语法如下：

    var m=new Map([['张三',98],['李四'，96],['王二',88]]);
    m.get('王二');//88

初始化 Map 需要一个二维数组，或者直接初始化一个空 Map。Map 具有以下方法：

    var m=new Map();
    m.set('张三',80);//添加新的内容
    m.set('李四',88);
    m.has('王二');//返回 false， 不存在键 '王二'
    m.delete('张三');//删除张三
    m.get('张三');//undefined
    m.set('李四',100);//覆盖之前的 88

# Set
Set 内没有键，只含值且值不可以重复，若出现重复的值则会被自动过滤。要创建一个 Set，需要提供一个 Array 作为输入，或者直接创建一个空 Set。

    var s1=new Set([1,2,3]);
    var s2=new Set();
    s2.add(4);//增加元素
    s1.add(1);//重复元素自动过滤，Set 内还为 [1,2,3]
    s1.delete(1);//删除元素1

# Map 与 Set的遍历
为了统一集合类型，ES6 标准引入新的 `iterable` 类型，Array、Map 和 Set 都属于 iterable 类型。具有 iteration 类型的集合可以通过新的 `for……of` 循环来遍历。

`for……of` 循环是 ES6 引入的新的语法，用 `for……of` 循环遍历集合，用法如下：

    var a=[1,2,3];
    var s=new Set(['a','b','c']);
    var m=new Map([[1,'A'],[2,'B'],[3,'C']]);
    //遍历Array
    for(var x of a){
      document.write(x);
    }
    //遍历Set
    for(var x of s){
      document.write(x);
    }
    //遍历Map
    for(var x of m){
      document.write(x[0]+' '+x[1]);
    }

`for……of` 与 `for……in` 循环的区别：
>`for……in` 循环遍历的实际上是对象的属性名称。一个 Array 数组实际上也是一个对象，它的每个元素的索引被视为一个属性。当我们手动给 Array 对象添加了额外的属性后，`for……in` 循环将带来意想不到的意外效果：

    var a=['a','b','c'];
    a.name='Hello';
    for(var x in a){
      alert(x);
    }
    //输出
    '0','1','2'，'name'
>`for……in` 循环将把 `name` 包括在内，但 `Array` 的 length 属性却不包含在内。`for……of` 循环修复了这些问题，它只循环集合本身的元素：

    var a=['a','b','c'];
    a.name='Hello';
    for(var x of a){
      alert(x);//'a','b','c'
    }

然而，更好的方式是直接使用 iterable 内置的 `forEach` 方法，它接收一个函数，每次迭代就自动回调该函数。以 Array 为例：

    var a=['a','b','c'];
    a.forEach(function(element,indx,array){
      //element -指向当前元素的值
      //index -指向当前索引
      //array -指向Array对象本身
      alert(element);
      });
