v-for作用：专门用于迭代的指令
**我们可以用 v-for 指令基于一个数组来渲染一个列表。
v-for 指令需要使用 item in items 形式的特殊语法，其中 items 是源数据数组，而 item 则是被迭代的数组元素的别名。**
1. 迭代字符串数组
```
var app = new Vue({
	el:'.app',
	data:{
		foodList:['apple','banana','orange']
	}
});
```
```
//html
<!DOCTYPE html>
<html>
<head>
	<title>demo</title>
</head>
<body>
	<div class="app">
		<ul>
			<li v-for="food in foodList">{{food}}</li>
		</ul>
	</div>	
	<script src="https://cdn.bootcss.com/vue/2.6.8/vue.js"></script>
	<script src="../js/main.js"></script>
</body>
</html>
```
单单迭代字符串的情况还是比较少，一般迭代对象组成的数组
2. 迭代对象数组
```
var app = new Vue({
	el:'.app',
	data:{
		foodList:[{
			name:'apple',
			price:8,
		},{
			name:'banana',
			price:3,
		},{
			name:"orange",
			price:12,
		}]
	}
});
```
这样的数据结构更清晰，里面一条一条的数据，每一条数据都包含子一个对象中。
在输出显示的时候，可以直接.的形式来拿到对应的属性
```
<div class="app">
	<ul>
		<li v-for="food in foodList">{{food.name}}:{{food.price}}</li>
	</ul>
</div>	
```
另外，{{}}双花括号里面的值是可以运算的。比如有个折扣
```
var app = new Vue({
	el:'.app',
	data:{
		foodList:[
		{
			name:'apple',
			price:8,
			discount:.8
		},
		{
			name:'banana',
			price:3,
			discount:.9
		},
		{
			name:"orange",
			price:10,
			discount:.7
		}
		]
	}
});
```
花括号里面可以进行运算
```
<div class="app">
	<ul>
		<li v-for="food in foodList">{{food.name}}:{{food.price * food.discount}}元</li>
	</ul>
</div>	
```
避免当没有折扣的时候显示NAN
```
<div class="app">
	<ul>
		<li v-for="food in foodList">{{food.name}}:{{food.discount?food.price * food.discount:food.price}}元</li>
	</ul>
</div>	
```
（但是这样写特别臃肿，不够语义化，以后可以使用计算属性来写。）
也可以动态插入
```
app.foodList.push({name:'pear',price:20,discount:.7});
```
对应也是动态的页面展示。
也就是说v-for也是一直在监视着数据的变化，当数据发生改变的时候，页面也会跟着改变。所以我们只要结构样式写好，只需要动数据就好了，其他东西不用管。

**你也可以用 of 替代 in 作为分隔符，因为它更接近 JavaScript 迭代器的语法**
```
<div v-for="food of foodList"></div>
```
3.   迭代单个对象的属性  
```
//main.js
var app = new Vue({
	el:'.app',
	data:{
		object:{
			title:"How to do Lists in Vue",
			author:"Alice",
			publishedAt:"2019-6-11"
		}
	}
});
```
迭代对象属性
```
<ul>
  <li v-for = "val in object">{{val}}</li>
</ul>
```
![迭代单个对象](https://upload-images.jianshu.io/upload_images/17785871-9ccfc70eae4a56c0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

提供第二个的参数为 property 名称 (也就是键名)：
```
<div class="app">
	<ul>
		<li v-for="(value, name) in object">{{ name }}: {{ value }}</li>
	</ul>
</div>
```
![提供第二个参数，接收键名](https://upload-images.jianshu.io/upload_images/17785871-eb0e788629edb6ce.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

还可以用第三个参数作为索引：
```
<div class="app">
	<ul>
		<li v-for="(value, name,index) in object">{{ index }}. {{ name }}: {{ value }}</li>
	</ul>
</div>	
```
![键值、键名和索引](https://upload-images.jianshu.io/upload_images/17785871-2b5858f190f15f38.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)






