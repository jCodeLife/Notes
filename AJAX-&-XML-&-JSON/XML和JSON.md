在企业开发中，前端和后端交换数据的时候，一般都不会直接返回字符串，因为字符串容易出问题。而是返回XML或者JSON格式的数据。
#XML
XML 可扩展标记语言
XML 被设计用来传输和存储数据。
- XML格式：
第一行是 XML 声明：<?xml version="1.0" encoding="UTF-8"?>，它定义 XML 的版本 (1.0) 和所使用的编码 。
在XML中数据都是放在一对标签中的，标签名可以随意写。如下：
下一行描述文档的根元素<note>
接下来 4 行描述根的 4 个子元素（to, from, heading 以及 body）
最后一行定义根元素的结尾

注意：所有的数据必须有个根标签，如上note；
```
<?xml version="1.0" encoding="UTF-8"?>
<note>
<to>George</to>
<from>John</from>
<heading>Reminder</heading>
<body>Don't forget the meeting!</body>
</note>
```
XML 文档形成一种树结构
XML 文档必须包含根元素。该元素是所有其他元素的父元素。
XML 文档中的元素形成了一棵文档树。这棵树从根部开始，并扩展到树的最底端。
```
<root>
  <child>
    <subchild>.....</subchild>
  </child>
</root>
```
以上差不多就是XML的固定格式。
####那么后端如何返回一个XML数据给我们前端呢
JS端
```
window.onload = function(){
		var btn = document.querySelector(".btn");
		btn.onclick = function(){
			// 此处ajax是我自己封装的ajax方法
			ajax({
				type:"GET",
				url:"ajax-xml.php",
				success:function(xhr){//xhr表示调用时传来的异步对象
					// 通过xhr.ressponseXML来返回数据
					console.log(xhr.ressponseXML);//返回的是xml里的#document，可以使用DOM相关的方法来操作。
					var res = xhr.ressponseXML;
					console.log(res.querySelector("note").innerHTML);//比如这里查看note元素里面的内容。
				},
				error:function(xhr){//xhr表示调用时传来的异步对象
					console.log(xhr.status);
				}
			});
		}
	} 
```
PHP端
```
<?php
header(string:"content-type:text/xml;charset="utf-8");
 
echo file_get_contents(filename:"info.xml");
```
XML端

```
<?xml version="1.0" encoding="UTF-8"?>
<note>
<to>George</to>
<from>John</from>
<heading>Reminder</heading>
<body>Don't forget the meeting!</body>
</note>
```
1.**注意：如果执行结果有中文或者PHP中需要返回XML数据，那必须在PHP的文件内的顶部设置header(string:"content-type:text/xml;charset="utf-8");**
2.xhr表示调用时传来的异步对象
3.通过xhr.ressponseXML来获取返回的数据
4.返回的是xml里的#document，可以使用DOM相关的方法来操作。


#JSON
###简介
JSON：JavaScript 对象表示法（JavaScript Object Notation）。
JSON 是存储和交换文本信息的语法。类似 XML。
JSON 比 XML 更小、更快，更易解析。是轻量级的文本数据交换格式
JSON 独立于语言 
JSON 具有自我描述性，更易理解

JSON 使用 JavaScript 语法来描述数据对象，但是 JSON 仍然独立于语言和平台。JSON 解析器和 JSON 库支持许多不同的编程语言。

该格式由 Douglas Crockford 提出。
被设计用于可读的数据交换。
它是从 JavaScript 脚本语言中演变而来。
文件名扩展是 .json。
JSON 的网络媒体类型是 application/json。
统一标示符类型（Uniform Type Identifier）是 public.json。

##JSON 语法规则
1. 在 JS 语言中，一切都是对象。因此，任何支持的类型都可以通过 JSON 来表示，例如字符串、数字、对象、数组等。但是对象和数组是比较特殊且常用的两种类型
- 对象表示为键值对,数据由逗号分隔
 - 花括号保存对象,方括号保存数组
2. JSON 键/值对
```
{"name": "Json"}
```
3. JSON 与 JS 对象的关系
JSON 是 JS 对象的字符串表示法，它使用文本表示一个 JS 对象的信息，本质是一个字符串。
```
var obj = {a: 'Hello', b: 'World'}; //这是一个对象，注意键名也是可以使用引号包裹的

var json = '{"a": "Hello", "b": "World"}'; //这是一个 JSON 字符串，本质是一个字符串
```
4. JSON 和 JS 对象互转

**要实现从JSON字符串转换为JS对象，使用 JSON.parse() 方法：**
```
var obj = JSON.parse('{"a": "Hello", "b": "World"}'); //结果是 {a: 'Hello', b: 'World'}
```
**要实现从JS对象转换为JSON字符串，使用 JSON.stringify() 方法：**
```
var json = JSON.stringify({a: 'Hello', b: 'World'}); //结果是 '{"a": "Hello", "b": "World"}'
```

案例
 js中
```
window.onload = function(){
		var btn = document.querySelector(".btn");
		btn.onclick = function(){
			// 此处ajax是我自己封装的ajax方法
			ajax({
				type:"GET",
				url:"ajax-json.php",
				success:function(xhr){			
					console.log(xhr.ressponseText);					
				},
				error:function(xhr){//xhr表示调用时传来的异步对象
					console.log(xhr.status);
				}
			});
		}
	} 
```
ajax-json.txt文件中
```
{
  "firstName": "Brett", "lastName": "McLaughlin"
}
```
ajax-json.php文件中
```
<?php 
echo file_get_contents(filename:"ajax-json.txt");//返回
```

操作返回的部分
```
success:function(xhr){			
  var str = xhr.ressponseText;
  var obj = JSON.parse(str);//转成js对象
  console.log(obj);		//之后可以操作js对象
},
```

但是IE低级版本不支持parse方法，得用个框架兼容：json2.js，可以去github下载。使用也很简单。
