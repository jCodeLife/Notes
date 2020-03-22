- 文本设置
1、font-size: 字号大小 
2、font-style: 字体格式
3、font-weight: 字体粗细
4、颜色属性color: 文本颜色

- 超链接设置
text-decoration: 参数
参数取值范围： 
underline：为文字加下划线 
overline：为文字加上划线 
line-through：为文字加删除线 
blink：使文字闪烁 
none：不显示上述任何效果

- 背景
1、背景颜色
background-color: 设置背景色
2、背景图片
background-image: url(URL)
URL就是背景图片的存放路径，none表示无。
3、背景图片重复
background-repeat: 参数
参数取值范围 ：
no-repeat：不重复平铺背景图片
repeat-x：使图片只在水平方向上平铺
repeat-y：使图片只在垂直方向上平铺
如果不指定背景图片重复属性，浏览器默认的是背景图片向水平和垂直两个方向平铺。
4、背景图片固定
background-attachment: 参数
背景图片固定控制背景图片是否随网页的滚动而滚动。如果不设置背景图片固定属性，浏览器默认背景图片随网页的滚动而滚动。为了避免过于花哨的背景图片在滚动时转移浏览者的注意力，一般都设为固定。
参数取值范围：
fixed：网页滚动时，背景图片相对于浏览器的窗口而言，固定不动
scroll：网页滚动时，背景图片相对于浏览器的窗口而言，一起滚动

- 区块
1、单词间距 
word-spacing: 单词间距 
2、字母间距 
letter-spacing: 字母间距
3、文本对齐
text-align: 参数
参数的取值：
left：左对齐
right：右对齐
center：居中对齐
justify：相对左右两端对齐
4、垂直对齐
vertical-align: 参数
top：顶对齐
bottom：底对齐
text-top：相对文本顶对齐
text-bottom：相对文本底对齐
baseline：基准线对齐
middle：中心对齐
sub：以下标的形式显示
super：以上标的形式显示
5、文本缩进
text-indent: 缩进距离
12px相当于一个文字距离
6、空格
white-space: 参数
参数取值范围： 
normal 默认，空白会被浏览器忽略
pre 保留空白
nowrap 文本不换行
7、显示样式 
display: 参数 
参数取值范围： 
block：块级元素，在对象前后都换行 
inline：在对象前后都不换行 
list-item：在对象前后都换行，增加了项目符号 
none：无显示

- 方框
1、height 高度
2、width 宽度
3、padding 内边距
4、margin 外边距
5、float（浮动）：可以让块级元素在一行中排列，例如横向菜单。 
6、clear 清除

- 边框
1、样式
border style 参数
边框样式的参数：
none：无边框 
dotted：边框为点线
dashed：边框为长短线
solid：边框为实线
double：边框为双线
2、宽度 border width 
3、颜色 border color

- 列表
list-style-type 列表样式
不同浏览器的列表符可能不相同，可能会影响到网页，所以网页中的列表大多都是由背景图片显示。
控制用户界面的样式

- 鼠标
cursor：鼠标形状参数 
CSS鼠标形状参数表： 
鼠标形状：CSS代码
style="cursor:hand" 　　　　　手形
style="cursor:crosshair" 　　十字形
style="cursor:text" 　　　　　文本形
style="cursor:wait" 　　　　　沙漏形
style="cursor:move" 　　　　十字箭头形：
style="cursor:help" 　　　　　问号形
style="cursor:e-resize" 　　　右箭头形
style="cursor:n-resize" 　　　上箭头形
style="cursor:nw-resize" 　　左上箭头形
style="cursor:w-resize" 　　　左箭头形
style="cursor:s-resize" 　　　下箭头形 
style="cursor:se-resize" 　　右下箭头形 
style="cursor:sw-resize" 　　左下箭头形



2. HTML常用代码
 ncontextmenu="window.event.returnValue=false" 将彻底屏蔽鼠标右键
<table borderncontextmenu=return(false)><td>no</table> 可用于Table

<body nselectstart="return false"> 取消选取、防止复制

onpaste="return false" 不准粘贴

oncopy="return false;" ncut="return false;" 防止复制

<link rel="Shortcut Icon"href="favicon.ico"> IE地址栏前换成自己的图标

<link rel="Bookmark"href="favicon.ico"> 可以在收藏夹中显示出你的图标

<inputstyle="ime-mode:disabled"> 关闭输入法

