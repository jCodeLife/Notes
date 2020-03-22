用来绑定数据和元素value值，实现双向绑定。
当元素的值改变的时候，数据也改变，反过来，当数据发生改变，元素的值也改变。
在大部分情况下，所有用户的输入值都要通过v-model,一来好用，二来安全，而且功能也很强大。
```
<div class="app">
	<input type="text" v-model="name">
	{{name}}
</div>
```
```
var app = new Vue({
	el:'.app',
	data:{
		name:'Alice'
	}
});
```
####v-model的修饰符：
- lazy
懒惰，表示惰性更新，不会立马更新。
事实上它是触发了一个change事件。
好处：当用户输入完了才绑定，才会显示表单验证的结果，不管正确还是错误。但在用户输入的过程中，不去打扰他。另外性能也有一点点的提高（不过很小，可以忽略不计）
```
<div class="app">
    <input type="text" v-model.lazy="name">
    {{name}}
</div>
```
- trim
修剪; 切去，割掉，这里表示：去掉前后两端的所有空格
```
<div class="app">
    <input type="text" v-model.trim="name">
    {{name}}
</div>
```
- number
一般用于年龄、价钱等可以用数字来表示的类型
```
<div class="app">
    <input type="text" v-model.number="age">
    {{age}}
</div>
```
在通常情况下，如果没有number，用户输入的是数字，但是也是字符串的数字。如果这里填了修饰符 v-model.number那么得到就是number类型的数字了，不用再转换了。

v-model除了能在input 的type为text输入框中使用，还能在其他地方使用。

#v-model在不同input类型以及在其他元素上的使用
###1.除了在<input type="text">以外，还能在input元素为其他类型上使用
#####1.1  在input元素 类型为radio上使用(单选框)
<input type="radio">
之前
```
<div class="app">
	<label>
		男
		<input type="radio" name="sex" value="male">
	</label>
	<label>
		女
		<input type="radio" name="sex" value="famale">
	</label>
</div>
```
现在使用v-model

```
<div class="app">
	<label>
		男
		<input type="radio" v-model="sex" value="male">
	</label>
	<label>
		女
		<input type="radio" v-model="sex" value="famale">
	</label>
	{{sex}}
</div>
```
```
//main.js
var app = new Vue({
	el:'.app',
	data:{
		sex:'',
	}
});
```
#####1.2在input元素 类型为checkbox上使用(复选框)
```
<div class="app">
	你喜欢男的还女的：<br>
	<label>
		男
		<input type="checkbox" v-model="sex" value="male">
	</label>
	<label>
		女
		<input type="checkbox" v-model="sex" value="famale">
	</label><br>
	{{sex}}
</div>
```
```
var app = new Vue({
	el:'.app',
	data:{
		sex:['male'],
	}
});
```
###2. v-model在textarea中的使用(多行文本)
多行文本<textarea>
其实多行文本，跟单行文本的使用没有什么区别，只不过一个多行一个单行，使用是一样的。
```
<div class="app">
	<textarea v-model="article"></textarea>
</div>
```
```
var app = new Vue({
	el:'.app',
	data:{
		article:`has a lot of code。。。。。。。。。。。。。。。。。。。。`,
	}
});
```
###3. v-model在select中的使用(下拉列表)
3.1 单选下拉列表  
```
<div class="app">
	<div>where are you from？</div>
	<select v-model='from'>
		<option value="1">GUANGZHOU</option>
		<option value="2">BEIJING</option>
	</select>
</div>
```
```
var app = new Vue({
	el:'.app',
	data:{
		from:'1',
	}
});
```
3.2 多选下拉列表
其实就是元素加个multiple属性，表示多个，多选
```
<div class="app">
	<div>where are you want to go？</div>
	<select v-model='from' multiple>
		<option value="1">GUANGZHOU</option>
		<option value="2">BEIJING</option>
		<option value="4">SHANGHAI</option>
		<option value="5">CHENGDU</option>
	</select>
</div>

```
```
var app = new Vue({
	el:'.app',
	data:{
		from:['1','2'],
	}
});
```
