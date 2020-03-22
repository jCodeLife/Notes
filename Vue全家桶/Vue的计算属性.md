有时候我们可能需要在{{}}里进行一些计算在展示出来数据：
```
<div class="app">
	<table border="1">
		<thead>
			<th>学科</th>
			<th>分数</th>
		</thead>
		<tbody>
			<tr>
				<td>数学</td>
				<td><input type="text" v-model="Math"></td>
			</tr>
			<tr>
				<td>英语</td>
				<td><input type="text" v-model="English"></td>
			</tr>
			<tr>
				<td>化学</td>
				<td><input type="text" v-model="chemistry"></td>
			</tr>
			<tr>
				<td>总分</td>
				<td>{{Math + English + chemistry}}</td>
			</tr>
			<tr>
				<td>平均分</td>
				<td>{{(Math + English + chemistry)/3}}</td>
			</tr>
		</tbody>
	</table>

</div>
```
```
var app = new Vue({
	el:'.app',
	data:{
		Math:88,
		English:77,
		chemistry:99,
	}
});
```
虽然能解决问题，但是特别不不清晰。
这种情况下，vue给我们提供了一个特别好的解决方案：**计算属性**，
我们可以把这些计算的过程写到一个计算属性中去，然后让它动态的计算就可以了。
计算属性是vue实例中的选项：**computed**
通常里面每一个都是计算相关函数，返回最后计算出来的值。
```
<body>
<div class="app">
	<table border="1">
		<thead>
			<th>学科</th>
			<th>成绩</th>
		</thead>
		<tbody>
			<tr>
				<td>数学</td>
				<td><input type="text" v-model.number="Math"></td>
			</tr>
			<tr>
				<td>英语</td>
				<td><input type="text" v-model.number="English"></td>
			</tr>
			<tr>
				<td>化学</td>
				<td><input type="text" v-model.number="chemistry"></td>
			</tr>
			<tr>
				<td>总分</td>
				<td>{{sum}}</td>
			</tr>
			<tr>
				<td>平均分</td>
				<td>{{average}}</td>
			</tr>

		</tbody>
	</table>
</div>
<script src="jquery-3.3.1.js"></script>
<script src="vue.js"></script>
<script src="main.js"></script>
</body>
```
```
var vm = new Vue({
	el:'.app',
	data:{
		Math:88,
		English: 77,
		chemistry:99,
	},
	computed:{
		sum:function(){
			return this.Math+ this.English+this.chemistry;
		},
		average:function(){
			return Math.round(this.sum/3);
		}
	}
});
```
如上，**计算属性一般就是用来通过其他的数据算出一个新数据，而且它有一个好处就是它把新的数据缓存下来了，当其他的数据没有发生改变，它调用的是缓存的数据，这就极大的提高了我们程序的性能**。不然可以直接用用methods了，如果写在methods里，每次都会重新计算。所有用计算属性比较好，因为有缓存。
