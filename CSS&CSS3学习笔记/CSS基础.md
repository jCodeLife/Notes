CSS Cascading Style Sheets 层叠样式表
1. 引入CSS
（1）行间样式
```
<div style="width:100....">
```
（2）页面级样式
```
<style type = "text/css">
  width:100px;
  height:100px;
  background:red;
</style>
```
（3）外部样式
```
<link rel:'stylesheet' type = "text/css" href="引用文件地址">
```
2.css注释
以 "/*" 开始, 以 "*/" 结束
```
/*这是个注释*/    
```
**3.选择器汇总：**
```
1.id选择器（#myid）

2.类选择器（.myclassname）

3.标签选择器（div,h1,p）

4.相邻选择器（h1+p） 指定元素的直接后继元素 所有h1标签后面的第一段

5.兄弟节点组合选择器（X ~ Y）会选择跟在X后面的所有Y元素

6.子选择器（ul > li）

7.后代选择器（li a）

8.通配符选择器（*）

9.属性选择器 X[title]]

10.属性值选择器X[href="foo"]属性值包含foo的

11.属性值开头的 X[href^="href"]

12.属性值以什么结尾的 X[href$=".jpg"]

13.伪类选择器
a:hover
input[type=radio]:checked
.clearfix:before
.clearfix:after
X:not(selector) 取反伪类,非
p::first-line 选中某标签的部分内容，如第一段或者d第一行、第一个字等。（伪标签是由两个冒号 :: 组成的。）
X:nth-child(n) 第几个子元素
X:nth-last-child(n) 倒数第几个子元素
X:nth-of-type(n) 根据元素的类型来进行选择，选中第几个X元素
X:nth-last-of-type(n) 倒数第几的x标签元素
X:first-child 第一个孩子
X:last-child 最后一个孩子
X:only-child  只有一个孩子的父标签
X:only-of-type 只有一个子标签的
X:first-of-type  选择指定标签的第一个兄弟标签

```

注：选择器之前不会覆盖，除非里面的值覆盖
**4. 选择器优先级**
选择器有存在优先级，
一般而言，选择器越特殊，它的优先级越高。也就是选择器指向的越准确，它的优先级就越高。
规则：
**!important > 行间样式  > ID > class | 属性 > 标签选择器 | 伪类选择器 > 通配符选择器**

**5.  选择器权重**
实际，权重表示的就是选择器优先级，各个选择器的权重如下：
```
CSS权重：
!important   Infinity
行间样式  1000
ID选择器 100
class类选择器 | 属性选择器 10
标签选择器 | 伪类选择器  1
通配符选择器 0
```
注意：
权重的数值是256进制；
其他复杂选择器（如：父子选择器，直接子元素选择器，并列选择器），只要写在同行的选择器，权重值等于各个简单的选择器的权重相加。

6. 元素分类
- 行内元素
如：span strong em a del...
特点：
（1）内容决定元素所占位置；
（2）不可以通过css改变宽高；
- 块级元素
如：div p ul li ol form address...
特点：
（1）独占一行；
（2）可以通过css改变宽高；
- 行级块元素
如：img...
特点：
（1）内容决定元素所占位置；
（2）可以通过css改变宽高；

注：
凡是带有inline属性的元素都有文字特性，就会被分割，如img，图片间有间隙，可以通过margin-left：-6px来处理。
可以用display来改变元素，inline/ inline-block / block

7. 盒子模型
Content（内容）
Padding（内边距）
Border（边框）
Margin（外边距）

padding和margin的值个数：
4个时：上，右，下，左；
3个时：上，左右，下；
2个时：上下，左右；
1个时：四个方向都一样

8. 定位
（1）position：absolute 绝对定位，表示可以被定位的元素：
top：距离上边
left：距离左边
right：距离右边
bottom：距离下边
被absolute绝对定位的元素特点：
- 脱离原来位置进行定位，其位置是根据最近有定位的父级进行定位，没有的话相对文档定位。

（2）position：relative;相对定位；
relative定位的元素特点：保留原来的位置进行定位，即相当于相对于自己原来的位置进行定位。

（3）position: fixed；固定定位

在有position的定位元素下，可以用z-index:设置元素在第几层显示，值越大，越靠近我们。

9. bfc
block format context 块级格式上下文
触发一个盒子的bfc的方式：
```
1.position:absolute;定位

2.display:inline-block;改变样式为行内块

3.float:left/right;浮动

4.overflow:hidden；溢出隐藏
```

10. 浮动模型
float:left/right
（1）可以让元素站队；
（2）浮动模型的本质是：浮动元素产生了浮动流；
所有产生了浮动流的元素，块级元素看不到他们，但产生了bfc的元素和文本类带有inline属性的元素以及文本都能看到浮动元素。

利用伪元素清除浮动流
```
.nav:after{
  content:'';
  display:block;
  clear:both/right/left
}
```
注意：
伪元素天生就存在任意一个元素里，
清除浮动使用者必须是块级元素；
有两个伪元素：
span：：before
span：：after

11. 凡是设置了position：absolute以及float：left/right的元素，实质内部自动变成了inline-block元素。
      凡是带有inline的元素都有文本的特点，叫文本类元素，包括inline和inline-block元素。

12. 溢出容器打点显示
```
white-space:nowrap;文字不换行
overflow:hidden;超出部分隐藏
text-overflow:ellipsis；打点
```

13. 一般行内元素只能嵌套行内元素，特别的：a标签不能嵌套a标签；
      一般块级元素可以嵌套任何元素，特别的：p标签不能嵌套块级元素；

