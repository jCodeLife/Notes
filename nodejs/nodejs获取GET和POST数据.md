用户发送数据请求的时候，无论是发送GET请求还是POST请求，其数据事实上都在请求内容对象的rul属性中！
`1. GET数据的解析方式`
get数据发送的时候都是在url中的，`req.url`,req表示请求的内容对象，里面包括了很多请求相关的信息。
```
方法一：手动切
const http=require("http");//引入http模块
http.createServer(function(req,res){//通过http模块对象创建服务器
	//req获取前台发的数据
	var GET ={};
	if (req.url.indexOf('?')!=-1) {
		var arr = req.url.split('?');
		var url=arr[0];//地址
		var arr2 = arr[1].split('&');
		for (var i = 0; i < arr2.length; i++) {
			var arr3 = arr2[i].split('=');
			GET[arr3[0]]=arr3[1];
		}
	}else{
		var url=req.url;
		// GET={}
	}
console.log(url,GET);
res.write("aaa");//响应写在页面上的内容
res.end();//结束响应
}).listen(8080);//要个端口并监听
---------------------------------------------------------------------------------

方法二：使用querystring模块
const http = require('http');
const querystring=require('querystring');
http.createServer(function(req,res){
	var GET={};
	if (req.url.indexOf('?')!=-1) {
		var arr=req.url.split('?');
		var url = arr[0];
		GET=querystring.parse(arr[1]);//
	}else{
		var url=req.url;
	}
	console.log(GET);
	res.write('aaaa');
	res.end();
}).listen(8080);
---------------------------------------------------------------------------------

方法三：使用url模块
const http = require('http');
const urlLib = require('url');
var GET={};
http.createServer(function(req,res){
	var obj=urlLib.parse(req.url,true);
	var url=obj.pathname;
	var GET=obj.query;

	console.log(url,GET);
	res.write('aaaaa');
	res.end();
}).listen(8080);
```
GET数据的解析方式：req.url----->urlLib.parse(url,true);

`2. POST数据如何接收`
与GET数据相比，POST数据量大，得分段：
`req.on('data',function(data){})`监听当有一段数据到达的时候，回调函数参数data为每段达到的数据。
`req.on('end',function(){})`数据全部到达

```
var http=require('http');
var querystring=require('querystring');
http.createServer(function(req,res){	
	var str='';
	var i=0;
	req.on('data',function(data){
		console.log(`第${++i}次收到数据`);
		str+=data;
	});//当有一段数据到达的时候
	req.on('end',function(){
		var POST=querystring.parse(str);
		console.log(POST);
	});//数据全部到达
}).listen(8080);

```
`重新搭一遍服务器`
```
//引入相应模块
const http=require('http');//http协议相关
const fs=require('fs');//文件系统相关
const querystring=require('querystring');//查询字符串相关
const urlLib=require('url');//处理url相关

var server=http.createServer(function(req,res){
	//GET
	var obj=urlLib.parse(req.url,true);
	var url=obj.pathname;
	const GET=obj.query;

	//POST
	var str='';
	var POST='';
	req.on('data',function(data){
		str+=data;
	});
	req.on('end',function(){
		POST=querystring.parse(str);
	});
	// console.log(url,GET,POST)

	//文件请求
	var file_name='./www'+url;
	fs.readFile(file_name,function(err,data){
		if (err) {
			res.write("404");
		}else{
			res.write(data);
		}
		res.end();
	});

});

server.listen(8080);//要个端口并且监听该端口
```

