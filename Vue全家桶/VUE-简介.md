#基本用法
##一、vuejs简介
-  是一个构建用户界面的框架
- 是一个轻量级的MVVM（Model-View-ViewModel），其实就是所谓的数据的双向绑定
- 数据驱动和组件化的前端开发
- 通过简单的API就能实现**响应式的数据绑定**和**组合的视图组件**
指令：
用来扩展html标签的功能

vue与其他框架的对比
- 简单、易学、更轻量
- 指令v-xxx开头
- HTML + JSON数据
- 开发者 尤雨溪 华人

这几个框架都不兼容低版本IE

##二、起步
1. 下载核心库vue.js
目前有1.0和2.0两个大版本
vue2.0与vue1.0相比，最大的变化就是引入了Virtual DOM（虚拟DOM），页面的更新效率更高，速度更快。
2. hello word
```
<div class="app" >
		{{msg}}
	</div>
	<script src="vue.js"></script>
	<script type="text/javascript">
		window.onload = function(){
			new Vue({
				el:".app",
				data:{
					msg:"HelloWord!"
				}
			});
		}
	</script>
```
3. 可以安装vue-devtools插件，便于在Chrome中调试vue
可以在GITHUB上下载vue-devtools，解压后，将文件中的chrome拖放到扩展程序中。


##VUE中常用指令
v-model：双向数据绑定，一般用于表单元素
v-for：对数组或者对象进行循环操作
v-on:用来绑定事件，用法：v-on:事件="函数"
v-show:用来显示或者隐藏元素，实质是通过display实现
v-if
...
##四、事件和属性
1. 事件
1.1 事件简写
**v-on:事件**，简写成：**@事件名**
1.2 事件对象
vue里面的事件对象使用$event
这个$event包含了事件事件相关的信息，如事件源、事件类型、偏移量等等...
如：点击按钮，将对应按钮的文字返回给我
```
<div class="app" >
		<input type="button" value="点我" @click="print($event)">
	</div>
	<script src="vue.js"></script>
	<script type="text/javascript">
		window.onload = function(){
			let vm = new Vue({
				el:".app",
				data:{
					msg:"HelloWord!"
				},
				methods:{
					// print:function(event){
					// 	console.log(event.target.value);						
					// }
					// 或者：如下结果一样的
					print(event){
						console.log(event.target.value);						
					}
				}
			});
		}
	</script>
```
  1.3 事件冒泡
  阻止事件冒泡：
  （1）原生JS，依赖于事件对象
  （2）vue方式，不依赖于事件对象
       在事件里加个stop修饰符：  **@click.stop**

1.4 事件默认行为
  阻止默认事件
  （1）原生JS，依赖于事件对象 e.preventDefault()
  （2）vue方式，不依赖于事件对象
       在事件里加个prevent修饰符：  **@click.prevent**

1.5 关于键盘事件
@keydown、@keypress、@keyup
 比如我们在判断按键是不是回车的时候，不用挂在判断keycode了。可以加个修饰符：
@keydown.13 或者keydown.enter
其实13是ACILL码值，enter是vue内部做了映射，也就是回车键的别名。
上：keydown.38或者keydown.up
...
注意：默认没有@keydown.a/b/c.......,可以自定义。成为自定义键码或者自定义键位别名。

1.6 事件修饰符
.stop
调用event.stopPropagation();
.prevent
调用event.preventDefault();
.{keyCode | keyAlias}
只当事件是从特定键触发时，才触发回调。
.native
监听组件根元素的原生事件
.once
只触发一次回调

2.  属性
2.1 属性的绑定和简写
 v-bind用于属性绑定，
格式**v-bind:属性=""**,可简写为**:属性=""**
2.2 class和style属性

##五、 模板
1. 简介
Vue.js使用基于HTML的模板语法，可以将DOM绑定到Vue实例中的数据模板就是{{}},用来进行数据绑定，显示在页面中，这种{{}}叫做Mustache语法。
2. 数据的绑定方式
2.1 双向绑定
  v-model
2.2 单项绑定
 方法1：使用{{}}，可能会出现闪烁问题，可以使用v-cloak解决。
 方法2：使用v-text、v-html
3. 其他指令
v-once 数据只绑定一次
v-pre 直接原样显示

