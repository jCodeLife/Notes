vue的控制流指令包括：
v-if、v-else、v-if-else
```
<div class="app">
	<div v-if="role=='admin' || role=='superAdmin'">
		管理你好！
	</div>
	<div v-else-if="role=='HR'">
		HR你好，请查看待查看简历列表：......
	</div>
	<div v-else>
		没有选项访问此页面！
	</div>
</div>
```
```
var app = new Vue({
	el:'.app',
	data:{
		role:'',
	}
});
```
1. v-if
根据表达式的值的真假条件渲染元素。在切换时元素及它的数据绑定 / 组件被销毁并重建
2. v-else-if
前一兄弟元素必须有 v-if 或 v-else-if。
3. v-else
前一兄弟元素必须有 v-if 或 v-else-if。
v-else后面不需要表达式
