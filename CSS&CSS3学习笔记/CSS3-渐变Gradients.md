CSS3 主要可以分为以下几个模块：
边框和背景，渐变，文字特效，选择器，盒模型，2D/3D转换，动画，多列布局，用户界面
下面接着是渐变的知识点：
1. 渐变分类：
线性渐变（Linear Gradients）- 向下/向上/向左/向右/对角方向
径向渐变（Radial Gradients）- 由它们的中心定义

2.线性渐变：
为了创建一个线性渐变，你必须至少定义两种颜色，同时，也可以设置一个起点和一个方向（或一个角度）；
语法：
```
background:linear-gradients(direction,color1,color2...);
```
线性渐变 - 从上到下（默认情况下）
```
#grad1 {
    height: 200px;
    background: -webkit-linear-gradient(red, blue); /* Safari 5.1 - 6.0 */
    background: -o-linear-gradient(red, blue); /* Opera 11.1 - 12.0 */
    background: -moz-linear-gradient(red, blue); /* Firefox 3.6 - 15 */
    background: linear-gradient(red, blue); /* 标准的语法（必须放在最后） */
}
```
线性渐变 - 从左到右
```
#grad { 
  background: -webkit-linear-gradient(left, red , blue); /* Safari 5.1 - 6.0 */ 
  background: -o-linear-gradient(right, red, blue); /* Opera 11.1 - 12.0 */ 
  background: -moz-linear-gradient(right, red, blue); /* Firefox 3.6 - 15 */ 
  background: linear-gradient(to right, red , blue); /* 标准的语法 */ 
}
```
线性渐变 - 对角
```
#grad { 
  background: -webkit-linear-gradient(left top, red , blue); /* Safari 5.1 - 6.0 */ 
  background: -o-linear-gradient(bottom right, red, blue); /* Opera 11.1 - 12.0 */ 
  background: -moz-linear-gradient(bottom right, red, blue); /* Firefox 3.6 - 15 */ 
  background: linear-gradient(to bottom right, red , blue); /* 标准的语法 */ 
}
```
也支持透明度（transparency）
```
#grad { 
  background: -webkit-linear-gradient(left,rgba(255,0,0,0),rgba(255,0,0,1)); /* Safari 5.1 - 6 */ 
  background: -o-linear-gradient(right,rgba(255,0,0,0),rgba(255,0,0,1)); /* Opera 11.1 - 12*/ 
  background: -moz-linear-gradient(right,rgba(255,0,0,0),rgba(255,0,0,1)); /* Firefox 3.6 - 15*/ 
  background: linear-gradient(to right, rgba(255,0,0,0), rgba(255,0,0,1)); /* 标准的语法 */ 
}
```

重复的线性渐变
```
#grad1 {
    height: 200px;
    background: -webkit-repeating-linear-gradient(red, yellow 10%, green 20%); /* Safari 5.1 - 6.0 */
    background: -o-repeating-linear-gradient(red, yellow 10%, green 20%); /* Opera 11.1 - 12.0 */
    background: -moz-repeating-linear-gradient(red, yellow 10%, green 20%); /* Firefox 3.6 - 15 */
    background: repeating-linear-gradient(red, yellow 10%, green 20%); /* 标准的语法（必须放在最后） */
}
```

