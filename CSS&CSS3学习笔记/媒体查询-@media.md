
`@media`的作用：`媒体查询可以在指定的设备上使用对应的样式替代原有的样式。`
可以简单理解为`告诉浏览器：当满足某条件时，调用某样式。`当满足条件A时，调用A样式；      当满足条件B时，调用B样式


1. 媒体查询可用于检测：
★viewport(视窗) 的宽度与高度
★设备的宽度与高度
★朝向 (智能手机横屏，竖屏) 。
★分辨率
2. 语法和操作符
`语法一：内联@media`
`@media  查询条件表达式｛ CSS样式 ｝`

```
@media not|only mediatype and (expressions) {...}
```
媒体查询由多媒体组成，可以包含一个或多个表达式，根据表达式条件判断是否成立，返回 true 或 false。
如果指定的多媒体类型匹配设备类型则返回查询结果为true，文档会在匹配的设备上显示指定样式效果。

可以使用`操作符` `not `或 `only` 或`and`或`，`限定。 
`and`:表示并且，要求必须满足所有的表达式要求时，才能使用media定义样式
`not`: 不，表示除…外，即排除掉某些特定的设备的，如 @media not print（非打印设备）
not 针对的是一整条媒体查询语句，而非其中的某一个条件
```
@media not print and(max-width:1024px){...}
或者
@media not(print and (max-width:1024px)){..}
```
`only`: 表示只有 仅仅，表示某一种的媒体类型设备。
对于支持Media Queries的移动设备来说，如果存在only关键字，移动设备的Web浏览器会忽略only关键字并直接根据后面的表达式应用样式文件。对于不支持Media Queries的设备但能够读取Media Type类型的Web浏览器，遇到only关键字时会忽略这个样式文件。
`,`多个条件设定使用逗号分隔，表手或者or，满足其中之一。


`方法二：外链 media属性`
`<link media=“查询条件表达式” />`
除了上述格式，也可以在不同的媒体上使用不同的样式文件，使用link外联引入：
```
<link rel="stylesheet" media="mediatype and|not|only (expressions)" href="print.css">
```
3. CSS3 `媒体类型`(mediatype)
`print`	打印机
**`screen`**	电脑屏幕，平板，智能手机等。
`speech	`语音合成器等发声设备
`all`	用于所有多媒体类型设备（默认）


4.常见媒体特性（属性）
`color`颜色
`color-index`	颜色索引
**`aspect-ratio`指定设备视口区域的宽高比**
```
@media only screen and (min-aspect-ratio:16/9){...}
```
`device-aspect-ratio`设备屏幕宽高比
`device-height`设备屏幕高度
`device-width`设备屏幕宽度
`grid`网格栅格
`scan`扫描
`height`高度
`monochrome`黑白
★**`orientation`方向**，横屏`landscape`还是竖屏`portrait`
```
@media (orientation:landscape){
	h1:before{
		content: '现在是横屏效果';
		color:green;
	}
}
@media (orientation:portrait){
	h1:before{
		content: '现在是竖屏效果';
		color:gold;
	}
}
```
★**`resolution`设备的分辨率范围**  分辨率(dpi),分辨率倍数(dppx),
```
@media screen and (resolution:2dppx){...}
@media screen and (resolution:3dppx){...}
@media screen and (min-resolution:2dppx){...}
```
★★**`width`视口宽度**  终端设备对页面的渲染区域
视口就是通常我们定义移动端头部meta的`viewport`
在浏览器窗口中，视口不包括滚动条、顶部或底部工具栏、菜单的部分
```
//在屏幕可视窗口尺寸大于 480 像素的设备上修改背景颜色:
@media screen and (min-width:480px){
  body{
    background-color:lightgreen;
  }
}

//在屏幕可视窗口尺寸大于 500 像素时将菜单浮动到页面左侧：
 @media screen and (min-width:500px){
  #leftsidebar{
    width:200px;
    float:left;
  }  
  #main{
    margin-left:200px;
  }
}
```


以上几乎所有的属性都可以使用【min-】和【max-】前缀做限定 （grid、scan和orientation除外）
max-color：最大颜色
max-color-index：最大颜色索引
max-aspect-ratio：最大宽高比
max-device-aspect-ratio：最大设备屏幕宽高比
max-device-height：设备屏幕的最大高度
max-device-width：	设备屏幕的最大宽度
max-height：	最大高度
max-monochrome：每个像素的最大单色原件个数
max-resolution：最大分辨率
max-width：最大宽度

min-color：最小颜色
min-color-index：最小颜色索引
min-aspect-ratio：最小宽高比
min-device-aspect-ratio：最小设备屏幕宽高比
min-device-height：设备屏幕的最小高度
min-device-width：	设备屏幕的最小宽度
min-height：	最小高度
min-monochrome：每个像素的最小单色原件个数
min-resolution：最小分辨率
min-width：最小宽度

5. 移动端配置媒体查询步骤：

（1）定义移动端视口，即设置好meta标签
```
<meta name="viewport" content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no"/>
```
`width=device-width`宽度等于当前设备的宽度
`initial-scale=1.0`  初始缩放比例
`minimum-scale`允许用户缩放到的最小比例
`maximum-scale`允许用户缩放到的最大比例
`user-scalable`用户是否可手动缩放
提示：手机系统默认会给予一定的视口宽度设置，并且允许用户进行页面缩放，这样一些未做移动端处理的PC网站也可以在手机上呈现（只不过是页面的内容会看上去很小）。因此我们设置meta的目的就是要修改默认设置，达到页面尺寸和移动端设备能匹配
（2）针对IE兼容处理
a. 为防止IE的实际浏览器模式默认较低，需要设置IE渲染方式为最新（ edge ）
```
<meta http-equiv="X-UA-Compatible" content="IE=edge">
```
b. IE9以下不支持HTML5、不支持CSS3 @Media，所以需要加载两个JS文件，来保证代码实现兼容
```
<!--[if lt IE 9]>
      <script src="https://cdn.bootcss.com/html5shiv/3.7.3/html5shiv.min.js"></script>
      <script src="https://cdn.bootcss.com/respond.js/1.4.2/respond.min.js"></script>
<![endif]-->

```
（3）规划移动端适配需求
主要根据项目需求而定，常见尺寸有320、480、640、768、960、1024、1200等![image.png](https://upload-images.jianshu.io/upload_images/17785871-7a0a71fc8873ad6e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



