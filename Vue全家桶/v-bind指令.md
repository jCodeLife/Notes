v-bind就是**用于绑定数据和元素属性的**
```
var app = new Vue({
	el:'.app',
	data:{
		url:"https://www.baidu.com",
	}
});
```
```
<div class="app">
	<a v-bind:href="url">click me</a>
</div>	
```
注意：
v-bind后面是**：属性名=**，我的理解是表示绑定这个属性，绑定之后，对应的值要去vue的数据里面找。
当我们在控制台改变url时，对应也会变化。
相同的，我们还可以绑定图片src属性、超链接的class
```
var app = new Vue({
	el:'.app',
	data:{
		url:"https://www.baidu.com",
        imgsrc:"https://cn.vuejs.org/images/logo.png",
        class:"btn btn-default"
	}
});
```
```
<div class="app">
	<a v-bind:href="url" v-bind:class="klass">click me</a>
	<img v-bind:src="imgsrc">
</div>	
```
另外一种够可以传入一个对象，如下
对象的名active，表示要添加的类名，isActive是vue中的数据，表示在什么情况下添加该类名，对应为真才添加。
```
<div class="app">
	<a v-bind:class="{active:isActive}">click me</a>
</div>	
```
通常我们可以将**v-bind：**简写成**：**
```
<div class="app">
	<a :class="{active:isActive}">click me</a>
</div>	
```

