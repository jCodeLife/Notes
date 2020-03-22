有的时候，有些数据是半动态的，即数据的一部分是变化的，一部分是固定不变或者也可能能动态，但是这种动态是相对比较少的。那么我可以使用过滤器来对数据进行一步优化过滤。在vue中提供了Vue.filter('flterName',fn)来定义一个过滤器，过滤器可以在HTML代码中使用，如对动态拿到的数据进行过滤，
一个简单例子：
```
<body>
	<div class="demo">
		<input type="text" v-model="price">
		{{price | currency('$')}}<!--通过‘|’管道符来过滤前面的price-->
	</div>
<script src="https://cdn.bootcss.com/vue/2.6.10/vue.js"></script>
<script type="text/javascript">
	Vue.filter('currency',function(val,unit){//定义过滤器，并定义功能。
		val =  val || 0;
		unit = unit || '元';
		return val + unit;
	});
	new Vue({
		el:'.demo',
		data:{
			price:'',
		}
	});
</script>
</body>
```
1.定义过滤器
第一个参数是过滤器的名字
第二个参数是过滤器的功能函数。如果不定义，vue也不知道你这个字符串是什么，有什么作用。
2. 过滤器功能函数
第一个参数是传入的要过滤数据，即原数据。
第二个参数开始就是html调用过滤器的时候传入的参数。

再来看一个例子：长度的简单换算
```
<body>
	<div class="demo">
		<input type="number" v-model="length">
		{{length}}mm => {{length | meter}}
	</div>
<script src="https://cdn.bootcss.com/vue/2.6.10/vue.js"></script>
<script type="text/javascript">
	Vue.filter('meter',function(val,unit){	
		val = val/1000 || 0;
		if (val) {
			unit = "m";		
			return val + unit;
		}
		return;			
	});
	new Vue({
		el:'.demo',
		data:{
			price:'',
			length:'',
		}
	});
</script>
</body>
```

注意：
filter不会修改原始数据，它的作用是过滤数据，给人的感觉就像解决最后一公里的问题，就是最后达到用户界面前的最后一步 可能需要做一些数据格式上的修改，让用户更舒服，其实就是一个优化用户体验的过程。
如果一个filter内部特别复杂，就可以考虑，看看要不要把它写成一个计算属性，因为计算属性本身带有缓存，而且可重用性特别强，而filter一般是做一些简单的事情。