3. CSS3 径向渐变
径向渐变由中心定义
为了创建一个径向渐变，你也必须至少定义两种颜色,同时，可以指定渐变的中心、形状（圆形或椭圆形）、大小。
语法
```
background:radial-gradient(center,shape size,color1,color2,....lastcolor)
```
径向渐变 - 颜色结点均匀分布（默认情况下）
```
#grad1 {
    height: 150px;
    width: 200px;
    background: -webkit-radial-gradient(red, green, blue); /* Safari 5.1 - 6.0 */
    background: -o-radial-gradient(red, green, blue); /* Opera 11.6 - 12.0 */
    background: -moz-radial-gradient(red, green, blue); /* Firefox 3.6 - 15 */
    background: radial-gradient(red, green, blue); /* 标准的语法（必须放在最后） */
}
```
设置形状
shape 参数定义了形状。它可以是值 circle 或 ellipse。其中，circle 表示圆形，ellipse 表示椭圆形。默认值是 ellipse。
```
#grad1 {
    height: 150px;
    width: 200px;
    background: -webkit-radial-gradient(red, yellow, green); /* Safari 5.1 - 6.0 */
    background: -o-radial-gradient(red, yellow, green); /* Opera 11.6 - 12.0 */
    background: -moz-radial-gradient(red, yellow, green); /* Firefox 3.6 - 15 */
    background: radial-gradient(red, yellow, green); /* 标准的语法（必须放在最后） */
}

#grad2 {
    height: 150px;
    width: 200px;
    background: -webkit-radial-gradient(circle, red, yellow, green); /* Safari 5.1 - 6.0 */
    background: -o-radial-gradient(circle, red, yellow, green); /* Opera 11.6 - 12.0 */
    background: -moz-radial-gradient(circle, red, yellow, green); /* Firefox 3.6 - 15 */
    background: radial-gradient(circle, red, yellow, green); /* 标准的语法（必须放在最后） */
}
```

不同尺寸大小关键字的使用
size 参数定义了渐变的大小。它可以是以下四个值：
closest-side
farthest-side
closest-corner
farthest-corner 默认值
```
#grad1 {
    height: 150px;
    width: 150px;
    background: -webkit-radial-gradient(60% 55%, closest-side,blue,green,yellow,black); /* Safari 5.1 - 6.0 */
    background: -o-radial-gradient(60% 55%, closest-side,blue,green,yellow,black); /* Opera 11.6 - 12.0 */
    background: -moz-radial-gradient(60% 55%, closest-side,blue,green,yellow,black); /* Firefox 3.6 - 15 */
    background: radial-gradient(60% 55%, closest-side,blue,green,yellow,black); /* 标准的语法（必须放在最后） */
}

#grad2 {
    height: 150px;
    width: 150px;
    background: -webkit-radial-gradient(60% 55%, farthest-side,blue,green,yellow,black); /* Safari 5.1 - 6.0 */
    background: -o-radial-gradient(60% 55%, farthest-side,blue,green,yellow,black); /* Opera 11.6 - 12.0 */
    background: -moz-radial-gradient(60% 55%, farthest-side,blue,green,yellow,black); /* Firefox 3.6 - 15 */
    background: radial-gradient(60% 55%, farthest-side,blue,green,yellow,black); /* 标准的语法（必须放在最后） */
}

#grad3 {
    height: 150px;
    width: 150px;
    background: -webkit-radial-gradient(60% 55%, closest-corner,blue,green,yellow,black); /* Safari 5.1 - 6.0 */
    background: -o-radial-gradient(60% 55%, closest-corner,blue,green,yellow,black); /* Opera 11.6 - 12.0 */
    background: -moz-radial-gradient(60% 55%, closest-corner,blue,green,yellow,black); /* Firefox 3.6 - 15 */
    background: radial-gradient(60% 55%, closest-corner,blue,green,yellow,black); /* 标准的语法（必须放在最后） */
}

#grad4 {
    height: 150px;
    width: 150px;
    background: -webkit-radial-gradient(60% 55%, farthest-corner,blue,green,yellow,black); /* Safari 5.1 - 6.0 */
    background: -o-radial-gradient(60% 55%, farthest-corner,blue,green,yellow,black); /* Opera 11.6 - 12.0 */
    background: -moz-radial-gradient(60% 55%, farthest-corner,blue,green,yellow,black); /* Firefox 3.6 - 15 */
    background: radial-gradient(60% 55%, farthest-corner,blue,green,yellow,black); /* 标准的语法（必须放在最后） */
}
```
重复的径向渐变
repeating-radial-gradient() 函数用于重复径向渐变：
```
#grad1 {
    height: 150px;
    width: 200px;
    background: -webkit-repeating-radial-gradient(red, yellow 10%, green 15%); /* Safari 5.1 - 6.0 */
    background: -o-repeating-radial-gradient(red, yellow 10%, green 15%); /* Opera 11.6 - 12.0 */
    background: -moz-repeating-radial-gradient(red, yellow 10%, green 15%); /* Firefox 3.6 - 15 */
    background: repeating-radial-gradient(red, yellow 10%, green 15%); /* 标准的语法（必须放在最后） */
}
```
