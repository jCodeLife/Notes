1. 网络状态改变事件接口

ononline:当网络连通的时候触发此事件
 ```
window.addEventListener("online",function(){
	console.log("网络连通了！");
});		
```
onoffline:当网络断开时触发此事件
```
window.addEventListener("offline",funciton(){
	console.log("网络连通了！");
});
```
2. 全屏接口API，实现元素全屏效果

全屏操作的主要方法和属性
- requestFullScreen():开启全屏显示
注意：不同浏览器需要添加不同的前缀：webkit / moz / ms / o;
如div.webkitRequestFullScreen();
使用能力测试,兼容不同浏览器，这里添加的前缀；
```
<script>
if (div.requestFullScreen) {
	div.requestFullScreen();
}else if (div.webkitRequestFullScreen) {
	div.webkitRequestFullScreen();
}else if (div.mozRequestFullScreen) {
	div.mozRequestFullScreen()
}else if (div.msRequestFullScreen) {
	div.msRequestFullScreen()
}else(div.oRequestFullScreen) {
	div.oRequestFullScreen();
}
</scirpt>
```

- cancelFullScreen():退出全屏
也需要能力测试兼容各个浏览器
需要添加在document上退出
-   fullScreenElement:是否是全屏状态
也只能使用document进行判断
```
<body>
	<div>
		<img src="./Hydrangeas.jpg" alt="">
		<input type="button" id="full" value="全屏">
		<input type="button" id="canceFull" value="退出全屏">
		<input type="button" id="isFull" value="是否全屏">
	</div>
	<script type="text/javascript">
			window.onload=function(){
			var div = document.querySelector('div');
			//全屏操作
			document.querySelector('#full').onclick = function(){
				if (div.requestFullScreen) {
					div.requestFullScreen();
				}else if (div.webkitRequestFullScreen) {
					div.webkitRequestFullScreen();
				}else if (div.mozRequestFullScreen) {
					div.mozRequestFullScreen();
				}else if (div.msRequestFullScreen) {
					div.msRequestFullScreen();
				}else{
					div.oRequestFullScreen();
				}
			}
			//退出全屏
			document.querySelector('#canceFull').onclick = function(){
				if (document.cancelFullScreen) {
					document.cancelFullScreen();
				}else if (document.webkitCancelFullScreen) {
					document.webkitCancelFullScreen();
				}else if (document.mozCancelFullScreen) {
					document.mozCancelFullScreen();
				}else if (document.msCancelFullScreen) {
					document.msCancelFullScreen();
				}else{
					document.oCancelFullScreen();
				}
			}
			//判断是否是全屏
			document.querySelector('#isFull').onclick= function(){
				if (document.fullScreenElement || document.webkitFullScreenElement || document.mozFullScreenElement || document.msFullScreenElement || document.oFullScreenElement) {
					console.log('显示是全屏！');
				}else{
					console.log('显示不是全屏！');
				}
			}
		}
	</script>
</body>
```
3. 使用文件读取接口，实现文件读取预览效果

- FileReader:读取文件内容，可以用来创建读取文件的对象；
- readAsText()：读取文本文件（可以使用txt打开的文件），返回文本字符串，默认编码UTF-8;
- readAsBinaryString()：读取任意类型的文件。返回二进制字符串。通常这个方法不是用来读取文件展示给用户看，而是存储文件。例如：读取文件的内容，获取二进制数据，传递给后台，后台接受数据之后，再将数据存储。
- readAsDataURL()：读取文件获取一段以data开头的字符串，这个字符串本质就是DataURL，DataURL是一种将文件（一般就是指图像或者能够嵌入到文档的文件格式）嵌入到文档的方案（如展示图片）
展示图片
src：指定路径（资源定位：url），src请求的是外部文件，一般来说是服务器资源，意味着它需要向服务器发送请求，它占用服务器资源（另外雪碧图也是为了少占用资源）。DataURL是将资源转换为base64的字符串（base64是一种编码），并且将这些内容直接存储在url中。本身目的：优化网站的加载速度和执行效率。
- abort():中断读取；
通常，当我们选择文件如图片的时候有一个预览，而不是这样子：
![选定图片后只有一个文件名，这不是我们想要的](https://upload-images.jianshu.io/upload_images/17785871-68b94cd9bef8f4b3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
例子：
需求：即时预览；
步骤
即时：当用户选择图片后，立即有个预览
预览：通过文件读取对象的readAsDataURL()完成
代码：
```
!DOCTYPE html>
<html>
<head>
	<title>demo</title>
</head>
<body>
	<form action="">
		文件：<input type="file" name="myFile" id="myFile" onchange="getFileContent()">
		<input type="submit">
	</form>
	<img src="">
	<script type="text/javascript">
		function getFileContent(){
			// 1.创建文件读取对象
			var reader = new FileReader();
			// 2.读取文件，获取DataURL
			//readAsDataURL([Blob] blob)(FileReader) void;
			// 注意：
			// (1)通过readAsDataURL来读取文件的时候，没有任何返回值，是void。但是读取完文件之后（所以我们需要监听文件是否读取结束,FileReader提供了完整的事件处理模型），它会把读取的结果存储在文件读取对象的result中;
			// (2)需要传递一个参数blob即（binary large object 二进制的大文件，一般是图片或者其他可以嵌入到文档的类型）
			// (3)文件存储在file表单元素的files中，是一个数组
			var file = document.querySelector("#myFile").files[0];
			// console.log(file);
			reader.readAsDataURL(file);
			// 获取数据
			// FileReader提供了完整的事件处理模型，用来捕获读取文件时的状态：
			// onabort:读取文件中断时触发；
			// onerror:读取错误时触发；
			// onload:文件读取成功完成时触发；
			// onloadend:文件读取完成时触发，无论成功还是失败
			// onloadstart：开始读取文件时
			// onprogress：读取文件过程中持续触发
			reader.onload = function(){
				// console.log(reader.result);
				// 展示
				document.querySelector('img').src = reader.result;
			}
		}

	</script>
</body>
</html>
```
![方框后面的那一段就是读取到的文件](https://upload-images.jianshu.io/upload_images/17785871-925f080bc26d8a94.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![最后显示](https://upload-images.jianshu.io/upload_images/17785871-6eab55949a671497.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