永远都会带着框架
<script. language="JavaScript"><!--
if (window == top)top.location.href = "frames.htm"; //frames.htm为框架网页
// --></script>

 防止被人frame.

<SCRIPT. LANGUAGE=JAVASCRIPT><!--
if (top.location != self.location)top.location=self.location;
// --></SCRIPT>

 网页将不能被另存为

<noscript><iframe.src=*.html></iframe></noscript>

 查看网页源代码

<input type=button value=查看网页源代码
onclick="window.location = "view-source:"+"[http://www.w3cschool.cn](hhttp://www.w3cschool.cn)"">

删除时确认

<a href="javascript:if(confirm("确实要删除吗?"))location="boos.asp? &areyou=删除&page=1"">删除</a>

屏蔽功能键Shift,Alt,Ctrl
<script>
function look(){
if(event.shiftKey)
alert("禁止按Shift键!");//可以换成ALT　CTRL
}
document.onkeydown=look;
</script>

 网页不会被缓存
<META. HTTP-EQUIV="pragma" CONTENT="no-cache">
<META. HTTP-EQUIV="Cache-Control"CONTENT="no-cache, must-revalidate">
<META. HTTP-EQUIV="expires"CONTENT="Wed, 26 Feb 1997 08:21:57 GMT">
或者<META. HTTP-EQUIV="expires"CONTENT="0">

怎样让表单没有凹凸感？
<input type=text style="border:1 solid #000000">
<input type=text style="border-left:none;border-right:none; border -top:none; border-bottom: 1 solid#000000"></textarea>

不要滚动条?
让竖条没有:
<body style="overflow:scroll;overflow-y:hidden">
</body>　　

让横条没有:
<body style="overflow:scroll;overflow-x:hidden">
</body>
两个都去掉？更简单了
<body scroll="no">
</body>

怎样去掉图片链接点击后，图片周围的虚线？

<a href="#"nFocus="this.blur()"><img src="logo.jpg"border=0></a>

电子邮件处理提交表单

<form. name="form1"method="post" action="mailt****@***.com"enctype="text/plain">
<input type=submit>
</form>

在打开的子窗口刷新父窗口的代码里如何写？
window.opener.location.reload()

如何设定打开页面的大小
<body nload="top.resizeTo(300,200);">
打开页面的位置<bodynload="top.moveBy(300,200);">

在页面中如何加入不是满铺的背景图片,拉动页面时背景图不动
<STYLE>
body
{background-image:url(logo.gif); background-repeat:no-repeat;
background-position:center;background-attachment: fixed}
</STYLE>

 检查一段字符串是否全由数字组成
<script. language="Javascript"><!--
function checkNum(str){return str.match(//D/)==null}
alert(checkNum("1232142141"))
alert(checkNum("123214214a1"))
// --></script>

获得一个窗口的大小
document.body.clientWidth; document.body.clientHeight

怎么判断是否是字符
if (/[^/x00-/xff]/g.test(s)) alert("含有汉字");
else alert("全是字符");

TEXTAREA自适应文字行数的多少
<textarea rows=1 name=s1 cols=27npropertychange="this.style.posHeight=this.scrollHeight">
</textarea>

 日期减去天数等于第二个日期
<script. language=Javascript>
function cc(dd,dadd)
{
//可以加上错误处理
var a = new Date(dd)
a = a.valueOf()
a = a - dadd * 24 * 60 * 60 * 1000
a = new Date(a)
alert(a.getFullYear() + "年" + (a.getMonth() +1) + "月" + a.getDate() + "日")
} cc("12/23/2002",2)
</script>

 选择了哪一个Radio
<HTML><script. language="vbscript">
function checkme()
for each ob in radio1
if ob.checked then window.alert ob.value
next
end function
</script><BODY>
<INPUT name="radio1" type="radio"value="style" checked>Style.
<INPUT name="radio1" type="radio"value="barcode">Barcode
<INPUT type="button" value="check"nclick="checkme()">
</BODY></HTML>

脚本永不出错
<SCRIPT. LANGUAGE="JavaScript">
<!-- Hide function killErrors(){return true;} window.onerror = killErrors;// -->
</SCRIPT>

ENTER键可以让光标移到下一个输入框
<input nkeydown="if(event.keyCode==13)event.keyCode=9">

来源于：[W3Cschool](https://www.w3cschool.cn/html/html-code.html)
