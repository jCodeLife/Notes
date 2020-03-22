
##拖拽接口
学习拖拽，主要是学习拖拽事件，根据应用于被拖拽元素和应用于目标元素的不同，我们一般可以将拖拽事件分类：

1. 应用于被拖拽元素的拖拽事件：
- **ondragstrat：当拖拽开始时调用；**
- **ondrag：当拖拽的时候，在整个拖拽过程都会调用**
- **ondragleave：当鼠标离开拖拽元素的时候调用**
- **ondragend：当拖拽结束时调用**

触发顺序：
 1-->ondragstart 拖拽开始
 2-->ondrag 拖拽过程中（持续拖拽 持续触发）
 3-->ondragleave 离开拖拽元素时
 4--> ondrag 还在拖拽过程中（持续拖拽 持续触发）
 5--> 拖拽结束

2. 拖拽事件应用于目标元素：
- **ondragenter：应用于目标元素，当拖拽元素进入目标元素时调用；**
- **ondragover：当拖拽元素停留在目标元素上时调用；**
- **ondrop：当拖拽元素在目标元素上松开鼠标放下时调用；**
注意：浏览器有个默认行为，默认阻止ondrop事件：那么我们必须在ondragover中阻止浏览器的默认行为。
- **ondragleave：当鼠标离开目标元素时调用**

使用上面的这些事件，写个简单的拖拽案例：

