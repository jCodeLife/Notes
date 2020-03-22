**关于ES6新的变量声明方式**

在ES5中，变量声明只有var 和function以及隐式声明三种，而ES6中新增了let、const import和class四种。
- let
```
1. let的块级作用域
let声明的变量的作用域是块级作用域，在ES5 并没有块级作用域，只有函数作用域和全局作用域。
for (var i = 0; i <10; i++) {  
  setTimeout(function() {  // 同步注册回调函数到异步的宏任务队列。
    console.log(i);        // 执行此代码时，同步代码for循环已经执行完成
  }, 0);
}
// 输出结果
10   （共10个）
// 这里变量为i的for循环中，i是一个全局变量，在全局范围内都有效，
//所以每一次循环，新的i值都会覆盖旧值，导致最后输出的是最后一轮i的值，即i的最终结果为10个10。

把 var改成 let声明：
for (let i = 0; i < 10; i++) { 
  setTimeout(function() {
    console.log(i);    
//当前的i仅在本轮的循环中有效，就是说每一次循环，i其实都是一个新产生的变量。                      
//用 let 声明的变量 i 只作用于循环体内部，不受外界干扰。
  }, 0);
}
// 输出结果：
0  1  2  3  4  5  6  7  8 9
这时在全局console.log(i)，结果报错：
Uncaught ReferenceError: i is not defined

*JS中的for循环体比较特殊，每次执行都是一个全新的独立的块作用域，
用let声明的变量传入到 for循环体的作用域后，不会发生改变，不受外界的影响。*


2. let的TDZ--暂时性死区（Temporal Dead Zone）
其实所谓的暂时性死区就是：即变量所在的作用域的开始位置，到变量声明那行结束的空间位置区域。
只要变量一进入TDZ作用域，该变量其实就已经存在了，但是不可获取，
只有等到声明变量的那一行代码出现，才可以获取和使用该变量。
临时死区导致let变量并不能在声明前使用

暂时性死区的意义也是让我们标准化代码，将所有变量的声明放在作用域的最开始。

在一个块级作用域中，变量唯一存在，一旦在块级作用域中用let声明了一个变量，
那么这个变量就唯一属于这个块级作用域，不受外部变量的影响


3.let不允许重复声明（在同一个作用域）
(1) 在相同的作用域内，用let声明变量时，只允许声明一遍，但 var是可以多次声明的。
function fun() {
  let a = '123';
  var a = '456';// 报错
}
function fun() {
  let a = '123';
  let a = '456';// 报错
}
(2) 不能在函数内部重新声明参数，
function fun(a) {
  let a; // 报错
}

4. let 没有预解析，不存在变量提升；
也就是变量定于在哪里，就从哪里开始可以使用。这点跟TDZ相映。

```
- **const**
```
const的特性与let基本一致：块级作用域、暂时性死区、不能重复声明，没有变量提升等。
不同的是
1. const是用来定义常量；
2. const声明的常量的值，必须在声明的时候赋值，并且赋值后不能修改；
3. 特殊情况，当声明的常量是一个对象时：
那么对于对象本身是不允许重新赋值的，但是对于对象的属性是可以重新赋值的。
const obj = {};
obj.name = 'xxx';
console.log(obj.name);    //'xxx'
注：
1.实际上const能保证的，并不是变量的值不得改动，而是变量指向的那个内存地址所保存的数据不得改动。

对于像数值、字符串、布尔值的简单数据类型，值就保存在变量指向的那个内存地址，因此等同于常量。
但对于像对象、数组这样的复合类型的数据，变量指向的内存地址，保存的只是一个指向实际数据的指针。

2.要彻底将对象或数组冻结，让其属性也不可修改，可使用Object.freeze(obj)方法。
const obj = {
  prop: 10
};
Object.freeze(obj);

obj.prop = 33;// error

console.log(obj.prop);//10


```

- **import**
```
ES6采用import来代替node等的require来导入模块。
import {$} from './jquery.js'  
//$对象就是jquery中export暴露的对象。

import命令要使用as关键字，将输入的变量重命名
import { A as $ } from './jquery.js';

注意，import命令具有提升效果，会提升到整个模块的头部，首先执行。
```
- **class**
```
ES6引入了类的概念-class
1. 定义一个类
class Person{
 constructor(name, age) {
        this.name = name;
        this.age = age;
  }   
 //...more code
}
constructor方法，就是构造方法，是ES5时代函数对象的主体，而this关键字则代表实例对象。
function Person(name, age){
        this.name = name;
        this.age = age;
}

2.生成类的实例对象
与ES5通过构造函数生成对象完全一样，也是使用new命令
class Person{};
let student= new Person();

注：
Class其实就是一个function，不同的是，Class不存在变量提升，并且Class声明定义必须在使用之前。

```
 在ES6之前，JavaScript是没有块级作用域的，如果在块内使用var声明一个变量，它在代码块外面仍旧是可见的。ES6规范给开发者带来了块级作用域，let和const都添加了块级作用域，使得JS更严谨和规范。
```
*Question：
1.let 与 const 相同点：
块级作用域
有暂时性死区 
约束了变量提升 
禁止重复声明变量 

2.let 与 const不同点：
const声明的变量不能重新赋值，也是由于这个规则，const变量声明时必须初始化，不能留到以后赋值。

```
