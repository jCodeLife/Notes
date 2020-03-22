vue本身提供了很多的指令，如v-model、v-for、v-if、v-on、v-....
但是有的时候，我们可能需要特殊的一些指令来实现我们特定的功能，在vue中这些指令我们可以自己定义。

自定义指令看成是自定义属性吧，这样更好理解一点。当我们定义指令或者属性后，就可以运用到我们想运用的元素上，并且指令和我们的组件一样，也是可以重用的。组件是一个一个的组件，指令可以放在组件里头，丰富组件的功能和特性。

自定义指令的定义：
使用Vue.directive("指令名",fn(){});
注意：
第一个参数是指令的名称；
第二个参数是一个function,里面是定义指令的相关功能。
需要注意的是这个功能函数中，第一个参数是该指令所在的整个元素，vue会自动传进来，在函数体里面可以使用原生的API去调用它，也可以使用jQuery等第三方库来调用。第二个参数就是这个指令对应的对象，里面包含了指令的基本信息，通过这个参数也可以得到指令的信息如直接.value，表示指令在html中传入的值。

```
<!DOCTYPE html>
<html>
<head>
	<title>demo</title>
	<style type="text/css">
		.card{
			height: 100px;
			width:200px;
			border: 1px solid red;
			overflow: hidden;
			font-size: 10px;
			padding: 10px;
			margin-top: 10px;
		}
	</style>
</head>
<body>
	<div class="app">
		<div class="card" v-pin="card1.isPind">
			<button @click="card1.isPind=!card1.isPind">定住</button>
			Vue 是一套用于构建用户界面的渐进式框架。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。
		</div>
		<div class="card" v-pin='card2.isPind'>
			<button @click="card2.isPind=!card2.isPind">可以点我试试</button>
			Angular 是一个开发平台。它能帮你更轻松的构建 Web 应用。Angular 集声明式模板、依赖注入、端到端工具和一些最佳实践于一身，为你解决开发方面的各种挑战。
		</div>
		<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
	</div>
	
<script src="https://cdn.bootcss.com/vue/2.6.10/vue.js"></script>
<script type="text/javascript">
	Vue.directive('pin',function(el,obj){
		//console.log(el);//说明第一个参数是表示：指令所在的整个元素及内容，有多少个绑定的元素就打印多少个
		//console.log(obj);//返回object对象，里面包含了这个元素的基本信息，有多少个绑定的元素就打印多少个
		//console.log(obj.value);//这个对象里面有个value属性，它的值跟html元素里面的对应指令的值对应。
		var pinned = obj.value;
		if (pinned) {
			el.style.position = 'fixed';
			el.style.top="20px";
			el.style.left="20px";
		}else{
			el.style.position = 'static';
		}
	});

	new Vue({
		el:'.app',
		data:{
			card1:{
				isPind:false
			},
			card2:{
				isPind:false
			},
		},
	});
</script>
</body>
</html>
```
#自定义指令-配置传参及修饰符
主要还是通过在定义指令的时候，传入的第二个参数-功能函数里面的参数来获取和修改。
功能函数中的第二个参数除了可以获得上面的：obj.value----指令的值
还能获得指令的参数obj.arg
还能获得指令的修饰符obj.modifiers
通过传达参数和修饰符来更改元素的相关样式。
1. 添加修饰符
div class="card" v-pin.right="card1.isPind">
通过obj.modifiers遍历得到每个修饰符，然后执行相关操作。
```
<!DOCTYPE html>
<html>
<head>
	<title>demo</title>
	<style type="text/css">
		.card{
			height: 100px;
			width:200px;
			border: 1px solid red;
			overflow: hidden;
			font-size: 10px;
			padding: 10px;
			margin-top: 10px;
		}
	</style>
</head>
<body>
	<div class="app">
		<div class="card" v-pin.right="card1.isPind">
			<button @click="card1.isPind=!card1.isPind">定住</button>
			Vue 是一套用于构建用户界面的渐进式框架。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。
		</div>
		<div class="card" v-pin.bottom='card2.isPind'>
			<button @click="card2.isPind=!card2.isPind">可以点我试试</button>
			Angular 是一个开发平台。它能帮你更轻松的构建 Web 应用。Angular 集声明式模板、依赖注入、端到端工具和一些最佳实践于一身，为你解决开发方面的各种挑战。
		</div>
		<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
	</div>
	
<script src="https://cdn.bootcss.com/vue/2.6.10/vue.js"></script>
<script type="text/javascript">
	Vue.directive('pin',function(el,obj){
		var pinned = obj.value;
		var position = obj.modifiers;
		if (pinned) {
			el.style.position = 'fixed';
			for(var val in position){				
				if (position[val]) {
					el.style[val]='10px';					
				}
			}
		
	
		}else{
			el.style.position = 'static';
		}
	});

	new Vue({
		el:'.app',
		data:{
			card1:{
				isPind:false
			},
			card2:{
				isPind:false
			},
		},
	});
</script>
</body>
</html>
```
1 添加指令的参数
通过在指令后面加：参数名
<div class="card" v-pin:warning.right="card1.isPind">
通过obj.arg获得参数
```
<!DOCTYPE html>
<html>
<head>
	<title>demo</title>
	<style type="text/css">
		.card{
			height: 100px;
			width:200px;
			border: 1px solid red;
			overflow: hidden;
			font-size: 10px;
			padding: 10px;
			margin-top: 10px;
		}
	</style>
</head>
<body>
	<div class="app">
		<div class="card" v-pin:warning.right="card1.isPind">
			<button @click="card1.isPind=!card1.isPind">定住</button>
			Vue 是一套用于构建用户界面的渐进式框架。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。
		</div>
		<div class="card" v-pin.bottom='card2.isPind'>
			<button @click="card2.isPind=!card2.isPind">可以点我试试</button>
			Angular 是一个开发平台。它能帮你更轻松的构建 Web 应用。Angular 集声明式模板、依赖注入、端到端工具和一些最佳实践于一身，为你解决开发方面的各种挑战。
		</div>
		<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
	</div>
	
<script src="https://cdn.bootcss.com/vue/2.6.10/vue.js"></script>
<script type="text/javascript">
	Vue.directive('pin',function(el,obj){
		var pinned = obj.value;
		var position = obj.modifiers;
		var args = obj.arg;

		if (pinned) {
			el.style.position = 'fixed';
			if (args=="warning") {
				el.style.backgroundColor="red";
			}

			for(var val in position){				
				if (position[val]) {
					el.style[val]='10px';					
				}
			}
		
	
		}else{
			el.style.position = 'static';
			el.style.backgroundColor="";
		}
	});

	new Vue({
		el:'.app',
		data:{
			card1:{
				isPind:false
			},
			card2:{
				isPind:false
			},
		},
	});
</script>
</body>
</html>
```
