CSS3 主要可以分为以下几个模块：
边框和背景，选择器，盒模型，文字特效，2D/3D转换，动画，多列布局，用户界面
1.边框和背景
（1）边框新增属性
- border-radius 设置圆角
```
div { 
border:2px solid; 
border-radius:25px; 
}

border-radius值个数：
四个值: 左上，右上，右下，左下。
三个值: 左上, 第二个值为右上和左下，右下
两个值: 左上与右下，右上与左下
一个值： 四个圆角值相同

可以拆为：
border-top-left-radius	定义了左上角的弧度
border-top-right-radius	定义了右上角的弧度
border-bottom-right-radius	定义了右下角的弧度
border-bottom-left-radius	定义了左下角的弧度
```

```
图片圆角
.img {
    border-radius: 8px;
}

.img2 {
    border-radius: 50%;
}
```

```
缩略图
img{
  border:1xp solid #ddd;
  border-radius:4px;
  padding:5px;
}
```

- box-shadow 设置阴影
```
div{ 
box-shadow: 10px 10px 5px #888888; 
}

全：
box-shadow: h-shadow v-shadow blur spread color inset;
水平和垂直方向阴影必须写。
```
- border-image  设置图片边框
```
div { 
border-image:url(border.png) 30 30 round; 
-webkit-border-image:url(border.png) 30 30 round; /* Safari 5 and older */ 
-o-border-image:url(border.png) 30 30 round; /* Opera */ 
}
```

（2）背景新增
- background-image 添加背景图片
```
#example1 {
    background-image: url(img_flwr.gif), url(/paper.gif);
    background-position: right bottom, left top;
    background-repeat: no-repeat, repeat;
    padding: 15px;
}

#example1 { 
background: url(img_flwr.gif) right bottom no-repeat, url(paper.gif) left top repeat; 
}
```
- background-size 设置背景大小
```
div { 
background:url(img_flwr.gif); 
background-size:80px 60px; 
background-repeat:no-repeat; 
}
```
- background-origin 设置背景图像的位置区域
```
div{
	border:1px solid black;
	padding:35px;
	background-image:url('/statics/images/course/smiley.gif');
	background-repeat:no-repeat;
	background-position:left;
}
#div1{
	background-origin:border-box;
}
#div2{
	background-origin:padding-box,;
}
#div3{
	background-origin:content-box;
}
```
- background-clip 设置从哪个位置开始绘制
```
#example1 {
    border: 10px dotted black;
    padding:35px;
    background: yellow;
}

#example2 {
    border: 10px dotted black;
    padding:35px;
    background: yellow;
    background-clip: padding-box;
}

#example3 {
    border: 10px dotted black;
    padding:35px;
    background: yellow;
    background-clip: content-box;
}
```
