- **什么是解构**(Destructuring)
汉语中，解构是指对某种事物的结构和内容进行剖析；
在ES6中
**解构是:按照一定的模式，从数组或对象中提取值的过程。**
解构赋值就是：按照一定的模式从数组或对象中取值，对变量进行赋值的过程。
```
没有解构赋值前
var arr =[1,2,3,4,5,6,7,8,9];
var a= arr[0];
var b= arr[1];
var c= arr[2];
....
var i = arr[8];

使用解构赋值：
let[a,b,c,d,e,f,g,h,i] = arr;

注：
1.使用解构赋值，将会使等效的代码变得更加简洁并且可读性更高；
2.本质上，解构赋值属于一种“模式匹配”、“映射关系”；
只要等号两边的模式相同，一一对应，左边的变量就会被赋予右边对应的值。

但注意：
左边数组中没有找到右边数组中对应值，则解构不尽人意：
let [x,y,z] = [1,2];
x // 1
y // 2
z //undefined

当然可以给解构的对象设置一个默认值
var [x='a',y='a',z='a'] = ['a','b'];
x // 'a' 三个参数都有设置默认值a,有传'a' ，所以x='a' 
y // 'b' 默认值会被传入的覆盖
z // 'c' 没有传入会使用默认值

解构的过程相当于就是分解、匹配的过程
```


- **数组的解构赋值**
```
1. 数组解构赋值特点
根据数组数据的下标，有次序的赋值；
本质上，只要等号两边模式一致，左边变量即可获取右边对应位置的值。
let [a,b,c] = [1,2,3];//es6
2. 对嵌套数组解构
let [a, [[b], c],d] = [1, [[2], 3],4];
console.log(a); // 1
console.log(b); // 2
console.log(c);  // 3
console.log(d); // 4
能够非常迅速的获取二维数组、三维数组，甚至多维数组中的值；
3.不需要匹配的位置可以置空
[,,c] = [1, 2, 3];
console.log(c);//3
4.使用...扩展运算符，匹配余下的所以值，形成一个数组
var [a,b,...c] = [1,2,3,4,5,6,7,8,9];
a//1
b//2
c//[3,4,5,6,7,8,9]
```

- **对象的解构赋值**
```
1.特点
数组的元素是按次序排列的，变量的取值由它的位置决定；
而对象的属性没有次序，变量必须与属性同名，才能取到正确的值。
let { a, b } = { a : 1, c : 2 };
a // 1
b // undefined

2.对任意深度的嵌套对象进行解构
let obj= {
   arr: [1,{ a: 2 } ]
 };
 let { arr: [x, { y}] } = obj;
 console.log(x); // 1
 console.log(y); // 2

3.自定义属性名称
var {name, id: ID} = { name: 'jack', id: 1  };
ID // 1
id // Uncaught ReferenceError: id is not defined
对象的解构赋值的内部机制，是先找到同名属性，然后再赋给对应的变量;
真正被赋值的是后者。
```
- **字符串解构**
```
字符串也可以解构赋值
const [a, b, c, d, e] = 'hello';
a // "h"
b // "e"
c // "l"
d // "l"
e // "o"
```
- **数值和布尔值的解构赋值**
```
只要等号右边的值不是对象或数组，就先将其转为对象。
如果转换之后的对象或原对象拥有Iterator接口，则可以进行解构赋值，否则会报错。
null或undefined不能转换成此类对象，所以解构的话会报错。
```
- **圆括号的用法**
```
如果在解构之前就已经定义了对象
let obj;
{obj}={obj:'James'};//报错
大括号{}位于行首，JS引擎 就会认为 { obj } 是一个代码块，所以等号就出问题了。
解决方式是在包裹一层括号（）
let obj;
（{obj}={obj:'James'}）;
//括号的出现，让整个解构赋值的结构被看做一个代码块，而内部的 { obj } 模式则可以正常匹配到。
```
- **解构的用途**
```
1.交换变量
let a = 1;
let b = 2;
[a,b] = [b,a];

2.函数参数
// 参数是一组有次序的值
function foo([width,height,left,right]) { 
    //... 
}
foo([100, 200, 300, 300])

// 参数是一组无次序的值
function foo({width,height,left,right}){
     // ...
}
foo([left:300, width:100, right:300, height:200,])

3. 配置对象参数默认值
避免每个属性都重复var foo = config.foo || theDefaultFoo操作
jQuery.ajax = function (url, {
      async = true,
      beforeSend = noop,
      cache = true,
      complete = noop,
      crossDomain = false,
      global = true,
      // ... 更多配置 
 }) {  // ...  };

4.函数返回多个值
// 返回一个数组
function foo() {
  return [1, 2, 3];
}
let [a, b, c] = foo();

// 返回一个对象
function foo2() {
  return {
    a: 1,
    b: 2
  };
}
let { a, b } = foo2();

5.引入模块的指定方法
加载模块时，往往需要指定输入那些方法。
import { xxx} from 'xxxx'
```

