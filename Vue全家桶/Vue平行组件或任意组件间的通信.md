任意间的通信需要时借助事件调渡器var Event = new Vue()，
大概思路是：
**通过一个组件触发一个事件并传递通信相关的数据，在另外一个组件里监听该事件的触发并处理接收相关数据。**
注意，调度器必须写在mounted之前，其实就是调度器声明赋值要写在调度器使用前。
```
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title>demo</title>
</head>
<body>
	<div id="app">
		<alice></alice>
		<br><br>
		<tom></tom>
	</div>

<script src="vue.js"></script>
<script type="text/javascript">	
	var Event = new Vue();
	//使用一个事件的调渡器来将两个组件的数据联系在一起，如上两个数据i_say和aliceSay	

	// 任意组件间的通信的核心是要有一个中间的事件调度器，用来关联两个数据。在一个组件中通过$emit来触发事件，并传递数据，我们在另外的一个组件中通过$on来监听事件并接受数据。
	Vue.component('alice',{
		template:`<div>
				My name is alice:<br>
				<input type="text" v-model="i_say" @keyup="onChanged"><br>
				I say：{{i_say}}
			</div>`,
		data:function(){
			return {
				i_say:'',
			}
		},
		methods:{
			onChanged:function(){
				Event.$emit('alice-say-something',this.i_say);//触发一个事件，并传递数据。可以在其他组件监听该事件
			}
		}
	});
	Vue.component('tom',{

		template:`<div>
				My name is tom:<br>
				alice say：{{aliceSay}}
			</div>`,
		data:function(){
			return {
				aliceSay:'',
			}
		},
		// mounted表示组件挂载完毕的时候，初始化完毕是。可以在这监听看看其他组件说了什么。
		// mounted也叫生命周期的钩子，可以理解为生命周期里的一些关键节点，就像关键帧 里程碑一样。
		//
		mounted:function(){
			var temp = this;
			Event.$on('alice-say-something',function(data){//注意是事件的调度器来监听
				console.log(111);
				temp.aliceSay = data;
			});//监听其他组件的事件
		}
	});
	var vm = new Vue({
		el:'#app'
	});
	
</script>
</body>
</html>
```
