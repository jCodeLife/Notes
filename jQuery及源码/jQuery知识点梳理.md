分以下基本
#1. 概述
- jQuery是一个js函数库
- 操作DOM和jQuery对象
- 入口函数美元符号.(document).ready(),也可以缩写成$();
#2. DOM操作
###查找元素
- 基本选择器：
\#id
.class
\*
s1,s2  (群组)
- 层级选择器
p c (父元素下方的所有子元素)
p>c (父元素下方的直接子元素)
prev+next (当前元素之后的第一个)
prev~nextAll (当前元素之后的所有元素)
- 表单元素选择器
:text
:password
:radio
:checkbox
:submit
:reset
:image
:file
:hidden
:checked
:selected
:disabled
:enabled
:input
:button
- 属性选择器
[attribute] (包含某属性的所有元素)
[attribute=value] (属性等于某值的)
[attribute!=value] (属性不等于某值的)
[attribute^=value] (属性开头是某值的)
[attribute$=value] (属性结尾是某值的)
[attribute*=value] (属性包含某值的)
- 基本过虑选择器
:first  第一个
:last  最后一个
:even  偶数
:odd  奇数
:eq()  第几个
:gt()  大于多少
:lt()  小于多少
:not()  不是哪一个
- 子元素过虑选择器
:first-child  第一个孩子
:last-child  最后一个
:nth-child()  第几个
:only-child 仅有一个
- 内容过滤选择器
:contains(text)  内容包含text的
:has(selector)  内容包含什么元素的
:parent  父亲元素，即匹配含有子元素或者文本的元素
:empty  内容为空的
- 可见性过虑选择器
:visible  
:hidden

###操作元素

- 属性
attr()
- 内容
html()
text()
- 值
val()
- 样式
css()
addClass()
removeClass()
hasClass()
toggleClass()

###遍历元素

parent()  找父亲
children()  找孩子
find()  找
prev() 前一个
next()  后一个
prevAll()  前面所有的
nextAll()  后面所有的
siblings()  所有兄弟元素

###添加元素

append()  后面添加
prepend()  前面添加

###删除元素

remove() 移除
empty()  清空

###替换元素

replacewith(content)  所有元素替换为指定的内容
replaceAll(selector)  替换所有 selector匹配的元素

###克隆元素

clone()

#3. 事件处理

one()
bind()  
delegate()
click\mouserenter...()
...
on()

#4. 动画
###隐藏和显示
show()
hide()
toggle()

###收起和展开
slideUp()
sildeDown()
slideToggle()

###淡入和淡出

fadeIn()
fadeOut()
fadeToggle()

###动画
animate()
#5. AJAX
