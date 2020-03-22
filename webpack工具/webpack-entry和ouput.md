
配置webpack主要是配置出口文件和入口文件：
```
//webpack.config.js文件
module.exports = {
  entry:'./a.js';//入口文件
  output:{
    filename:"pack.js",
    path:__dirname,//__dirname特殊变量表示当前目录
  }
}
```
但是有的时候业务逻辑比较复杂，页面中可能不止一页。当我们有很多页，而且每一页都有相同的依赖，不同的js控制着每一页不同的业务逻辑时。
```
//page one
<body>
	<script src="../js/base.js"></script>
	<script src="../js/home.js"></script>
</body>

//page two
<body>
	<script src="../js/base.js"></script>
	<script src="../js/sighup.js"></script>
</body>
```
webpack怎么做：
```
//webpack.config.js文件
module.exports= {
	entry:{
		home:'./js/home.js',
		signup:'./js/signup.js',
	},
	output:{
		filename:'[name].bundle.js',
		path:__dirname + '/dist',//
	}
}
```
注：
[name]其实就是对应的entry的名字，后面输入的时候名字就是home.bundle.js或者signup.bundle.js，变成动态的输出文件名。
__dirname表示的是当前目录下，
dis表示 distributable，可分发的，这个dist目录常常放置一些打包过的、压缩过的代码。
```
//base.js
var open = true;

module.exports = {
	open:open,
}

//home.js
var base = require('./base.js');
var open = base.open;
if(open){//如梭是开放注册
	document.body.innerHTML = `<a href="signup.html">注册</a>`
}

//signup.js
var base = require('./base.js');
var open = base.open;
if(open){
	document.body.innerHTML=`<h1>welcome！</h1>`;
}else{
	document.body.innerHTML=`<h1>暂时不开放注册</h1>`;
}
```
以上是依赖关系文件。

然后通过命令进行打包
```
npm run pack //pack是为了每次输入命令避免太长，我们自定义的命令。
```
执行完成之后就会多一个dist目录，里面有我们打包好的js文件：home.bundle.js和signup.boundle.js。
有了这两个js文件，文件引入的适合就只要引入打包好的js即可
```
//page one ---index.html
<body>
	<script src="../dist/home.bundle.js"></script>
</body>

//page two----signup.html
<body>
	<script src="../dist/signup.bundle.js"></script>
</body>
```
一般像这样多页的应用，给每一页一个打包的地址文件，具体它每一页的入口文件，用到了那些依赖，我们其实不用去管，把它全部交给webpack，让它去做。

再一个，我们在模块之间分享一些数据，我们可以用ES6的语法；
```
//base.js
var open = true;
export{open};

//home.js
import {open} from './base';//直接可以解构出来
if(open){//如梭是开放注册
	document.body.innerHTML = `<a href="signup.html">注册</a>`
}

//signup.js
import {open} from './base';//直接可以解构出来

if(open){
	document.body.innerHTML=`<h1>welcome！</h1>`;
}else{
	document.body.innerHTML=`<h1>暂时不开放注册</h1>`
}
```
这种方式更加简洁。
最重要的是webpack开箱就支持这种写法。
以上就是webpack对于多入口和多出口的打包情况

