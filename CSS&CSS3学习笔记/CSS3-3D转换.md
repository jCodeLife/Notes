CSS3 主要可以分为以下几个模块：
边框和背景，渐变，文字特效，字体，2D/3D转换，选择器，盒模型，动画，多列布局，用户界面
下面是3D转换
CSS3 允许使用 3D 转换来对元素进行格式化。
1. 转换属性有：
- transform	 2D 或 3D 转换
```
div{
  transform:rotate(7deg);
  -ms-transform:rotate(7deg);/* IE 9 */
  -webkit-transform:rotate(7deg);/* Safari and Chrome */
}
```
- transform-origin	设置旋转元素的基点位置
```
div{
  transform:rotate(45deg);
  transform-origin:20% 40%;
  -ms-transform:rotate(45deg);/* IE 9 */
  -ms-transform-origin:20% 40%;/* IE 9 */
  -webkit-transform:rotate(45deg);/* Safari and Chrome*/
  -webkit-transform-origin:20% 40%;/* Safari and Chrome*/
}
```
- transform-style 规定被嵌套元素如何在 3D 空间中显示
有两个值：
flat 不保留其 3D 位置
preserve-3d 保留其 3D 位置
```
div{
 transform:rotateY(60deg);
 transform-style:preserve-3d;
 -webkit-transform:rotateY(60deg);
 -webkit-transform-style:preserve-3d;
}
```
- perspective	透视图，3D 元素的透视效果,设置元素被查看位置的视图
语法：perspective: number|none;
number	元素距离视图的距离，以像素计。
none	默认值。与 0 相同。不设置透视。
```
div{
  perspective:500;
  -webkit-perspective:500;/* Safari and Chrome */
}
```
- perspective-origin	设置一个3D元素的基数位置
语法：perspective-origin: x-axis y-axis;
x-axis：定义该视图在 x 轴上的位置。默认值：50%。
y-axis：定义该视图在 y 轴上的位置。默认值：50%。
除了百分比，还可能是top center bottom length
```
div{
  perspective:150;
  perspective-origin:10% 10%;
  -webkit-perspective:150;/* Safari and Chrome*/
  -webkit-perspective:10% 10%;/* Safari and Chrome*/
}
```


- backface-visibility	定义元素在不面对屏幕时是否可见
语法：backface-visibility: visible（默认值）|hidden; 
如：背面是不可见的，隐藏旋转的div元素的背面:
```
div{
  backface-visibility:hidden;
  -webkit-backface-visibility:hidden;
  -moz-backface-visibility:hidden;
  -ms-backface-visibility:hidden;
}
```
2.  3D 转换方法
matrix3d(n,n, n,n,n,n ,n,n,n ,n,n,n, n,n,n,n )定义 3D 转换，使用 16 个值的 4x4 矩阵。
translate3d(x,y,z)	定义 3D 转化，往x，y，z轴
translateX(x)	仅 X 轴3D 转化
translateY(y)	 Y 轴3D 转化
translateZ(z)	 Z 轴3D 转化
scale3d(x,y,z)	3D 缩放，对应x，y，z轴
scaleX(x)	X 轴3D 缩放转换
scaleY(y)	Y 轴3D 缩放转换
scaleZ(z)	 Z 轴3D 缩放转换
rotate3d(x,y,z,angle) 定义 3D 旋转
rotateX(angle)	沿 X 轴3D 旋转
rotateY(angle)	沿 Y 轴的3D 旋转
rotateZ(angle)	沿 Z 轴的 3D 旋转
perspective(n)	定义 3D 转换元素的透视视图
```
#div1{
    transform:rotateX(120deg);
    -webkit-transform:rotateX(120deg); /* Safari and Chrome */
}

#div2{
	transform:rotateY(130deg);
	-webkit-transform:rotateY(130deg); /* Safari and Chrome */
}
.......

```


