CSS3 主要可以分为以下几个模块：
边框和背景，渐变，文字特效，字体，2D/3D转换，动画(过渡动画和动画)，多列布局，用户界面，选择器，盒模型

下面是用户界面相关：
在 CSS3 中, 增加了一些新的用户界面特性，来调整元素尺寸，框尺寸和外边框等。
主要重点：
- **box-sizing 盒子大小**
box-sizing：盒子的尺寸大小，也叫框大小或者盒模型。可以通过box-sizing属性设置元素的 width 和 height 是否包含了 padding 和 border。
通常，在默认情况下，元素的宽和高是不包括padding和border的，即：
**元素实际宽度= width(宽) + padding(内边距) + border(边框) 
元素实际高度 = height(高) + padding(内边距) + border(边框)**
这就意味着我们在设置元素的 width/height 时，元素真实展示的高度与宽度会更大。
```
所以，通常，下面的两个元素展示出来的大小是不一样的

.div1{
  width:100px;
  height:100px;

}
.div2{
  width:100px;
  width:100px;
  border:1px solid #333;
  padding:50px;
}
```
但在很多情况下，我们希望的是，我设置的宽高就是元素的实际宽高，不希望我在加入或者改变border和padding时，我的元素宽高就变了。那么我们可以使用，box-sizing属性来解决这样的问题。
```
下面两个元素所展示出来的大小是一样的。
.div1 {
    width: 300px;
    height:100px;
    border: 1px solid blue;
   box-sizing: border-box;
}

.div2 {
    width: 300px;
   height: 100px;
    padding: 50px;
   border: 1px solid red;
    box-sizing: border-box;
}
```
从结果上看 **box-sizing: border-box**; 效果很好，也正是我们需要的效果。
```
为所有元素使用 box-sizing ：
*{
  box-sizing:border-box;
}
```
box-sizing的语法：
```
语法:
div{
  box-sizing: content-box|border-box|inherit: 
}
```


还有两个稍微没那么重点的：
- resize 调整大小，表示是否由用户去调整元素大小，注：IE不支持
- outline-offset 轮廓偏移，并在超出边框边缘的位置绘制轮廓。，注：IE不支持
轮廓与边框有两点不同：
轮廓不占用空间
轮廓可能是非矩形


再下面还有一些，目前兼容性更不好的，与用户界面特性相关的属性，作为了解吧：
- appearance	使一个元素的外观像一个标准的用户界面元素，Firefox和IE完全不支持
- icon，所有主流浏览器都不支持
- nav-down	只有Opera支持
- nav-index	 只有 Opera 支持 
- nav-left	只有 Opera 支持 
- nav-right	只有 Opera 支持 
- nav-up	只有 Opera 支持 
