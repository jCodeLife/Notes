JavaScript语言自创立之初，一直没有模块（module）体系，在ES6之前，一些前端社区制定了模块加载方案，最主要的有CommonJS和AMD两种。前者用于服务器，后者用于浏览器。但这两种规范都由开源社区制定，没有统一。
ES6中引入了模块（Module）体系，从语言层在实现了模块机制，实现了模块功能，而且实现得相当简单，为JavaScript开发大型的、复杂的项目扫清了障碍。
ES6中的模块功能主要由两个命令构成：export和import。
**export规定模块的对外接口，import用于输入其他模块提供的功能**，二者属于相辅相成、一一对应关系。
一、模块
模块可以理解为函数代码块的功能，是封装对象的属性和方法的javascript代码，它可以是某单个文件、变量或者函数。
模块实质上是对业务逻辑分离实现低耦合高内聚，也便于代码管理而不是所有功能代码堆叠在一起，模块真正的魔力所在是仅导出和导入你需要的绑定，而不是将所有的东西都放到一个文件。
在理想状态下我们只需要完成自己部分的核心业务逻辑代码，其他方面的依赖可以通过直接加载被人已经写好模块进行使用即可。
二、export 导出 命令
一个模块就是一个独立的文件，该文件内部的所有变量，外部无法获取。如果想从外部能够读取模块内部的某个变量，就必须使用export关键字输出该变量。分为以下几种情况：
（1）在需要导出的js文件中， 使用 export{} 导出需要导出的接口
```
let x = 100;
let y = [1,2,3,4,5];
let str = "asd123"
let fun1 = ()=>{
	console.log("fun1")
}
export{x,y,str,fun1}
```
 import和export是对应的：
```
import {x,y,str,fun1} from '文件目录';
```
（2）export导出接口的时候，可以使用as，改变要导出的接口的接口名称。让接口字段更加语义化。
```
//lib.js文件
let fn0 = function() {
    console.log("fn0");
};
let obj0 = {}
export { fn0 as foo, obj0 as bar};

//main.js文件
import {foo, bar} from "./lib";
foo();
console.log(bar);

```
（3）直接在export的地方定义导出的函数，或者变量：
```
export let foo = ()=> {
  console.log("fnFoo") ;
  return "foo"
},
bar = "s,tringBar";
```
```
import {foo, bar} from "./lib";
console.log(foo());
console.log(bar);
```
（4）export default导出
当不知道变量名时，可以使用export default导出。
```
export default "string";
```
这种匿名情况，import时可以为该匿名函数指定任意名字。
```
import defaultString from "./lib";
console.log(defaultString);
```
（5）export也能默认导出函数， 在import的时候， 名字可以自定义， 因为每一个模块的默认接口就一个：
```
//lib.js
let fn = () => "string";
export {fn as default};

//main.js
import defaultFn from "./lib";
console.log(defaultFn());
```
（6）使用通配符* ，对应的所有接口
如果只想导出部分接口， 只要把接口名字列出来,如果要导出对应文件的所有，可以使用*
```
export * from "./other";
```
三、import 导入 命令  
ES6导入的模块都是属于引用，每一个导入的js模块都是活的， 每一次访问该模块的变量或者函数都是最新的， 这个是原生ES6模块 与AMD和CMD的区别之一。
使用export命令定义了模块的对外接口以后，其他 JS 文件就可以通过import命令加载这个模块。
```
import {bar,foo, fn0, fn1} from "./lib";
console.log(bar+"_"+foo);
fn0();
fn1();
```
大括号里面的变量名，必须与被导入模块对外接口的名称相同。
想要输入的变量重新取一个名字，import命令要使用 as关键字，将输入的变量重命名。
```
import { formatFn as fn0 } from 'lib.js';
```
注：import后面的from指定模块文件的位置，可以是相对路径，也可以是绝对路径，.js后缀可以省略。

**四、ES6模块化的基本规则、特点**

1. 每一个模块只加载一次。 每一个JS只执行一次， 如果下次再去加载同目录下同文件，直接从内存中读取。 一个模块就是一个单例，或者说就是一个对象。
2. 每一个模块内声明的变量都是局部变量， 不会污染全局作用域。
3. 模块内部的变量或者函数可以通过export导出。
4. 一个模块可以导入别的模块。
