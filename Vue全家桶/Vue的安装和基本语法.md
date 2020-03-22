#Vue安装
1.  cdn
```
<script src="https://cdn.bootcss.com/vue/2.6.8/vue.js"></script>
```
2. 下载到本地 
```
<script src="./js/vue.js"></script>
```
3.通过npm工具命令
先得安装npm，也很简单安装一下node即可。
```
npm i vue
```
#Vue的基本语法
 通过Vue通过new Vue()来构造Vue实例对象

HTML
```
<!DOCTYPE html>
<html>
<head>
	<title>demo</title>
</head>
<body>
	<div class="app">
		<span>你的名字是：{{name}}</span>
		<!-- 一旦出现{{}}这种形式的，vue就开始解析。vue就会把里面的东西当做类似js的语句来解析,也会解析一部分的js语句，注意并不是所有的js语句都能解析 -->
		<span>你的年龄是：{{age}}</span>
		<!-- <span>你的年龄是：{{sex}}</span> -->
		<!-- 如果范围在vue中没有定义的数据，会报错。 -->
		
	</div>
	
	<script src="https://cdn.bootcss.com/vue/2.6.8/vue.js"></script>
	<script src="../js/main.js"></script>
</body>
</html>
```
JS
```
//main.js
var app = new Vue({
	el:'.app',
	data:{
		name:'alice',
		age:22,
	}
});
```
注意：
1. 在HTML内，一旦出现{{}}这种形式的，vue就开始解析。vue就会把里面的东西当做类似js的语句来解析,也会解析一部分的js语句，注意并不是所有的js语句都能解析
2. 如果{{}}内的内容在vue中没有定义，程序会报错。 
3. 实例Vue是传入的对象中
-  el：表示element,是告诉vue它应该跟那个元素绑定。也就是生成的vue对象会产生一个域，这个域是作用在哪个元素上的。
- data：在vue中数据是放置在data里头的。
- data里面的属性名，如name，它会与HTML中该Vue实例所在域下的标签下的{{}}内的数据名对应。HTML显示的就是对应的键值。
- 那它是怎么知道html的的{{name}}就是这里的值呢。这其实就是Vue背后的一种默认机制。它就有这样的机制，data里面所有的数据都绑定到vue实例下。
- data里面可以添加很多数据，跟js一样，这其实就是js对象
- 当在控制台改变vue里面的值，如：app.name = 'Tom',页面上显示的名字也是Tom，我们发现vue里面的内容是直接跟内存中数据是绑定的。通常我们用原声js，它只是把数据放在内存中，我们必须调用浏览器的api（如DOMapi）才能改变，不会自动改变。这样可以提高开发效率和程序的性能。


可以在input输入框中动态绑定
```
<div class="app">
	<div>
		<input type="text" v-model="name">
		<span>你的名字是：{{name}}</span>
	</div>
	<div>
		<input type="text" v-model='age'>
		<span>你的年龄是：{{age}}</span>
	</div>
</div>
```
v-model并不是浏览器的原生属性，而是vue定义的属性，凡是这种在vue里面自定义的属性，我们把它叫做指令（directive）
同时这种指令有其对应的功能，这里v-model的功能就是将input里面的值指向哪里或者说是绑定到哪里。如这里绑定到data里的name或者age，而另外一边{{name}}和{{age}}里面的值也绑定在data里面，这其实就是双向绑定。 当输入的值变化是，页面也改变。

上面的例子有个不太好的点，当input没有输入时，对应的文字信息还是会出来。如果我们想当input没有值的时候，文字也没有，有两种方案：
1. v-show
显示指令，当对应值为真时显示元素，当值为false时隐藏元素。
```
<div class="app">
	<div>
		<input type="text" v-model="name"><br>
		<span v-show="name">你的名字是：{{name}}</span>
	</div>
	<div>
		<input type="text" v-model='age'><br>
		<span v-show="age">你的年龄是：{{age}}</span>
	</div>
</div>
```
2. v-if
判断指令，如果..
```
<div class="app">
	<div>
		<input type="text" v-model="name"><br>
		<span v-if="name">你的名字是：{{name}}</span>
	</div>
	<div>
		<input type="text" v-model='age'><br>
		<span v-if="age">你的年龄是：{{age}}</span>
	</div>
</div>
```
区别：
v-show：元素本身一直存在，只不过显不显示出来而已。要么显示要么display为none
二v-if:如果里面的值对应为false，元素就直接从dom中删除了。

