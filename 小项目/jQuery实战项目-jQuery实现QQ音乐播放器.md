1. 页面布局
1.1 首先将页面划分为header、content、footer三大部分
1.2 content和footer区域，其内容是居中对齐的，里面的区域就叫content-in和footer-in，如下：![structure.png](https://upload-images.jianshu.io/upload_images/17785871-8e03b37c27e03d3d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
1.3 结构代码
HTML结构
```
html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<link rel="stylesheet" type="text/css" href="main.css">
	<title>QQ音乐播放器</title>
</head>
<body>
	<!-- 头部 -->
	<div class="header"></div>
	<!-- 中间内容区域 -->
	<div class="content">
		<div class="content_in"></div>
	</div>
	<!-- 尾部区域 -->
	<div class="footer">
		<div class="footer_in"></div>
	</div>
</body>
</html>
```
css
```
*{
	margin: 0;
	padding: 0;
}
.header{
	width: 100%;
	height: 45px;
	border: 1px solid red;
}
.content{
	width: 100%;
	height: 460px;
	border: 1px solid green;
}
.content .content_in{
	width: 1200px;
	height: 100%;
	margin: 0 auto;
	background: pink;
}
.footer{
	width: 100%;
	height: 60px;
	position: absolute;
	left: 0;
	bottom: 0;
	border: 1px solid #f44;
}
.footer .footer_in{
	width: 1200px;
	height: 100%;
	margin: 0 auto;
	background: red;
}
```
2.  header部分
header可以分为左边logo，右边一个ul,分别左浮右浮；
其中logo 和登录 注册，鼠标进入时高亮，客户端下载的背景再移入时颜色会更深一点。
![header](https://upload-images.jianshu.io/upload_images/17785871-9718eb079ca6fc1c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
3. content部分
content中的content_in主要分成左边和右边两部分，如图：![content](https://upload-images.jianshu.io/upload_images/17785871-7d8a17087b682dd6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
而左边可分为上和下两部分![image.png](https://upload-images.jianshu.io/upload_images/17785871-3bf7e2a41d3194e8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


