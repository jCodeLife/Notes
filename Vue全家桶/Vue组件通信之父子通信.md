web中的component其实就是一个自定义标签，背后有一些自定义功能。同样一个component在不同的场景下，它的表现不一定相同的。我们有时候想，能不能给component传一个参数，让里头的代码重用起来。如：
```
Vue.component('alert',{
	template:"#Alert",
	methods:{
		myAlert:function(){
			alert(111111);
		}
	}
});

new Vue({
	el:'#app',
});

```
```
<body>
<div id="app">
	<alert></alert>
</div>
<template id="Alert">
	<button @click="myAlert()">
			Clike me!
	</button>
</template>
<script src="vue.js"></script>
<script src="main.js"></script>
```
我想重用上面组件，比如弹出来的信息是可以根据传入的值不同而动态改变的。vue提供了这样的方式：
如根据传入组件的属性值不同，而有不同的弹出信息：
```
<div id="app">
    <alert msg="222222"></alert>
</div>
```
那在点击时触发的方法,alert就应该时动态的
```
Vue.component('alert',{
    template:"#Alert",
    methods:{
        myAlert:function(){
            alert(this.msg);
        }
    }
});
```
那怎么将html的自定义组件的属性msg的值，跟Vue组件中的this.msg关联或者绑定起来。Vue在组件中提供了一个可选项：**props**
props可以是一个数组，注意：数组里面的值要与html自定义组件里的属性对应，即**props存储的就是组件的相关属性**
如果在html中指定很多属性，在component的props中没有定义，那那些属性都是没有意义的。
记住：**必须在props传了对应属性，它才会去解析。**解析大概就是，让对应的属性等于对应的值，再this.属性名的时候就能得到相应传入的值，因为他们调的是同一个数据。
```
Vue.component('alert',{
	template:"#Alert",
	props:['msg'],
	methods:{
		myAlert:function(){
			alert(this.msg);
		}
	}
});

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
	<alert msg="2222222222"></alert>
</div>
<template id="Alert">
	<button @click="myAlert()">
			Clike me!
	</button>
</template>
<script src="vue.js"></script>
<script src="main.js"></script>
</body>
</html>
```
事实上上例：this.msg就能找到props里的msg，而props里的数据是跟html中的对应组件的属性关联的（可以理解为vue的机制），所以他们调用的是同一个数据。

有的时候我们需要再页面显示一个用户的链接，链接不能写死，而是根据用户名不同而变化的。不可像下面那样一条条写这样的链接
```
<div id="app">
	<a href="/user/alice">alice</a>
</div>
```
那我们可以将这个链接封装到一个组件里。
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
	<user username="tom"></user>
	
</div>
<template id="user">
	<a :href='"/user/" + username'>@{{username}}</a>
</template>

<script src="vue.js"></script>
<script src="main.js"></script>
<script type="text/javascript">	
	Vue.component('user',{
		template:'#user',
		props:['username'],
	});


	new Vue({
		el:'#app',
	});

</script>
</body>
</html>
```
这样绑定的链接会根据传入的属性值不同，而生成不同的链接。即页面显示的名字是动态变化的，链接也是动态变化的。

其实以上都是组件的传参，通过自定义属性传参，这个属性是从外部往内部传值，也就是父级组件要跟子级组件通信，自定义属性就是一个沟通的桥梁。
