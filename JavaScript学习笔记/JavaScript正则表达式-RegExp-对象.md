作用：匹配特殊字符或有特殊搭配原则的字符。

##创建方法

1. 直接量
```
格式：/pattern/attributes
var reg = /abc/g
```

2. 创建RegExp对象
```
格式：new RegExp(pattern,attributes);

如：var reg = new RegExp("abc","g");

>  1. 参数
第一个参数：pattern 是一个字符串，指定了正则表达式的模式或其他正则表达式；
第二个参数：attributes 是一个可选的字符串，包含 "g"、"i" 和 "m";
"g"、"i" 和 "m"分别表示全局匹配、区分大小写的匹配和多行匹配。
> 2. 返回值
返回一个具有指定模式和标志的新RegExp对象;
当 pattern 是非合法的正则，或 attributes 含有 "g"、"i" 和 "m" 之外的字符时会抛出SyntaxError。
```
##方括号[]
 查找某个范围内的一个字符
```
[abc]	查找方括号之间的任何字符
[^abc]	查找任何不在方括号之间的字符
[0-9]	查找任何从 0 至 9 的数字
[a-z]	查找任何从小写 a 到小写 z 的字符
[A-Z]	查找任何从大写 A 到大写 Z 的字符
[A-z]	查找任何从大写 A 到小写 z 的字符
[adgk]	查找给定集合内的任何字符
[^adgk]	查找给定集合外的任何字符
(red|blue|green)	查找任何指定的选项
```
##元字符
元字符（Metacharacter）是拥有特殊含义的字符：
```
.	查找一个字符，除了换行和行结束符
\w	查找单词字符
\W	查找非单词字符
\d	查找数字
\D	查找非数字字符
\s	查找空白字符
\S	查找非空白字符
\n	查找换行符
\f	查找换页符
\r	查找回车符
\t	查找制表符
```
##量词
表示匹配字符的数量
```
n+	匹配任何包含至少一个 n 的字符串
n*	匹配任何包含零个或多个 n 的字符串
n?	匹配任何包含零个或一个 n 的字符串
n{X}	匹配包含 X 个 n 的序列的字符串
n{X,Y}	匹配包含 X 至 Y 个 n 的序列的字符串
n{X,}	匹配包含至少 X 个 n 的序列的字符串
n$	匹配任何结尾为 n 的字符串
^n	匹配任何开头为 n 的字符串
?=n	匹配任何其后紧接指定字符串 n 的字符串
?!n	匹配任何其后没有紧接指定字符串 n 的字符串
```
##RegExp 对象方法
```
compile	编译和改变正则
exec 检索字符串中指定的值。返回找到的值，并确定其位置。
test 检索字符串中指定的值。返回 true 或 false。
```

## String 对象中支持正则的方法
```
search	检索与正则相匹配的值
match	找到一个或多个正则的匹配
replace	替换与正则匹配的子串
split	把字符串分割为字符串数组
```
##常用的经典Javascript正则表达式
```
匹配中文字符的正则表达式：
[\u4e00-\u9fa5]

匹配双字节字符(包括汉字在内)：
[^\x00-\xff]

应用：计算字符串的长度（一个双字节字符长度计2，ASCII字符计1）
String.prototype.len=function(){ return this.replace([^\x00-\xff]/g,"aa").length; }

匹配空行的正则表达式：
\n[\s|]*\r

匹配HTML标记的正则表达式：
/<(.*)>.*<\/\1>|<(.*) \/>/

匹配首尾空格的正则表达式：
(^\s*)|(\s*$)

应用：实现trim函数，去掉字符串两端的空格
String.prototype.trim = function(){ return this.replace(/(^\s*)|(\s*$)/g, "");}

匹配IP地址的正则表达式
/(\d+)\.(\d+)\.(\d+)\.(\d+)/g

匹配Email地址的正则表达式
\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*

匹配网址URL的正则表达式：
http://([\w-]+\.)+[\w-]+(/[\w- ./?%&=]*)?

匹配非负整数（正整数 + 0）
^\d+$

匹配正整数
^[0-9]*[1-9][0-9]*$

匹配非正整数（负整数 + 0）
^((-\d+)|(0+))$

匹配负整数
^-[0-9]*[1-9][0-9]*$

匹配整数
^-?\d+$

匹配非负浮点数（正浮点数 + 0）
^\d+(\.\d+)?$

匹配正浮点数
^(([0-9]+\.[0-9]*[1-9][0-9]*)|([0-9]*[1-9][0-9]*\.[0-9]+)|([0-9]*[1-9][0-9]*))$

匹配非正浮点数（负浮点数 + 0）
^((-\d+(\.\d+)?)|(0+(\.0+)?))$

匹配负浮点数
^(-(([0-9]+\.[0-9]*[1-9][0-9]*)|([0-9]*[1-9][0-9]*\.[0-9]+)|([0-9]*[1-9][0-9]*)))$

匹配浮点数
^(-?\d+)(\.\d+)?$

匹配由26个英文字母组成的字符串
^[A-Za-z]+$

匹配由26个英文字母的大写组成的字符串
^[A-Z]+$

匹配由26个英文字母的小写组成的字符串
^[a-z]+$

匹配由数字和26个英文字母组成的字符串
^[A-Za-z0-9]+$

匹配由数字、26个英文字母或者下划线组成的字符串
^\w+$

匹配email地址
^[\w-]+(\.[\w-]+)*@[\w-]+(\.[\w-]+)+$

匹配url
^[a-zA-z]+://匹配(\w+(-\w+)*)(\.(\w+(-\w+)*))*(\?\S*)?$

匹配html tag
<\s*(\S+)(\s[^>]*)?>(.*?)<\s*\/\1\s*>
```
