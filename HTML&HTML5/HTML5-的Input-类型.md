本文来自：[W3School](https://www.w3cschool.cn/ldt2ek/2s4p1ppx.html)
一、文本类
- Text，文本
- Url，网络地址
- Password，密码
- Email，邮箱地址

二、操作类
- Checkbox ，复选框
- Radio，单选框
- File，上传文件
- Number，数值
- Range，百分百滑动条

三、功能类
- Button，按钮
- mage，图片提交按钮
- Submit，文字提交按钮
- Reset，重置表单



四、Date类
- Date，年月日控件
- Month，年月控件
- Week，年周控件
- Time，时间控件
- Datetime，年月日+时间控件
- Datetime-local，本地年月日+时间控件



五、特殊类
- Hidden，隐藏信息

 

扩展：

1.文本类属性：placeholder。这是一个占位符，可以作为提示信息，而且无法被用户选中。

2.Url和e-mail，在H5中，会在提交表单的时候检测其格式是否书写正确。

3.操作类。一般input标签会结合label标签使用，label一般有两种书写方法：
①非跨度：<label><input></input></label>

②跨度：<label for="input_id"></label>
　　　　<input id="input_id"></input>
如果网页结构中，input和label是相邻的关系，可以直接使用非跨度的书	写方法，以减少代码量。

4.file。在实际应用中，网页表单中需要上传的文件一般不止一个，这时候就要用到multiple属性，它是一个布尔值属性，在添加这个属性后，就可以上传多个属性。另外，上传的文件可以被规定，使用accept属性。这个一个数组属性，属性值是MIME规定的文件类型。

5.Button。Button类型只能在value中定义按钮上显示的提示文字。Image类型只能在src中链接图片。
而button标签则结合了button和image的属性，它是一个双标签，也就是说它可以在内部嵌套其他标签，让按钮的显示效果更多元化。

6.Date类。Date类型的input标签是H5中新增加的。它实际上是一个控件，可以很方便的选择和显示时间数据，但是目前支持该控件的浏览器并不多。其中IE是完全不支持的。

7.Hidden。这个属性的input标签无法显示，也无法被用户控制。它的作用可以用来标记一些隐藏的表单信息。
例如：在一些网站中，对于用户的描述，有一个信息完整度的提示。
用户在注册的时候，必填项有5个，可填项有5个。注册的表单可以用hidden来记录可填项中有多少个是有数据的。
假如，一个用户把所有的可填项全部填写。那么他的信息完整度就是100%。
另一个用户的可填项一个也没有填写，他的信息完整度就是50%。
而这个数值可以根据hidden中记录的数值来进行计算。





HTML5新增的8类INPUT输入类型介绍
已经有的输入类型 HTML代码示例：
代码如下:

文本域 <input type="text">
单选按钮 <input type="radio">
复选框 <input type="checkbox">
下拉列表 <select><option>
密码域 <input type="password">
提交按钮 <input type="submit">
可单击按钮 <input type="button">
图像按钮 <input type="image">
隐藏域 <input type="hidden">
重置按钮 <input type="reset">
文件域 <input type="file">
    
在HTML5中，增加了多个新的表单input输入类型，通过使用这些新增元素，可以实现更好的输入控制和验证。
1、email类型的应用
email类型的input元素是一种专门用于输入E-mail地址的文本输入框，在提交表单的时候，会自动验证email输入框的值。

代码如下:

<input type="email" name="user_email" />




2、url类型的应用
url类型的input元素提供用于输入url地址这类特殊文本的文本框。

代码如下:

<input type="url" name="user_url" />




3、number类型的应用
number类型的input元素提供用于输入数值的文本框。

代码如下:

<input type="number" name="number1" min="1" max="20" step="4" />




4、range类型的应用
range类型的input元素提供用于输入包含一定范围内数字值得文本框，在网页中显示为滚动条。

代码如下:

<input type="range" name="range1" min="1" max="30" />




5、日期检出类型的应用
输入类型 HTML代码  功能说明

代码如下:

date <input type="date">

选取日、月、年
month <input type="month">
选取月、年

代码如下:

week <input type="week">

选取周和年

码代码如下:

time <input type="time">

选取时间（小时和分钟）

代码如下:

datetime <input type="datetime">

选取时间、日、月、年（UTC时间）

代码如下:

datetime-local
<input type="datetime-local"> 选取时间、日、月、年（本地时间）




6、search类型的应用
search类型的input元素提供用于输入搜索关键词的文本框。

代码如下:

<input type="search" name="search1" />
input[type="search"]{
-webkit-appearance:textfield;
}




7、tel类型的应用
tel类型的input元素提供专门用于输入电话号码的文本框。

代码如下:

<input type="tel" name="tel" />




8、color类型的应用
color类型的input元素提供专门用于设置颜色的文本框。

代码如下:

<input type="color" name="color" />
