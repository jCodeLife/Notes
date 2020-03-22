如果把一段经常用的东西封装成一个组件，那么就可以对组件扩充，将组件写的更加强大。当用的时候就只需要写一对标签就可以了，其背后的具体逻辑有多复杂，用的时候根本不用管。这就是vue组件的好处。而且在vue里面组件的结构封装的特别好，这就意味着有很好的可维护性。所有vue组件既有可重用性又有可维护性。

根据组件定义的域不同，可以分为全局组件和局部组件。定义在全局里的组件叫全局组件，定义在局部域的脚局部组件
#全局组件
1. 定义全局组件
1.1 使用Vue.component表示定义组件，
第一个参数:表示组件在vue里面的名字，
第二个参数{}:表示组件的内容，组件的内容里，一些选项，如：
	（1）template表示组件模板，写的就是html代码的字符串。
	（2）methods表示组件里的方法，
```
Vue.component('alert',{
	template:"<button @click='onClick'>clicke me</button>",
	methods:{
		onClick:function(){
			alert('my first conponent!');
		}
	}
});
```

1.2 给组件一个域
定义了组件后，需要给组件一个域，不然component不知道自己要在哪里。这个域是就是我们常常写的new Vue();
```
new Vue({
	el:'#app',
});
```
html中：
```
<div id="app">
	<alert></alert>
	<alert></alert>
</div>
```
定义好组件并设置域后，就是可以在页面中放很多很多标签，相同的标签功能都是一模一样。
如上在页面中仅仅只是写了标签，甚至可以没什么内容，但是它背后的功能，还不能小瞧，它取决于想不想把它往强大里写。 
2. 多域的情况
在js中定义多个域
```
Vue.component('alert',{
	template:"<button @click='onClick'>clicke me</button>",
	methods:{
		onClick:function(){
			alert('my first conponent!');
		}
	}
});

new Vue({
	el:'#app1',
});
new Vue({
	el:'#app2',
});
```
域两个域对应的html标签内放入自定义全局组件
```
<div id="app1">
	<alert></alert>
</div>
<div id="app2">
	<alert></alert>
</div>
```
发现：使用Vue.component()多定义的组件，对下面定义的所欲域都是可见的。但是如果我有很多的全局component，这些component都是对所有域可见的，这种感觉就像是window下的全局变量，给人的感觉特别不踏实。
有的时候，我们很确切的知道一个component只能在那一个域里面用，那么就需要定义一个局部的component
#局部组件
1. 定义局部组件
在特定的域中使用选项**components**定义局部组件：
跟全局组件和相似，只不过它是在特定域中写个**components**。
注意：带s的，其实我觉得也很好理解，全局每次定义的是一个全局组件，局部可以定义多个局部组件，所有是复数conmponents

```
new Vue({
	el:'#app1',
	components:{
		alert:{
			template:"<button @click='onClick'>clicke me</button>",
			methods:{
				onClick:function(){
					alert('my first conponent!');
				}
			}
		}
	}
});
new Vue({
	el:'#app2',
});
```
上述情况，在#app1定义的局部组件，如果对应html的元素内（#app1的）加这个组件时可以的。如果在其他域，如这#app2中是不能添加这个组件的，因为该组件时局部组件，只能在#app1里使，
即**在对应域中定义的组件只能限制在该域中**，所以局部限制在指定的局部域，全局组件全局可见。一般全局组件比较少。

我们一般可以将组件的内容功能封装出来，让结构更加清晰,还可以方便给其他一些域使用该组件功能。
```
let Alert = {
	template:"<button @click='onClick'>clicke me</button>",
	methods:{
		onClick:function(){
			alert('my first conponent!');
		}
	}
}

new Vue({
	el:'#app',
	components:{
		alert:Alert,
	}
});
```
#配置组件
```
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title>demo</title>
	<link rel="stylesheet" type="text/css" href="main.css">
</head>
<body>
<div id="app">
	<like></like>
</div>
<script src="jquery-3.3.1.js"></script>
<script src="vue.js"></script>
<script src="main.js"></script>
</body>
</html>
```
```
.like{
	background-color:pink;
}
```
```
Vue.component('like',{
	template:`
		<button @click="toggleLike" :class="{like:liked}">
			赞{{like_count}}
		</button>`,
		
	data:function(){
		return {
			like_count:10,
			liked:false,//用来判断是否点赞，初始false
		}
	},

	methods:{
		//定义点击触发的事件
		toggleLike:function(){
			if (!this.liked) {//如果当前没有点赞,注意访问当前Vue实例中的数据，可用直接用this.数据名
				this.like_count++;
				this.liked = ! this.liked;
			}else{
				this.like_count--;
				this.liked = ! this.liked;
			}
		}
	}
});

//2 给组件一个生存的域
new Vue({
	el:'#app',
});

```
配置like组件的过程中：
0. 通过Vue.component("组件名",{选项1，选项2...})来定义组件
1. template选项:配置组件模板，其实就一些可视化的内容，给用户看
2. data选项：配置组件数据相关
注意：这个data跟域(Vus实例)中的data不同，这里全局的data不是对象，而是个function,因为我们这做的个组件，这个组件每用一次，它都会新实例出来一个对象，这个新实例对象就有一些新的数据，这个data function就是指定我们怎么去生成这写数据。这里return出来想要的数据。
3. methods选项：定义功能函数
4. template中可以想正常元素一样绑定事件和绑定元素，如 :class="{like:liked}，表示通过v-bind来绑定一个like类，当liked为true时，显示这个类，否则不显示。

另外由于模板有些比较大也比较长，可以用ES6的反引号``，也可以写在HTML中，通过<template id=""></template>标签，那在Vue中的template的值只需要填写ID选择器就行。如：
```
Vue.component('like',{

	template:'#like-tpl',
	data:function(){
		return {
			like_count:10,
			liked:false,
		}
	},
	methods:{

		toggleLike:function(){
			if (!this.liked) {
				this.like_count++;
				this.liked = ! this.liked;
			}else{
				this.like_count--;
				this.liked = ! this.liked;
			}
		}
	}
});

//2 给组件一个生存的域
new Vue({
	el:'#app',
});

```
```
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title>demo</title>
	<link rel="stylesheet" type="text/css" href="main.css">
</head>
<body>
<div id="app">
	<like></like>
</div>
<template id="like-tpl">
	<button @click="toggleLike" :class="{like:liked}">
			赞{{like_count}}
	</button>
</template>
<script src="jquery-3.3.1.js"></script>
<script src="vue.js"></script>
<script src="main.js"></script>
</body>
</html>
```

