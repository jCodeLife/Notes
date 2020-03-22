CSS3 主要可以分为以下几个模块：
边框和背景，渐变，文字特效，字体，2D/3D转换，选择器，盒模型，动画，多列布局，用户界面
下面是2D转换：
2D转换可以实现：移动，比例化，反过来，旋转，和拉伸元素。
2D变换transform的方法：
- **translate()**
元素根据给定的X轴和Y轴位置移动
```
移动到left 50px，top 100px的位置：
#div2 {
  transform:translate(50px,100px);
  -ms-transform:translate(50px,100px); /* IE 9 */
  -webkit-transform:translate(50px,100px); /* Safari and Chrome */
}
```
- **rotate()**
旋转一定的度数，默认随时针；允许负值，表示逆时针旋转
```
旋转30度
div { 
transform: rotate(30deg); 
-ms-transform: rotate(30deg); /* IE 9 */ 
-webkit-transform: rotate(30deg); /* Safari and Chrome */ 
}  
```
- **scale()**
缩放一定比例
可以给定x，y分别设置不同缩放
```
div 
{ 
transform: scale(2,4); 
-ms-transform: scale(2,4); /* IE 9 */ 
-webkit-transform: scale(2,4); /* Safari and Chrome */ 
}  

scale（2,4）表示宽度为原来的大小的2倍，高度是原始大小4倍
```
- **skew()**
倾斜
包含两个参数值，分别表示X轴和Y轴倾斜的角度，如果第二个参数为空，则默认为0，参数为负表示向相反方向倾斜。
skewX( );表示只在X轴(水平方向)倾斜。
skewY( );表示只在Y轴(垂直方向)倾斜。 
```
div 
{ 
transform: skew(30deg,20deg); 
-ms-transform: skew(30deg,20deg); /* IE 9 */ 
-webkit-transform: skew(30deg,20deg); /* Safari and Chrome */ 
}  
```
- **matrix()**
matrix()方法和2D变换方法合并成一个。
matrix 方法有六个参数，包含旋转，缩放，移动（平移）和倾斜功能。
```
利用matrix()方法旋转div元素30°
div 
{ 
transform:matrix(0.866,0.5,-0.5,0.866,0,0); 
-ms-transform:matrix(0.866,0.5,-0.5,0.866,0,0); /* IE 9 */ 
-webkit-transform:matrix(0.866,0.5,-0.5,0.866,0,0); /* Safari and Chrome */ 
}  
```
小结：
1. 新转换属性
transform	2D或3D转换
transform-origin 更改转化元素位置
2. 2D 转换方法
matrix(n,n,n,n,n,n)	定义 2D 转换，使用六个值的矩阵。
translate(x,y)	定义 2D 转换，沿着 X 和 Y 轴移动元素。
translateX(n)	定义 2D 转换，沿着 X 轴移动元素。
translateY(n)	定义 2D 转换，沿着 Y 轴移动元素。
scale(x,y)	定义 2D 缩放转换，改变元素的宽度和高度。
scaleX(n)	定义 2D 缩放转换，改变元素的宽度。
scaleY(n)	定义 2D 缩放转换，改变元素的高度。
rotate(angle)	定义 2D 旋转，在参数中规定角度。
skew(x-angle,y-angle)	定义 2D 倾斜转换，沿着 X 和 Y 轴。
skewX(angle)	定义 2D 倾斜转换，沿着 X 轴。
skewY(angle)	定义 2D 倾斜转换，沿着 Y 轴。

[CSS3 transform(变形)和transform-origin(变形原点)调试工具](https://www.w3cschool.cn/tools/index?name=css3_transform)
