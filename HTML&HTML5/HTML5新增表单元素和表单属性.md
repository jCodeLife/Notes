- **新表单元素**
<datalist>	选项列表。与 input 元素配合使用，定义 input 可能的值
<keygen>	用于表单的密钥对生成器字段
<output>	不同类型的输出，比如脚本的输出。

1. <datalist>
Safari和IE9以下不支持<datalist>,
<datalist>规定了输入域的选项内容 ，与input元素配合使用，定义input输入域的选项内容。
```
<form action="" method="">
<input list="browsers"><!-- 通过使用input里面的一个属性list，跟datalist的id相联系-->
<datalist id="browsers">
  <option value = "Internet Explorer">
  <option value = "Firefox">
  <option value = "Chrome">
  <option value = "Safari">
  <option value = "Opero">
</datalist>
</form>
```

2. <keygen>  
IE完全不支持
作用：提供一种验证用户的可靠方法  
用于表单的密钥对生成器字段,当提交表单时，会生成两个键，一个是私钥，一个公钥。
私钥（private key）存储于客户端，公钥（public key）则被发送到服务器。公钥可用于之后验证用户的客户端证书（client certificate）。  
```
<form action="" method="get">
  用户名: <input type="text" name="usr_name">
  加密: <keygen name="security">
  <input type="submit">
</form>
```

3. <output>
IE完全不支持
用于不同类型的输出，比如计算或脚本输出：
```
<form oninput="x.value=parseInt(a.value)+parseInt(b.value)">0
  <input type="range" id="a" value="50">100
  +<input type="number" id="b" value="50">
  =<output name="x" for="a b"></output>
</form>
```


- **新表单属性**
1. <form>新属性：
- **autocomplete 自动完成**
当用户在自动完成域中开始输入时，浏览器应该在该域中显示填写的选项。
autocomplete 适用于 <form> 标签，以及以下类型的 <input> 标签：text, search, url, telephone, email, password, datepickers, range 以及 color。
注：Opero不支持

