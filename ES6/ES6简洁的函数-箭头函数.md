ES6标准新增了一种新的函数：Arrow Function（箭头函数）， 允许使用“=>”定义函数，是一种简写的函数表达式。
- 箭头函数语法
```
//  一个参数对应一个表达式
 x => x+2;

// 多个参数对应一个表达式
 (x,y) => (x + y);

// 一个参数对应多个表示式
x = > { x++; return x;};

//  多个参数对应多个表达式
(x,y) => { x++;y++;return x*y;};

//表达式里没有参数
var flag = (() => 2)(); flag等于2

var flag = (() => {return 1;})(); flag就等于1

 //传入一个表达式，返回一个对象
var f = (x) => ({key:x})
        var obj = f(1);
        alert(obj);//{key:1}

小结：
看上去很多格式，其实只要记住完整的
() => {
  //语句
  //return
}

其实主要看什么时候省略()和{}：
当函数参数个数为1时，可省略()；
 x=> { ... } 
当函数参数个数大于1或者没有参数时，不省略()；
() => { ... }  
(x, y) => { ... }
如果只有一个return，{}可以省略即：
当右边表达式个数为1时，可以省略{}；
当右边表达式个数大于1时，不省略{}

特点：箭头函数是一种简写的函数表达式，函数表达式的名会直接忽略。所以箭头函数不能用作构造函数。

```
- **箭头函数中的 this**
```
箭头函数内的this值继承自外围作用域。
运行时会首先到父作用域找，如果父作用域还是箭头函数，那么接着向上找，直到找到我们要的this指向。
即箭头函数中的 this继承父级的this(父级非箭头函数)。

由于this在箭头函数中已经按照词法作用域绑定了，
所以，用call或者apply调用箭头函数时，无法对this进行绑定，即传入的第一个参数被忽略。


```
- **箭头函数中的特性**
```
1.箭头函数中的 this继承自外围父作用域；
2.箭头函数没有 arguments；(可以使用...args,变成数组)
3.箭头函数不能当作构造函数，不能new；
4.箭头函数没有原型属性；
5.箭头函数不能换行；
```
- **箭头函数使用场景性**
```
1.简化回调函数

[1,2,3].map(x => x * x);
2.在事件监听函数里使用
document.body.addEventListener('click', event=>console.log(event, this)); 
3.解决this问题，如：定时循环器，正常函数里面的this指向window，一般时在父级保存以下this，var self = this;但如果用箭头函数，则也同样可以指向继承父级函数里面的this。

```
- **箭头函数的优点**
```
简洁的语法，更直观的作用域和 this的绑定，它能让我们能很好的处理this的指向问题。
```

- **函数的其他变化**
```
1.函数可以有默认参数
2.函数参数默认已经被定义，在里面不能再使用let或者const声明；
3.扩展运算符...：可以展开数组或重置成数组，可以利用这个拷贝数组等操作
```