```
<!DOCTYPE html>
<html>
<head>
	<title>demo</title>
	<style type="text/css">
		p{
			background-color: #888;
		}
		div{
			width: 200px;
			height: 200px;
			border: 1px solid red;
			float: left;
			margin-left: 50px;
		}
	</style>
</head>
<body>
	<div class="div1" id="div1">
		<p id="pe" draggable="true">试着把我拖过去</p>
	</div>
	<div class="div2" id="div2"></div>
	<script type="text/javascript">
		//被拖拽元素
		var p = document.querySelector("#pe");
		p.ondragstart = function(){
			console.log('ondragstart 拖拽开始了');
		}
		p.ondragend = function(){
			console.log('ondragend 拖拽结束了');
		}
		p.ondragleave = function(){
			console.log('ondragleave 离开拖拽元素了');
		}
		p.ondrag = function(){
			console.log('ondrag 拖拽过程中');
		}

		// 拖拽目标
		var div2 = document.querySelector("#div2");
		div2.ondragenter=function(){
			console.log("ondragenter 拖拽元素进入目标元素了");
			
		}
		div2.ondragover = function(e){
			// 注意：浏览器有个默认行为，默认阻止ondrop事件：那么我们必须在ondragover中(一定要这里)阻止浏览器的默认行为。
			console.log("ondragover 拖拽元素在目标元素上时");
			e.preventDefault();

		}
		div2.ondrop = function(){
			// 注意：浏览器有个默认行为，默认阻止ondrop事件：那么我们必须在ondragover中阻止浏览器的默认行为。
			console.log("ondrop 拖拽元素在目标元素上松开鼠标放下");
			// 添加被拖拽的元素到当前目标元素。
			div2.appendChild(p);
		}
		div2.ondragleave = function(){
			console.log("ondragleave：鼠标离开目标元素了");
		}

		// 拖拽回去
		var div1 = document.querySelector("#div1");
		div1.ondragover = function(e){
			e.preventDefault();

		}
		div1.ondrop = function(){
			div1.appendChild(p);
		}
	</script>
</body>
</html>
```
![拖拽事件触发顺序](https://upload-images.jianshu.io/upload_images/17785871-52650c2c364ec750.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
当上面的例子还是有很大的问题，只能指定元素拖拽到指定位置，太局限。
很多时候，我们希望多个元素能被拖拽，同时也有多个目标元素，即：我希望能够任意个被拖拽元素，拖拽到任意一个目标元素中：
核心是：通过事件捕获来获取当前被拖拽的元素；先存储起来，再通过事件捕获找到目标元素，然后再目标元素中使用开始被存储的值来添加元素。
```
<body>
	<div class="div1" id="div1">
		<p id="pe" draggable="true">试着把我拖过去</p>
	</div>
	<div class="div2" id="div2"></div>
	<script type="text/javascript">
		var obj = null;//定义当前被拖拽的元素
		//被拖拽元素
		document.ondragstart = function(e){
			// 通过事件捕获来获取当前被拖拽的元素；
			// e.target事件源对象
			e.target.style.opacity = '.5';
			e.target.parentNode.style.borderWidth = "3px";
			//将被拖拽的元素放到一个全局对象中保存，当拖拽的结束的时候添加到目标元素中。
			obj = e.target;
		}
		document.ondragend = function(e){
			e.target.style.opacity = '1';
			e.target.parentNode.style.borderWidth = "1px";
		}	
		// 拖拽目标
		document.ondragover = function(e){
			e.preventDefault();

		}
		document.ondrop = function(e){
			e.target.appendChild(obj);			
		}		
	</script>
</body>
```
当时这种情况有个问题：使用了一个全局变量obj；一般情况下我们不到最后的时候都不要使用全局变量，以为使用全局变量有两个问题：
1.不安全，全局变量任何人都能使用，你也可以该，我也可以该；
2.全局变量会导致内存泄漏；

为了解决上述问题 ，我们使用另外一种方式来存储这个全局对象；
通过dataTransfer来实现数据的存储和获取：

**通过事件对象e中的dataTransfer里的setData()来实现数据的存储和获取
setData(format,data);**
**format:数据类型，一般有两种：text/html、text/uri-list**
**data：数据:一般来说是字符串**
**这里设置的值，只能在ondrop里面取得；**

存储
```
e.dataTransfer.setData("text/html",e.target.id)
```
获取：
```
var id = e.dataTransfer.getData("text/html");
 e.target.appendChild(document.getElementById(id));  
```
完整代码：
```
<!DOCTYPE html>
<html>
<head>
	<title>demo</title>
	<style type="text/css">
		p{
			background-color: #888;
		}
		div{
			width: 200px;
			height: 200px;
			border: 1px solid red;
			float: left;
			margin-left: 50px;
		}
	</style>
</head>
<body>
	<div class="div1" id="div1">
		<p id="pe" draggable="true">试着把我拖过去</p>
	</div>
	<div class="div2" id="div2"></div>
	<script type="text/javascript">
			//被拖拽元素
		document.ondragstart = function(e){
			e.target.style.opacity = '.5';
			e.target.parentNode.style.borderWidth = "3px";
			obj = e.target;


			// 通过事件对象e中的dataTransfer里的setData()来实现数据的存储和获取
			// setData(format,data);
			// format:数据类型，一般有两种：text/html、text/uri-list
			// data：数据:一般来说是字符串
			//这里设置的值，只能再ondrop里面取得；
			e.dataTransfer.setData("text/html",e.target.id);
		}
		document.ondragend = function(e){
			e.target.style.opacity = '1';
			e.target.parentNode.style.borderWidth = "1px";
		}		

		// 拖拽目标
		document.ondragover = function(e){
			e.preventDefault();

		}
		document.ondrop = function(e){
			// 通过dataTransfer.setData()存储的数据只能再ondrop事件中获取；
			var id = e.dataTransfer.getData("text/html");
			e.target.appendChild(document.getElementById(id));			
		}		
	</script>
</body>
</html>
```
 

##地理定位
Geolocation（地理定位），用于获取用户位置的信息；

在H5规范中，增加获取用户地理定位信息的API，我们可以发送一个位置信息的请求，用户同意后，浏览器会返回一个包含经度和维度的位置信息！那么我们可以基于用户位置开发互联网应用，即基于位置服务；

了解获取位置的方式：
1.IP地址：任何能上网的电脑都可以，不够精确
2.GPS：精准，但是时间长，耗电。
3.WiFi：精准，但在乡村接入点少
4.手机信号：相当精准，但需要能够访问手机设备等
5.用户自定义：可能不够精准，特别是当用户位置改变。

注意：
浏览器是自动选择定位方式，我们无法设置；
浏览器默认地理位置为私密信息，所以浏览器会弹出一个请求，是否用户允许获取位置。

**语法：**
```
navigator.geolocation.getCurrentPosition(successCallback,errorCallback,option);
```
navigator.geolocation.getCurrentPosition(success,error,option);
第一个参数:success;获取当前地理信息成功时的回调
第二个参数:error;获取当前地理信息失败时的回调
第三个参数:option;可以设置获取数据的方式,如:
	enableHighAccuracy:true/false;表示是否使用高精度
	timeout:设置超时时间,单位ms;
	maximumAge:可以设置浏览器重新获取地理信息的时间间隔,单位也时ms;
	如:
```
navigator.geolocation.getCurrentPosition(showPosition,showError,{
	enableHighAccuracy:true,
	timeout:3000,
});
```
成功获取定位后的回调
当获取地理信息成功时, getCurrentPosition() 方法会返回一个对象,这个地理信息对象,会通过参数传递给成功后的回调,如下position就是代表获取成的地理信息对象
```
function showPosition(position){
div.innerHTML="Latitude:" + position.coords.latitude ;
}
```
注意：这个返回的地理信息对象会有一个坐标信息，对应很多属性:
coords.latitude	十进制数的纬度
coords.longitude	十进制数的经度
coords.accuracy	位置精度
coords.altitude	海拔，海平面以上以米计
coords.altitudeAccuracy	位置的海拔精度
coords.heading	方向，从正北开始以度计
coords.speed	速度，以米/每秒计
timestamp	响应的日期/时间

失败获取定位时回调,也会有一个对象，如下error
```
function showError(error){
		  switch(error.code) {
		    case error.PERMISSION_DENIED:
		      x.innerHTML="用户拒绝对获取地理位置的请求。"
		      break;
		    case error.POSITION_UNAVAILABLE:
		      x.innerHTML="位置信息是不可用的。"
		      break;
		    case error.TIMEOUT:
		      x.innerHTML="请求用户地理位置超时。"
		      break;
		    case error.UNKNOWN_ERROR:
		      x.innerHTML="未知错误。"
		      break;
		    }
 	    }
```
错误代码：
Permission denied - 用户不允许地理定位
Position unavailable - 无法获取当前位置
Timeout - 操作超时

代码：
```
script type="text/javascript">
		var div =document.getElementsClassName("demo")[0];
		function getLocation(){
			// 能力测试,看是否支持或者用户是否允许; 
			if (navigator.geolocation) {
				navigator.geolocation.getCurrentPosition(showPosition,showError,{});
			}else{
				x.innerHTML = "Geolocation is not supported by this browser";
			}
		}
		function showPosition(position){
			div.innerHTML="Latitude:" + position.coords.latitude + "<br/> Longitude:" + position.coords.longitude;
		}		
		function showError(error){
		  switch(error.code) {
		    case error.PERMISSION_DENIED:
		      x.innerHTML="用户拒绝对获取地理位置的请求。"
		      break;
		    case error.POSITION_UNAVAILABLE:
		      x.innerHTML="位置信息是不可用的。"
		      break;
		    case error.TIMEOUT:
		      x.innerHTML="请求用户地理位置超时。"
		      break;
		    case error.UNKNOWN_ERROR:
		      x.innerHTML="未知错误。"
		      break;
		    }
 	    }
	</script>
```
当既然我们个人无法获取地理信息，我们可以通过第三方的接口API来获取，如百度地图，谷歌地图;
例子：借助百度地图提供的接口，来实现当前地理定位：
可以查看：[百度地图开放平台 ](http://lbsyun.baidu.com/)
![image.png](https://upload-images.jianshu.io/upload_images/17785871-6efafe77a174704b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

很多都写好了
注意:一般需要密钥，即授权码
```
<script type="text/javascript" src="http://api.map.baidu.com/api?v=2.0&ak=您的密钥"></script>
```
```
<!DOCTYPE html>
<html>
<head>
	<title>普通地图&全景图</title>
	<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
	<script type="text/javascript" src="http://api.map.baidu.com/api?v=2.0&ak=您的密钥"></script>
	<style type="text/css">
		body, html{width: 100%;height: 100%;overflow: hidden;margin:0;font-family:"微软雅黑";}
		#panorama {height: 50%;overflow: hidden;}
		#normal_map {height:50%;overflow: hidden;}
	</style>
</head>
<body>
	<div id="panorama"></div>
	<div id="normal_map"></div>
	<script type="text/javascript">
	//全景图展示
	var panorama = new BMap.Panorama('panorama');
	panorama.setPosition(new BMap.Point(120.320032, 31.589666)); //根据经纬度坐标展示全景图
	panorama.setPov({heading: -40, pitch: 6});

	panorama.addEventListener('position_changed', function(e){ //全景图位置改变后，普通地图中心点也随之改变
		var pos = panorama.getPosition();
		map.setCenter(new BMap.Point(pos.lng, pos.lat));
		marker.setPosition(pos);
	});
	//普通地图展示
	var mapOption = {
			mapType: BMAP_NORMAL_MAP,
			maxZoom: 18,
			drawMargin:0,
			enableFulltimeSpotClick: true,
			enableHighResolution:true
		}
	var map = new BMap.Map("normal_map", mapOption);
	var testpoint = new BMap.Point(120.320032, 31.589666);
	map.centerAndZoom(testpoint, 18);
	var marker=new BMap.Marker(testpoint);
	marker.enableDragging();
	map.addOverlay(marker);  
	marker.addEventListener('dragend',function(e){
		panorama.setPosition(e.point); //拖动marker后，全景图位置也随着改变
		panorama.setPov({heading: -40, pitch: 6});}
	);
	</script>
</body>
</html>
```