```
<form action="" method="" autocomplete="on">
	FirstName:<input type="text" name="fname"><br>
	LastName:<input type="text" name="lname"><br>
	E-mail:<input type="email" name="email" autocomplete="off"><br>
	<input type="submit" name="">
</form>
```
![image.png](https://upload-images.jianshu.io/upload_images/17785871-43038548340e10ab.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- **novalidate不验证数据**
在提交表单时，不验证 form 或 input 里的东西。
如，在一般情况下，input的类型是email，会有验证：
![image.png](https://upload-images.jianshu.io/upload_images/17785871-de7a3afdac1b2bf6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
如果设置novalidate
```
<form action="" method="" novalidate="novalidate">
	E-mail:<input type="email" name="email">
	<input type="submit" name="">
</form>
```
![如果设置了novalidate，可以不验证，直接提交了](https://upload-images.jianshu.io/upload_images/17785871-30e27ae4c1275f63.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

注：Safari不支持
2. <input>新属性：
- **autocomplete 自动完成**
- autofocus 自动获得焦点  
```
FirstName:<input type = "text" name = "fname" autofocus/>
```
![在页面加载时，自动地获得焦点。](https://upload-images.jianshu.io/upload_images/17785871-4a575f88c7f52360.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- **form 所属哪个form 表单**
一般表单外的input字段使用form属性，来表示此input是哪个表单的一部分：
注意：IE不支持
```
<form action="" id="form1">
First name: <input type="text" name="fname"><br>
<input type="submit" value="提交">
</form>

<p> "Last name" 字段没有在form表单之内，但它也是form表单的一部分。当表当提交的时候会一起提交</p>

Last name: <input type="text" name="lname" form="form1">

<p><b>注意:</b> IE不支持form属性</p>
```
- **formaction** 用于**描述表单提交的URL地址**，会覆盖<form> 元素中的action属性.
用于input的type="submit" 和 type="image"的元素
以下表单包含了两个不同地址的提交按钮：
```
<form action="demo-form.php"> 
 First name: <input type="text" name="fname"><br> 
 Last name: <input type="text" name="lname"><br> 
 <input type="submit" value="Submit"><br> 
 <input type="submit" formaction="demo-admin.php" 
  value="Submit as admin"> 
</form> 
```
- **formenctype 表单提交到服务器的数据编码** (只对form表单中 method="post" 表单)
会覆盖 form 元素的 enctype 属性。
注意: 该属性与input的type="submit" 和 type="image" 配合使用。  
如：
```
<form action="demo-post_enctype.php" method="post"> 
 First name: <input type="text" name="fname"><br> 
 <input type="submit" value="Submit"> 
 <input type="submit" formenctype="multipart/form-data" 
  value="Submit as Multipart/form-data"> 
</form> 
```
第一个提交按钮已默认编码发送表单数据，第二个提交按钮以 "multipart/form-data" 编码格式发送表单数据
- **formmethod 表单提交方式**，会覆盖 <form> 的method 属性。
注意: 该属性可以与 type="submit" 和 type="image" 配合使用。
如：重新定义表单提交方式:
```
<form action="demo-form.php" method="get"> 
 First name: <input type="text" name="fname"><br> 
 Last name: <input type="text" name="lname"><br> 
 <input type="submit" value="Submit"> 
 <input type="submit" formmethod="post" formaction="demo-post.php" 
  value="Submit using POST"> 
</form>   
```
- **formnovalidate 表单提交无需被验证**，会覆盖 <form> 元素的novalidate属性.
注意: formnovalidate 属性与type="submit"一起使用
```
<form action=""> 
 E-mail: <input type="email" name="userid"><br> 
 <input type="submit" value="Submit"><br> 
 <input type="submit" formnovalidate value="Submit without validation"> <!-- 提交的时候不验证 -->
</form>   
```
- **formtarget 表单提交数据接收后，怎么的展示。** 
会覆盖 <form>元素的target属性.
注意: formtarget 属性与type="submit" 和 type="image"配合使用.
```
<form action="/statics/demosource/demo-form.php">
  First name: <input type="text" name="fname"><br>
  Last name: <input type="text" name="lname"><br>
  <input type="submit" value="正常提交">
  <input type="submit" formtarget="_blank" value="提交到一个新的页面上">
</form>
```
- **<input> height 和 width 属性，  仅用于<input> 标签type="image"的图像高度和宽度** 
注意: height 和 width 属性只适用于 image 类型的<input> 标签。
提示:图像通常会同时指定高度和宽度属性。如果图像设置高度和宽度，图像所需的空间 在加载页时会被保留。如果没有这些属性， 浏览器不知道图像的大小，并不能预留 适当的空间。图片在加载过程中会使页面布局效果改变 （尽管图片已加载）。
```
<form action="/statics/demosource/demo-form.php">
  First name: <input type="text" name="fname"><br>
  Last name: <input type="text" name="lname"><br>
  <input type="image" src="/statics/images/submit.gif"  alt="Submit" width="48" height="48">
</form>

```
- **list  表示input输入域的 datalist**（datalist 是输入域的选项列表）
```
<input list="browsers"> 

<datalist id="browsers"> 
  <option value="Internet Explorer"> 
  <option value="Firefox"> 
  <option value="Chrome"> 
  <option value="Opera"> 
  <option value="Safari"> 
</datalist> 
```
- **min  max step ** 用来给input 类型为数字或日期的添加限定约束的，最大最下值；
注意: min、max 和 step 属性适用于以下类型的 <input> 标签：date pickers、number 以及 range。
```
<!--Enter a date before 1980-01-01: -->
<input type="date" name="bday" max="1979-12-31"> 

<!--Enter a date after 2000-01-01: -->
<input type="date" name="bday" min="2000-01-02"> 

<!--Quantity (between 1 and 5): -->
<input type="number" name="quantity" min="1" max="5"> 
```
- **multiple 多种多样**表示<input> 元素中可选择多个值。  
注意: multiple 属性适用于以下类型的<input> 标签type="email" 和 type="file"
```
<form action="/statics/demosource/demo-form.php">
  选择图片: <input type="file" name="img" multiple>
  <input type="submit">
</form>

<p>尝试选取一张或者多种图片。</p>
```
- **pattern  正则表达式**用于验证<input> 元素的值。
注意:pattern 属性适用于以下类型的<input> 标签: text, search, url, tel, email, 和 password.
```
<!--一个只能包含三个字母的文本域（不含数字及特殊字符）：-->
Country code: <input type="text" name="country_code" pattern="[A-Za-z]{3}" title="Three letter country code">
```
- **placeholder 占位**提供一种提示（hint），描述输入域所期待的值。
注意: placeholder 属性适用于以下类型的<input> 标签：text, search, url, telephone, email 以及 password。
```
<input type="text" name="fname" placeholder="First name"> 
```
- **required 被要求的，必须的**，  规定必须在提交之前填写输入域（不能为空）。
注意:required 属性适用于以下类型的<input> 标签：text, search, url, telephone, email, password, date pickers, number, checkbox, radio 以及 file。
```
<!--不能为空的input字段:-->
Username: <input type="text" name="usrname" required>
```
- **step 步伐、一步、步长**，规定输入域合法的数字间隔
提示： step 属性可以与 max 和 min 属性创建一个区域值.
注意: step 属性与以下type类型一起使用: number, range, date, datetime, datetime-local, month, time 和 week.
```
<input type="number" name="points" step="3"> 
```
