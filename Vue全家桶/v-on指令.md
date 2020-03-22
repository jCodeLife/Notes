v-on就是**用于绑定事件的**
例如 有个按钮，我想点击的时候执行一些操作
```
<div class="app">
	<button v-on:click="myclick">click me</button>
</div>	
```
注意：后面的值是一个方法，可以写成myclick()，如没有参数也可以写成myclick。另外这种事件对应的方法不是定义在data里面，而是定义在vue实例的methods里 
```
var app = new Vue({
	el:'.app',
	data:{
		
	},
	methods:{
		myclick:function(){
			console.log(111111);
		}
	}
});
```
v-on可以绑定多个事件
```
<div class="app">
	<button v-on="{mouseenter:onenter,mouseleave:leave}">click me</button>
</div>	
```
```
<div class="app">
	<button v-on:mouseenter='onenter' v-on:mouseleave='leave'>click me</button>
</div>	
```
```
<div class="app">
	<button v-on:mouseenter='onenter' v-on:mouseleave='leave' v-on:click="myclick">click me</button>
</div>	
```
```
<div class="app">
	<button v-on="{mouseenter:onenter,mouseleave:leave}" v-on:click="myclick">click me</button>
</div>	
```
当绑定多个事件时，需要传入一个对象，对象的键名就是事件名，对象的键值就是对应事件要执行的方法。注意在vue实例中方法一定要有，不然就报错。
```
var app = new Vue({
	el:'.app',
	data:{
		
	},
	methods:{
		myclick:function(){
			console.log("clicked");
		},
		onenter:function(){
			console.log("mouseented");
		},
		leave:function(){
			console.log("mouseleaved");
		}
	}
});
```
在绑定form表单中的提交事件时
```
<div class="app">
	<form v-on:submit='onSubmit($event)'>
		<!-- $event是vue里面的事件对象，vue能认识 -->
		<input type="text" >
		<button type="submit">提交</button>
	</form>
</div>	
```
```
var app = new Vue({
	el:'.app',
	data:{
		
	},
	methods:{
		onSubmit:function(e){
			e.preventDefault();
			//阻止浏览器的默认行为，因为在表单提交的时候，浏览器会默认发送一个get或者post请求到指定页面，刷新整个页面。
			console.log("onSubmited");
		}
	}
});
```
注意：
$event是vue里面的事件对象，vue能认识
在表单提交的时候，浏览器会默认发送一个get或者post请求到指定页面，刷新整个页面。阻止浏览器的默认行为，可以用事件对象e.preventDefault();

像上述form表单提交的这种浏览器默认事件，其实vue也想到了，它封装好了，只要在事件的后面添加一个.prevent修饰符，表示阻止默认事件。
```
<div class="app">
	<form v-on:submit.='onSubmit'>
		<input type="text" >
		<button type="submit">提交</button>
	</form>
</div>	
```
```
var app = new Vue({
	el:'.app',
	data:{
		
	},
	methods:{
		onSubmit:function(){
			console.log("onSubmited");
		}
	}
});
```
绑定事件中，除了prevent阻止默认事件，还有stop,表示停止冒泡事件
```
<div class="app">
	<div v-on:click.stop='onClick'>
	</div>
</div>	
```
另外,当我们绑定的事件是keyup、keypress、keydown键盘事件时，而且需要判断按下是回车时。这在以前我们需要判断事件对象的keyCode，虽然功能特别简单，但是每次去写还是特别麻烦。vue也想到了这点，只需要在键盘事件后面添加一个.enter修饰符即可。

```
<div class="app">
	<div v-on:keydown.enter='mykeydownFn'>
	</div>
</div>	
```
另外跟v-bind一样，v-on也有快捷方式：
**v-on:事件名**   可以简写为  **@事件名**，如

```
<div class="app">
	<div @keydown.enter='mykeydownFn'>
	</div>
</div>	
```
