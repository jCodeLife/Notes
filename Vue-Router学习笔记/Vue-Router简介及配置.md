`1. 简介`
Vue Router：是 Vue.js官方的路由管理器
作用：`指导一个网页的层级以及用与定位资源。`可以用于快速的构建单页面应用。
好处：Vue Router每次刷新时只需要加载一次数据，页面中的数据包括任一组件的状态都是可以保留的。不丢失状态，不丢失数据，极大的节省资源。 
 
`2. 基础配置`
使用 Vue.js + Vue Router 可以快速的构建单页面应用。使用 Vue.js ，我们已经可以通过组合组件来组成应用程序，当把 Vue Router 添加进来，我们需要做的是，将组件 (components) 映射到路由 (routes)，然后告诉 Vue Router 在哪里渲染它们。

```
<!DOCTYPE html>
<html>
<head>
	<title>demo</title>
</head>
<body>
	<div id="app">
		<div>
			<!-- 使用 router-link 组件来导航. -->
			<!-- 通过传入 `to` 属性指定链接. -->
			<!-- <router-link> 默认会被渲染成一个 `<a>` 标签 -->
			<router-link to="/">首页</router-link>
			<router-link to="/about">关于我们</router-link>	
		</div>
		<div>
			<!-- 路由出口 -->
			<!-- 路由匹配到的组件将渲染在这里 -->
			<router-view></router-view>
		</div>

	</div>

	<!-- 引入vue和vue-router -->
	<script src="https://cdn.bootcss.com/vue/2.6.10/vue.js"></script>
	<script src="https://cdn.bootcss.com/vue-router/3.0.7/vue-router.js"></script>
	<script type="text/javascript">
		// 定义路由，每个路由应该映射一个组件(component)。
		//路由组件可以从其他文件 import 进来
		var routes = [{
			path:'/',
			component:{
				template:`
				<div>
					<h1>首页</h1>
				</div>
				`,
			},
		},
		{
			path:'/about',
			component:{
				template:`
				<div>
					<h1>关于我们</h1>
				</div>
				`,
			}
		}];
		//创建 router 实例，然后传 `routes` 配置
		var router = new VueRouter({
			routes:routes,
		});
		//创建和挂载根实例。
		//要通过 router 配置参数注入路由，从而让整个应用都有路由功能
		new Vue({
			el:'#app',
			router:router,
		});
	</script>

</body>
</html>
```  
