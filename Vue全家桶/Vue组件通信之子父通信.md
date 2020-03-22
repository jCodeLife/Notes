子父通信
子组件跟父级组件通信是通过事件的方式来通信。
使用this.$emit('show',{})不仅触发了事件还传递了数据。
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
	<father></father>	
</div>


<script src="vue.js"></script>
<script type="text/javascript">	
	Vue.component('father',{
		template:`
		<div>
			<child @show="showfn"></child>
			<div v-if="show">成绩：88</div>
		</div>`,
		data:function(){
			return {
				show:false
			}
		},
		methods:{
			showfn:function(data){
				this.show = true;
				console.log(data);//data是在用$emit触发事件时传递的数据。
			}
		}
	});
	Vue.component('child',{
		template:'<button @click="onClick">这里是子组件</button>',
		methods:{
			onClick:function(){
				this.$emit('show',{a:1,b:2,c:3});//触发事件
			}
		}
	});
	new Vue({
		el:'#app'
	});
</script>
</body>
</html>
```
1. 首先定义两个组件，父组件father和子组件child;
2. 父组件包含子组件；
2. 在子组件触发相关事件，在事件方法里使用$emit('事件名',{要传递的数据})来触发其他事件，这个使事件是在父组件中的子组件内监听，然后在父级组件调用触发该事件的对应的方法。
简单的说就是，子组件触发相关事件传递给父级组件，父级组件进行相关操作。
