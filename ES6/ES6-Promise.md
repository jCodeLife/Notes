**一、同步异步**
异步：操作之前没有关系，同时进行多个操作；
同步：同时只能做一件事；

异步：代码更复杂
同步：代码简单
```
异步：
ajax('/banners',function(banner_data){
	ajax('/hotItems',function(hotitem_data){

		ajax('/slides',function(slide_data){
			// more.........
		},function(){
		  alert(‘读取失败’)
		});

	},function(){
	  alert(‘读取失败’)
	});


},function(){
  alert(‘读取失败’)
});
```
**二、Promise**
Promise简单的说是消除异步操作，但是它只不过是非常巧妙的封装了，本质上依然是异步。
可以用同步一样的方式，来书写异步代码。
Promise是es6自带的，不用引任何东西。
```
使用Promise：
let p = new Promise(function(resolve,reject){
  //异步代码
	$.ajax({
		url:'arr.txt';
		dataType:'json',
		success(arr){
			resolve(arr);//成功时调用resolve()
		},
		error(error){
			reject(error);//失败时调用error()
		}
	});
});
//参数：
//resolve--成功了
//reject--失败了

p.then(function1(){
  alert("成功了");
},function2(){
  alert("失败了");
});
//then可以理解为：然后呢,
//当p成功时候，调用第一个function，调用失败时第二个
```
```
//json.txt
{"a":12,"b":"asdfgh","c":55}

let p = new Promise(function(resolve,reject){
  //异步代码
	$.ajax({
		url:'./data/arr.txt';
		dataType:'json',
		success(arr){
			resolve(arr);//成功时调用resolve()
		},
		error(error){
			reject(error);//失败时调用error()
		}
	});
});

let p2 = new Promise(function(resolve,reject){
  //异步代码
	$.ajax({
		url:'./data/json.txt';
		dataType:'json',
		success(arr){
			resolve(arr);//成功时调用resolve()
		},
		error(error){
			reject(error);//失败时调用error()
		}
	});
});

//Promise身上有一个all表示，全都执行完之后...全成功才成功，一个失败就失败
Promise.all([p1,p2]).then(function(arr){//其实arr中，装的就是p1和p2的结果
  let [res1,res2] = arr;//这样就可以通过解构找出对应的结果
  alert("全都成功");
},function(){
  alert("至少有一个失败");
});;
```
```
优化上面代码：

function createPromise(url){
  $.ajax({
        url;//url:url的简写
        dataType:'json',
        success(arr){
            resolve(arr);//成功时调用resolve()
        },
        error(error){
            reject(error);//失败时调用error()
        }
    });
}

Promise.all([createPromise('data/arr.txt'),createPromise('data/json.txt')]).then(function(arr){
  let [res1,res2] = arr;//这样就可以通过解构找出对应的结果
  alert("全都成功");
},function(){
  alert("至少有一个失败");
});;
```
```
其实jQuery的ajax高版本，也自带promise功能
let p = $.ajax([url:'data/arr.txt',dataType:'json']);
//其实这个时候ajax的返回值及时一个Promise对象
```
```
Promise.all([
  $.ajax({url:"data/arr.txt",dataType:''json"}),
  $.ajax({url:"data/json.tex",dataType:"json"})
]).then(function (results) {
  let[arr,json] = results;
  console.log(成功了);
  console.log(arr);
  console.log(json);
},function(){
  console.log("失败了");
});
```
所以有了Promise之后的异步：
```
Promise.all([$.ajax(),$.ajax()]).then(results=>{
  //对了
},err =>{
  //错了
});
```
三、Promise的其他用法
Promise.all 
Promise.race 竞速，用法跟all差不过
```
Promise.race([
  $.ajax({url:"https://a2.taobao.com/data/user"});
  $.ajax({url:"https://a3.taobao.com/data/user"});
  $.ajax({url:"https://a4.taobao.com/data/user"});
]);
```