##六、过滤器
1. 简介
用来过滤模型数据的，在显示之前进行数据的处理和筛选。
语法：
```
 {{data | filter(参数) | filter(参数)}}
```
2. 关于 内置过滤器
Vue1.0中内置了许多过滤器，如：
  currency、uppercase、lowercase
  limitBy
  orderBy
  filterBy
在Vue2.0中已经移除了所有内置过滤器。解决方案：
（1）使用第三方工具库：如loadash、date-fns日期格式化、accounting货币格式化；
（2）使用自定义过滤器；
#使用axios/vue-resource发送HTTP请求
##一、发送AJAX请求
1. 基本介绍
vue本身不支持发送AJAX请求，需要时vue-resource、axios等插件实现。
axios时一个基于Promise的HTTP请求客户端，用来发送请求，官方Vue2.0推荐使用axios，同时不再对vue-resource不再更新维护了。
参考	：GitHub上搜索axios，查看API
2. 使用axios发送AJAX请求
2.1   安装axios并引入
2.2基本用法：
Performing a GET request

```
const axios = require('axios');

// Make a request for a user with a given ID
axios.get('/user?ID=12345')
  .then(function (response) {
    // handle success
    console.log(response);
  })
  .catch(function (error) {
    // handle error
    console.log(error);
  })
  .finally(function () {
    // always executed
  });

// Optionally the request above could also be done as
axios.get('/user', {
    params: {
      ID: 12345
    }
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  })
  .then(function () {
    // always executed
  });  

// Want to use async/await? Add the `async` keyword to your outer function/method.
async function getUser() {
  try {
    const response = await axios.get('/user?ID=12345');
    console.log(response);
  } catch (error) {
    console.error(error);
  }
}
```
Performing a POST request
```
axios.post('/user', {
    firstName: 'Fred',
    lastName: 'Flintstone'
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```
Performing multiple concurrent requests
```
function getUserAccount() {
  return axios.get('/user/12345');
}

function getUserPermissions() {
  return axios.get('/user/12345/permissions');
}

axios.all([getUserAccount(), getUserPermissions()])
  .then(axios.spread(function (acct, perms) {
    // Both requests are now complete
  }));
```
Requests can be made by passing the relevant config to axios.
axios(config)
```
// Send a POST request
axios({
  method: 'post',
  url: '/user/12345',
  data: {
    firstName: 'Fred',
    lastName: 'Flintstone'
  }
});
// GET request for remote image
axios({
  method: 'get',
  url: 'http://bit.ly/2mTM3nY',
  responseType: 'stream'
})
  .then(function (response) {
    response.data.pipe(fs.createWriteStream('ada_lovelace.jpg'))
  });
```
axios(url[, config])
```
// Send a GET request (default method)
axios('/user/12345');
```

