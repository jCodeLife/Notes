
`多列布局`是专门针对于文本（图文）排版的一种布局形式，作用对象是容器中的内容数据。
常见应用于电子杂志、阅读APP类型的项目
兼容性较好，IE10+及现代浏览器都支持（加前缀）

相关属性：
- `column-count` 列数，表示分几列
```
例如：将div文本划分为3列
div{
  -moz-column-count:3;/* Firefox*/
  -webkit-column-count:3;/* Safari and Chrome */
  column-count:3;
}
```
column-count的默认值auto不代表单列1，是指按照列的宽度，自动去适配列的数量。
- `column-width` 列的(最小)宽度,注：值不能使用百分比 不能是负数
```
div
{
 column-width:100px;
 -moz-column-width:100px; /* Firefox */
 -webkit-column-width:100px; /* Safari 和 Chrome */
}
```
column-width的默认值auto不代表单列宽，是指按照列的数量，自动去适配列的宽度。

column-width  和  column-count 注意事项：
通常情况下，只需要设定两者之一即可…
两者相辅相成，在默认值auto情况下，相互以对方为依据进行平衡调节
如果两者发生冲突，则以满足width的前提条件下，再确定count…

- `columns`	复合属性，可以设置列宽和列数 注：值不能使用百分比 不能是负数
```
div{
  columns:100px 3;
  -webkit-columns:100px 3;/*Safari and Chrome*/
  -moz-columns:100px;/* Firefox */
}
```
★ `column-gap` 多列之间的间距
```
例如：列的间隙为40px
div{
  -moz-column-count:3;
  -webkit-column-count:3;
  column-count:3;

  -moz-column-gap:40px;
  -webkit-column-gap:40px;
  column-gap:40px;
}
```
- `column-rule` 
定义多列之间的间距样式
设置列中之间的宽度，样式和颜色
复合属性，玩法等同于border
由column-rule-width / column-rule-style / column-rule-color 三部分组成
呈现为单边框，由间距中线向两侧延展
column-width宽度是视觉呈现的宽度，不占据真实空间

```
div
{
 -moz-column-rule:3px outset #ff00ff; /* Firefox */
 -webkit-column-rule:3px outset #ff00ff; /* Safari and Chrome */
 column-rule:3px outset #ff00ff;
}
```
- `column-rule-width` 列中之间的宽度
- `column-rule-style` 列中之间的样式
取值可以是none、 hidden、 dotted、	dashed、 solid、 double、 groove、	 ridge、 inset 、outset；
- `column-rule-color` 列中之间的颜色


- `column-fill`	
定义文本数据填充列方式（列高度对齐）
2个值：balance（平衡） /  auto（自动）
balance值：默认，以适应多列等高为目的
auto值：以适应容器高度为目的

- `column-span`	
定义对象是否跨列 
2个值：none（不跨列） / all（跨所有列）
适用于多列布局中的block对象
不限制对象在布局容器中的位置
跨列对象的前后，会按照定义来分配多列

下面有还有一些兼容性不太好的多列属性：
- `break-*系列`
定义对象的换行断裂点，从断裂点位置来产生新列
种断点位置对应3个属性：
对象之前（break-before  / column-break-before  /  -webkit- column-break-before ） 
对象之后（break-after  / column-break-after  / -webkit-column-break-after）
对象内部（break-inside  / column-break-inside  / -webkit-column-break-inside）
3个值：auto（自动判断）   /   always（断裂且生成新列）  /  avoid  （不断裂）


