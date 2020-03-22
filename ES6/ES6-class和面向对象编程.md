在ES5中，我们经常使用方法或者对象去模拟类的使用，并基于原型实现继承，虽然可以实现功能，但是代码并不优雅，很多人还是倾向于用 class 来组织代码，很多类库、框架创造了自己的 API 来实现 class 的功能。
ES6 时代终于有了 class （类）语法，能让我们可以用更简明的语法实现继承，也使代码的可读性变得更高，同时为以后的JavaScript语言版本添加更多的面向对象特征打下基础。
一、 类的定义
1. ES5使用函数模拟类
```
function Person( name , age ) {
    this.name = name;
    this.age = age;
}
Person.prototype.say = function(){
    return '我叫' + this.name + ',今年' + this.age + '岁';
}
var  p = new Person('xiaoming',33);  // Person {name: "xiaoming", age: 33}
p.say();
```
使用ES5语法定义了一个Person类，该类有name age food三个属性和一个原型eat方法。

2.ES class定义类
```
class Person{
	constructor(name,age){
		this.name = name;
		this.age = age;
	}
	say(){
		return '我叫' + this.name + ',今年' + this.age + '岁';
	}
}
var stu = new Person("xiaoming",22);
p.say();
```
上面代码定义了一个同样的Person类，constructor方法就是构造方法，而this关键字则代表实例对象;
注：虽然ES6引入了class关键字，但并没有真的引入类这个概念，通过class定义的仍然是函数，数据类型中也没有class类型。
```
console.log(typeof Person);//还是'function'
```
所以说，class仅仅是通过更简单直观的语法去实现原型链继承。这种对语言功能没有影响、但是给程序员带来方便的新语法，被称为语法糖。

二、类的传参
在类的参数传递中,我们在constructor( )进行传参，传递参数后可以直接使用this.xxx进行调用。
```
class Person{
	constructor(x,y){
		this.x = x;
		this.y = y;
	}
	add(){
		return this.a + this.b;
	}
}
let stu = new Person(11,22);
stu.add();//11+22=33
```
用constructor来传递参数，然后用了一个add方法，把参数相加。

三、静态方法
1. 使用函数模拟类时，通过函数名.静态方法名，来定义静态方法：
```
function Person(name,age){
	this.name = name;
	this.age = age;
	Person.say = function(){
		return "I can say!"
	}
}
Person.say();//I can say！
var student = new Person("xiaoming",11);
student.say();//报错
```
静态方法是不需要实例化，可以通过类名直接调用，注意的是静态方法不会继承到类实例中，因此静态方法经常用来作为工具函数。比如我们经常用的Math.random()。
2. 在ES6 class类定义中，可以使用static关键字定义静态方法：
```
class A{
	constructor(){};
	static say(){
		console.log("I can say!");
	}
}
A.say();//I can say
var a = new A();
a.say()//error
```
跟之前一样，通过类名直接调用，不会继承到类实例中。
static关键字是ES6的另一个语法糖，static 使静态方法声明也成为了一个一等公民。

四、封装和继承
1. ES6之前子类对象是通过使用原型来实现继承父类，子类函数和父类函数共享原型的形式来实现：
```
function Person(name,age){
	this.name = name;
	this.age = age;
}
function father(name,age,firstname,lastname){
	Person.call(this,name,age);//通过call来继承父类的方法来实现自己的功能
	this.lastname = lastname;
	this.firstname = firstname;
}
console.log(new father('zhangsan',11,'zhang','san'));
//father {name: "zhangsan", age: 11, lastname: "san", firstname: "zhang"}
function son(name,age,firstname,lastname){
	father.call(this,name,age,firstname,lastname);
};
son.prototype = Object.create(father.prototype);
son.constructor = son;
console.log(new son('zhangsi',5,'zhang','si'));
//son {name: "zhangsi", age: 5, lastname: "si", firstname: "zhang"}
```
2. ES6中新的extends关键字解决了这个麻烦问题：
```
语法：class son extends father{}
```
下面定义了一个Child类，该类通过extends关键字，继承了Parent类的所有属性和方法。
```
class Parent{
	constructor(firstname,lastname){
		this.firstname = firstname;
		this.lastname = lastname;
	}
}
class Child extends Parent{
	constructor (firstname,lastname,name){
		super(firstname,lastname);
		this.name = name;
	}
	say(){
		console.log("I can say!")
	}
}
console.log(new Child("蒙奇","D","路飞"));
//Child {firstname: "蒙奇", lastname: "D", name: "路飞"}
```
3. super关键字
super表示超，超类，父类。既可以当作函数，也可以当作对象使用。
（1）super作为函数调用，代表父类的构造函数。
注意，ES6中规定，子类的构造函数必须执行一次super函数。格式：
```
class Parent{}
class Child extends Parent{
	constructor (){
		super();
		// ...
	}
	// ...
}  
```
```
class Parent{}
class Child extends Parent{
	constructor (){
		// super();  如果调用super,程序会报错Uncaught ReferenceError: this is not defined
		// ...
	}
	// ...
}
new Child();
```
注意，super虽然代表父类中的构造函数，但是返回的是子类的实例，即super内部的this指的是子类Child，在这种情况下，super()相当于Parent.prototype.constructor.call(this)。
（2）super作为对象，代表父类的原型对象。
```
class Parent{
	constructor(firstname,lastname,age){
		this.firstname = firstname;
		this.lastname = lastname;
		this.age = age;
	}
	say(){
		console.log("I can say.");
	}
}
class Child extends Parent{
	constructor (firstname,lastname,age,score){
		super(firstname,lastname,age); //super在这里代表父类的构造函数 
		this.score = score;
		super.say();//super在这里代表父类的原型对象，可以调用父类的方法
	}
	
}

console.log(new Child("蒙奇","路飞",18,100));
// I can say.
// {firstname: "蒙奇", lastname: "路飞", age: 18, score: 100}
```
使用extends关键字实现继承，那么子类中可以通过super关键字调用父类的东西
（3）4.3 getter（取值）、 setter（存值）
与 ES5 一样，在“类”的内部可以使用get和set，对某个属性设置存值函数和取值函数，拦截该属性的存取行为。
```
class Parent{
	constructor(){}
	get firstname(){
		return "D.";
	}
	set lastname(value){
		console.log('我的名是：' + value);
	}
}

let p = new Parent();
console.log(p.firstname);//D.
console.log(p.lastname = "路飞")	;
//我的名是：路飞
//路飞

```