更多知识可以查看官方[https://github.com/axios/axios](https://github.com/axios/axios)
3. vue-resource发送请求
可以参考vue-resource的API[https://github.com/pagekit/vue-resource](https://github.com/pagekit/vue-resource)

另外还有jsonp的一些内容。以后了解。

# vue生命周期及实例的属性和方法
##一、vue的生命周期
vue实例从创建到销毁的过程，成为生命周期，共有八个阶段；
##二、计算属性
1. 基本用法
计算属性也是用来存储数据的，但是具有以下几个特点：
1.1数据可以进行逻辑处理操作
1.2 对计算属性中的数据进行监控
2. 计算属性VS方法
将计算属性的get函数定义为一个方法也可以实现类似的功能。
区别：
2.1 计算属性是基于它的依赖进行更新的，只有在相关依赖发生改变时才能更新变化。
2.2 计算属性是有缓存的，只要依赖关系没有发生改变，多次访问计算属性得到的值都是之前缓存的计算结果，不会多次执行。
3. get和set
 3.1 计算属性有两部分组成：get和set，分别用来获取计算属性和设置计算属性，默认只有get方法，如果需要set，要自己添加。
##三、Vue实例的属性和方法
1. 属性
vm.属性名  获取data中的属性
vm.\$el 获取vue实例相关的元素
vm.\$data 获取数据对象data
vm.\$options 获取自定义属性
vm.\$refs 获取所有添加ref属性的元素，得到是一个dom对象数组
2. 方法
vm.\$mount() 手动挂载vue实例
vm.\$destroy() 销毁实例
vm.\$nextTick() 在DOM更新完成后再执行里面的回调函数，一般修改数据后使用该方法，以便获得更新后的DOM。再重新修改数据的时候，Vue实现响应式，但是并不是数据发生改变的时候DOM就立即变化了，需要一定的时间进行DOM更新。那么这个时候，我们希望的是，当数据更新时，等DOM重新再页面更新完成后，再执行相关操作，那么我们可以使用该方法 。
vm.\$set() 在vue中通过普通的方式为对象添加属性时vue无法实时监控到如：this.user.age=22;这时，我们可以使用vue实例的\$set()方法来为对象添加属性，并可以实时监控。如this.\$set(this.user,'age',22);
vm.\$delete() 在vue中要想删除一个属性，普通方法delete this.user.age时无效的。可以通过全局Vue.delete(this.user,'age');或实例vm.\$delete(this.user,'age');
vm.\$watch()  对实例中的属性进行监控。
方法一：使用vue实例提供的vm.\$watch() 方法，
方法二：使用vue实例提供的watch选项，即跟data、methods等一样。

##四、自定义指令
1. 自定义全局指令
通过Vue.directive()注册或获取全局指令。
```
// 注册
Vue.directive('my-directive', {
  bind: function () {},
  inserted: function () {},
  update: function () {},
  componentUpdated: function () {},
  unbind: function () {}
})

// 注册 (指令函数)
Vue.directive('my-directive', function () {
  // 这里将会被 `bind` 和 `update` 调用
})

// getter，返回已注册的指令
var myDirective = Vue.directive('my-directive')
```
一个指令定义对象可以提供如下几个钩子函数 (均为可选)：
- bind：只调用一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置。
- inserted：被绑定元素插入父节点时调用 (仅保证父节点存在，但不一定已被插入文档中)。
- update：所在组件的 VNode 更新时调用，但是可能发生在其子 VNode 更新之前。指令的值可能发生了改变，也可能没有。但是你可以通过比较更新前后的值来忽略不必要的模板更新
- componentUpdated：指令所在组件的 VNode 及其子 VNode 全部更新后调用。
- unbind：只调用一次，指令与元素解绑时调用。

钩子函数参数
- el：指令所绑定的元素，可以用来直接操作 DOM 。
- binding：一个对象，包含以下属性：
name：指令名，不包括 v- 前缀。
value：指令的绑定值，例如：v-my-directive="1 + 1" 中，绑定值为 2。
oldValue：指令绑定的前一个值，仅在 update 和 componentUpdated 钩子中可用。无论值是否改变都可用。
expression：字符串形式的指令表达式。例如 v-my-directive="1 + 1" 中，表达式为 "1 + 1"。
arg：传给指令的参数，可选。例如 v-my-directive:foo 中，参数为 "foo"。
modifiers：一个包含修饰符的对象。例如：v-my-directive.foo.bar 中，修饰符对象为 { foo: true, bar: true }。
- vnode：Vue 编译生成的虚拟节点。移步 VNode API 来了解更多详情。
- oldVnode：上一个虚拟节点，仅在 update 和 componentUpdated 钩子中可用。

除了 el 之外，其它参数都应该是只读的，切勿进行修改。如果需要在钩子之间共享数据，建议通过元素的 dataset 来进行。
2. 自定义局部指令
在vue实例里面添加directives : {}
```
directives: {
  focus: {
    // 指令的定义
    inserted: function (el) {
      el.focus()
    }
  }
}

然后你可以在模板中任何元素上使用新的 v-focus 属性，如下：

<input v-focus>
```
##五、过渡动画

1.简介 
Vue在插入、更新或者移除DOM时，提供了多种不同方式的应用过渡效果。
本质上还是使用CSS3动画，transition、animation。只是做了一些封装，在操作的时候更加简单。
2. 基本使用
使用transition组件，将要执行动画的元素包含在该组件内。
```
<transition>
 需要执行动画的元素
</transtion>
```
过渡的CSS类名：6个
- v-enter：定义进入过渡的开始状态。在元素被插入之前生效，在元素被插入之后的下一帧移除。
- v-enter-active：定义进入过渡生效时的状态。在整个进入过渡的阶段中应用，在元素被插入之前生效，在过渡/动画完成之后移除。这个类可以被用来定义进入过渡的过程时间，延迟和曲线函数。
- v-enter-to: 2.1.8版及以上 定义进入过渡的结束状态。在元素被插入之后下一帧生效 (与此同时 v-enter 被移除)，在过渡/动画完成之后移除。
- v-leave: 定义离开过渡的开始状态。在离开过渡被触发时立刻生效，下一帧被移除。
- v-leave-active：定义离开过渡生效时的状态。在整个离开过渡的阶段中应用，在离开过渡被触发时立刻生效，在过渡/动画完成之后移除。这个类可以被用来定义离开过渡的过程时间，延迟和曲线函数。
- v-leave-to: 2.1.8版及以上 定义离开过渡的结束状态。在离开过渡被触发之后下一帧生效 (与此同时 v-leave 被删除)，在过渡/动画完成之后移除。
3. 钩子函数8个
```
<transition
  v-on:before-enter="beforeEnter"
  v-on:enter="enter"
  v-on:after-enter="afterEnter"
  v-on:enter-cancelled="enterCancelled"

  v-on:before-leave="beforeLeave"
  v-on:leave="leave"
  v-on:after-leave="afterLeave"
  v-on:leave-cancelled="leaveCancelled"
>
```

 4. 自定义过渡的类名
我们可以通过以下特性来自定义过渡类名：
```
enter-class
enter-active-class
enter-to-class (2.1.8+)
leave-class
leave-active-class
leave-to-class (2.1.8+)
```
他们的优先级高于普通的类名，这对于 Vue 的过渡系统和其他第三方 CSS 动画库，如 Animate.css 结合使用十分有用。
```
<link href="https://cdn.jsdelivr.net/npm/animate.css@3.5.1" rel="stylesheet" type="text/css">

<div id="example-3">
  <button @click="show = !show">
    Toggle render
  </button>
  <transition
    name="custom-classes-transition"
    enter-active-class="animated tada"
    leave-active-class="animated bounceOutRight"
  >
    <p v-if="show">hello</p>
  </transition>
</div>
new Vue({
  el: '#example-3',
  data: {
    show: true
  }
})
```
5. 多个元素的过渡
```
<transition-group>
  <p :key="1"></p>
  <p :key="2"></p>
</transition-group>
```

#组件及组件间的通信
组件用来扩展HTML元素，封装可重用代码。
组件就是自定义的元素（标签、对象）
1. 定义组件
方式1：先创建组件构造器，然后用组件构造器创建组件。
```
<div id="app"></div>
<script>
  //使用Vue.extend()创建组件构造器
  Vue.extend({
    template:"<h2>Hello Word</h2>" 
   });
  //使用Vue.component()根据传入的组件名和组件构造器来创建组件。
  Vue.component("hello","myComponent");
  new Vue({
    el:"#app"
  });
</script>
```
方式二：直接创建组件（推荐，比较简单。）
```
 Vue.component("test",{
  template:"<h3>try</h3>"     
 });
```
2. 组件的分类
- 全局组件
全局组件可以在所有vue实例中使用
```
Vue.component("my-hello",{
  template: "<h4>Hello Word！</h4>" ;
  data:function(){
    return:{
      name:"alice",
      age:12,
     //ande other data ....
    }
  }
});
new Vue({
  el:"#app"
});
```

- 局部组件
局部组件只能在当前vue实例中使用
在vue实例中添加一个components选项
```
new Vue({
  el:"#app",
  components:{
    "my-components-name":{
      template:"<p>111</p>"，
      data(){
        return{
          age:11,
          ...
        }
      }
    }，
     
  }
});
```
注意：在自定义全局或者局部组件的时候，如果要在组件中存储数据，那么data必须时函数形式，该函数返回一个对象，对象里面就是要存储的数据。这样在html中的该组件拿存储的数据的时候就能拿到了 。
3. 引用模板<template>
通过vue定义好的模板组件，将模板相关的内容写在html内部，通过id相连接自定义组件
简单的说就是：将组件内容放到模板中并引用。
```
<body>
  <div class="app">
    <my-hello></my-hello>
   </div>
   <template id="wbs">
      <div>
          <h3>{{msg}}</h3>
          <ul>
              <li v-for="v in arr">
                  {{v}}
              <li>
          </ul>
      </div>
   </template>
<script>
  var vm = new Vue({
    el:".app",
    components:{
      "my-hello":{
        name:"wbs12344",//指定组件的名称，若没加name，默认是标签名
        template:"#wbs",
        data(){
          return{
            msg:"welcome",
            arr:[1,2,3,4],
          }
        }
      }
    }
  });
</script>
</body>
```
注意：
<template>内，必须有且仅有一个根元素。
定于组件的时候组件若没加name，默认是标签名组件名是name。
4. 动态组件
<component :is="">动态组件
多个组件使用同一个挂载点，然后动态的在他们之间进行切换
```
<body>
<div class="app">
	<button @click="flag='my-name'">显示name组件</button>
	<button @click="flag='my-age'">显示age组件</button>
	<div>	
		<component :is="flag"></component>
	</div>
</div>
<script src="vue.js"></script>
<script type="text/javascript">
	var vm = new Vue({
		el:".app",
		data:{
			flag:"",
		},
		components:{
			"my-name":{
				template:"<h1>这是my-name组件，x为{{x}}</h1>",
				data:function(){
					return{
						x:Math.random()
					}
				}
			},
			"my-age":{
				template:"<h3>这是my-age组件，y为{{y}}</h3>",
				data(){
					return{
						y:Math.random()
					}
				}
			}
		}
	});

</script>

</body>
```
5. <keep-alive>组件
如果把切换出去的组件保留在内存中，可以保留它的状态或者避免重新渲染。为此可以在动态组件外部套一个keep-alive作为指令参数。
```
<body>
<div class="app">
	<button @click="flag='my-name'">显示name组件</button>
	<button @click="flag='my-age'">显示age组件</button>
	<div>	
		<keep-alive>
			<component :is="flag"></component>
		</keep-alive>
	</div>
</div>
<script src="vue.js"></script>
<script type="text/javascript">
	var vm = new Vue({
		el:".app",
		data:{
			flag:"",
		},
		components:{
			"my-name":{
				template:"<h1>这是my-name组件<br>{{x}}</h1>",
				data:function(){
					return{
						x:Math.random()
					}
				}
			},
			"my-age":{
				template:"<h3>这是my-age组件<br>{{y}}</h3>",
				data(){
					return{
						y:Math.random()
					}
				}
			}
		}
	});

</script>

</body>
```
如上，当在切换的时候，默认每次切换都会销毁非活动组件，并重新加载。通过keep-alive组件，将切换出去的元素还是保存在内存中，不会重新加载。即缓存非活动元素，可以保留状态，避免重新渲染，

6. 组件之间数据传递
6.1 父子组件间的数据传递
父子组件是在一个组件内包含另一个组件。
子组件只能在父组件内部使用
默认情况下，子组件不能直接访问夫组件中的数据，父组件也不能直接访问子组件的数据，因为每个组件中的数据的作用域的独立的。
6.2 父子组件间的数据传递（通信）
（1）子组件访问父组件的数据
第一步：当调用子组件时，在子组件中绑定想要获取的父组件中的数据。（在html中）
第二部：在子组件内部，使用props选项声明获取的数据，即使用props来接受来自父组件的数据。
即：父组件通过props向下传递数据给子组件
注：
**组件中的数据共有三种形式：data、props、computer**
Prop 验证
```
Vue.component('my-component', {
  props: {
    // 基础的类型检查 (`null` 和 `undefined` 会通过任何类型验证)
    propA: Number,
    // 多个可能的类型
    propB: [String, Number],
    // 必填的字符串
    propC: {
      type: String,
      required: true
    },
    // 带有默认值的数字
    propD: {
      type: Number,
      default: 100
    },
    // 带有默认值的对象
    propE: {
      type: Object,
      // 对象或数组默认值必须从一个工厂函数获取
      default: function () {
        return { message: 'hello' }
      }
    },
    // 自定义验证函数
    propF: {
      validator: function (value) {
        // 这个值必须匹配下列字符串中的一个
        return ['success', 'warning', 'danger'].indexOf(value) !== -1
      }
    }
  }
})
```
（2）父组件访问子组件的数据
第一步：在子组件中使用vm.$emit(事件名，数据)触发一个自定义事件，事件名自定义。
第二步：父组件在使用子组件的地方监听子组件触发的事件，并子父组件中定义方法，用来获取数据。
总结：子组件通过events给父组件发送消息，实际上就是子组件把自己的数据发送到父组件。



- 单项数据流 
父级 prop 的更新会向下流动到子组件中，但是反过来则不行。这样会防止从子组件意外改变父级组件的状态，从而导致你的应用的数据流向难以理解。
不允许子组件直接修改父组件中的数据，否则报错。
解决方案：
情况一：如果子组件想把父组件的数据作为局部数据使用，可以将数据存入到另外一个变量中再操作，不影响父组件中的数据。
情况二：如果子组件想修改拿到的数据并且同步更新到父组件，两个方法：
方法1：使用.sync修饰符，需要显示的触发一个事件。
方法2： 可以将数据包装成一个对象，然后子组件中修改对象的属性。（因为对象是引用类型，指向一个内存空间）

6.2 非父子组件间的通信
非父子组件间的通信，可以通过一个空的Vue实例作为中央事件总线（事件中心），用来触发事件和事件监听。
```
var Event   = new Vue();
Event.$emit(事件名，数据);
Event.$on(事件，data=>{})
```

7. slot内容分发
作用：获取组件中的原内容。
```
<body>
<div class="app">
	<demo-component>这里有内容，那么slot里面显示的就是这个。</demo-component>	
</div>
<template id="demo">
	<div>
		<h1>This is a demo</h1>
		<slot>如果没有内容，显示这个！</slot>
	</div>
</template>
<script src="vue.js"></script>
<script type="text/javascript">
	var vm =new Vue({
		el:".app",
		components:{
			"demo-component":{
				template:"#demo",
			}
		}
	});

</script>

</body>
```
#vue-router路由的使用
1. 简介
使用Vue.js开发单页面应用(Single Page Application)
根据不同的url地址，显示不同的内容，但显示在同一个页面中给，称为单页面应用。
[vue-router官网参考](https://router.vuejs.org/zh/)
2. 基本用法
布局
配置路由

3. 路由嵌套和参数的传递

#vue-cli脚手架
1. 简介
vue-cli是一个vue脚手架，可以快速构造项目结构
vue-cli本身集成了多种项目模板
simple 简单
webpack 包含ESLint代码规范的检查和unit单元测试
webpack-simple 没有代码规范检查和单元测试
browserify 使用的也比较多
browser-simple 也没有代码规范检查和单元测试。
2. 步骤
2.1 安装vue-cli，其实就是配置vue命令的环境。
conpm install vue-cli -g
vue --version
vue list
2.2 初始化项目，生成项目模板
语法：vue init 模板名 项目名
如vue init webpack-simple vue-cli-demo
2.3 进入生成的项目目录，安装模块包
cd vue-cli-demo
cnpm install
2.4 运行
npm run dev//启动测试服务
npm run build//将项目打包输出dist目录，项目上线的话要将dist目录拷贝到服务器上。
3. 使用webpack模板

注：ESLint是用来统一代码和风格的工具，如：缩进、空格、符号等，要求比较严格

#模块化开发
1.vue-router模块化
cnpm install vue-router -s
1.1.  编辑main.js
1.2. 编辑app.vue
1.3 编辑router.config.js
2. axios模块化
cnpm install axios -s
使用axios的两种方式
方法1：在每一个组件中引入axios
方法2：在main.js中全局引入axios并添加到Vue原型中

3. 为自定义组件添加事件

# Element UI
1. 简介
Element UI是饿了么团队提供的一套基于Vue2.0的组件库，用来快速搭建网站，提高开发效率。
  Element UI ：pc端
  MintUI ：移动端
2. 快速上手
2.1 安装Element ui
cnpm install element-ui -s
2.2在main.js中引入并使用组件
import ElementUI form "element-ui"
import "element-ui/lib/theme-default/index.css"//这样式文件需要单独引入
Vue.use(ElementUI)
这种方式引入了ElementUI中的所有组件。
2.3在webpack.config.js中添加loader
2.4使用组件
2.5使用less
#自定义全局组件（插件）
全局组件（插件），就是指可以在main.js中使用Vue.js进行全局引入，然后在其他组件中就都可以使用了。入vue-router.
普通组件（插件）.每次使用时都要引入，如axios


#状态管理模式
Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。
1. 基本用法
1.1 安装vuex
1.2创建store.js文件，在main.js中导入并配置store选项
1.3编辑store.js文件
1.4编辑app.vue
2. 更好的组织vuex项目结构




最后
最后
最后
最后
最后
最后
最后
最后
最后
这是第一次学习vue全家桶，看得很吃力，太多新的概念了，并且用到一些工具，前面没有学，如nodejs npm webpack等等...硬着头皮开完了视频。[视频来源w3c官网，小白学前端：Vue.js 2.0之全家桶](https://www.w3cschool.cn/vuejs_txy_base/ "小白学前端：Vue.js 2.0之全家桶（进阶课程）")

之后再重新开始学一遍全家桶的每个点。

