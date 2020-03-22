mixins 官方把它叫做混合，
它更像是 **重复功能和数据的存储器**

如：两个组件之前，他们有重复的功能和数据
```
<!DOCTYPE html>
<html>
<head>
	<title>demo</title>
	<style type="text/css">
	</style>
</head>
<body>
	<div class="demo">
		<myarticle></myarticle>
		<other></other>
	</div>
	
	
	<template id="atc">
		<div>
			<h2 @mouseenter='show' @mouseleave='hide'>come on! baby!!!</h3>
			<p v-if="isShow">ohh my god.This is a...</p>
		</div>
	</template>
	<template id="btn">
		<div>
			<button @click="onClick">click me</button>
			<div v-show="isShow">
				<h2>This is a story about...</h2>
				<p>Register.com offers domain name registration, web hosting, website design and online marketing - all in one place. Award-winning customer service and ...</p>
			</div>
		</div>
	</template>
<script src="https://cdn.bootcss.com/vue/2.6.10/vue.js"></script>
<script type="text/javascript">
	//第一个组件
	Vue.component('myarticle',{
		template:"#atc",
		data:function(){
			return {
				isShow:false,
			}
		},
		methods:{
			show:function(){
				this.isShow = true;
			},
			hide:function(){
				this.isShow = false;
			}
		}
	});
  //另一个组件
	Vue.component("other",{
		template:'#btn',
		methods:{
			onClick:function(){
				this.isShow=!this.isShow;
			}
		},
		data:function(){
			return {
				isShow:false,
			}
		}
	});

	new Vue({
		el:'.demo'
	});

</script>
</body>
</html>
```
以上两个组件都有同样的显示和隐藏功能，数据也是有一样的。重复了很多代码。这个时候vue提供了一个选项mixins机制，可以把一些东西定义到mixins里面。来更方便的存储这些重复功能和数据。相当于用一个数组来保持这些代码，然后在要用的组件定义中mixins进去，注意如果组件定义中有mixins的数据，组件定义的不会被mixins的数据覆盖，相当于样式写在行间的。
```
<!DOCTYPE html>
<html>
<head>
	<title>demo</title>
	<style type="text/css">
	</style>
</head>
<body>
	<div class="demo">
		<myarticle></myarticle>
		<other></other>
	</div>
	
	
	<template id="atc">
		<div>
			<h2 @mouseenter='show' @mouseleave='hide'>come on! baby!!!</h3>
			<p v-if="isShow">ohh my god.This is a...</p>
		</div>
	</template>
	<template id="btn">
		<div>
			<button @click="onClick">click me</button>
			<div v-show="isShow">
				<h2>This is a story about...</h2>
				<p>Register.com offers domain name registration, web hosting, website design and online marketing - all in one place. Award-winning customer service and ...</p>
			</div>
		</div>
	</template>
<script src="https://cdn.bootcss.com/vue/2.6.10/vue.js"></script>
<script type="text/javascript">
	//定义一个mixins对象，其实就是普通对象，可以将它当做component定义里的对象来书写。其实就是组件之间的共同点。
	var bases ={
		data:function(){
			return {
				isShow:false,
			}
		},
		//如果还有其他共同选项数据可继续加...

	};


	//第一个组件
	Vue.component('myarticle',{
		template:"#atc",
		methods:{
			show:function(){
				this.isShow = true;
			},
			hide:function(){
				this.isShow = false;
			}
		},
		mixins:[bases]//可以理解为，将一个或者多个mixins对象通过数组的形式追加到组件定义里头。即vue会合并这个对象和组件
	});

	Vue.component("other",{
		template:'#btn',
		methods:{
			onClick:function(){
				this.isShow=!this.isShow;
			}
		},
		mixins:[bases]//可以理解为，将一个或者多个mixins对象通过数组的形式追加到组件定义里头。即vue会合并这个对象和组件
	});

	new Vue({
		el:'.demo'
	});



</script>
</body>
</html>
```
mixins:[bases]
定义组件的时候加了mixins的选项，就自动加了mixins的功能。vue会合并这个对象和组件。
可以理解为，将一个或者多个mixins对象通过数组的形式追加到组件定义里头。

