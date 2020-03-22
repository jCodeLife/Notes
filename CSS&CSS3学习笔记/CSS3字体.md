CSS3 主要可以分为以下几个模块：
边框和背景，渐变，文字特效，字体，选择器，盒模型，2D/3D转换，动画，多列布局，用户界面
下面是字体模块：
在CSS3之前，web设计师必须使用已在用户计算机上安装好的字体，不能够使用离线字体，不过通过CSS3，web设计师可以使用他们喜欢的任意字体，
当找到或购买到希望使用的字体时，可将该字体文件存放到web服务器上，它会在需要时被自动下载到用户的计算机上。
- **@font-face**属性
在新的 @font-face 规则中，必须首先定义字体的名称（比如 myFont），然后指向该字体文件。
通过 font-family 属性来引用字体的名称。
```
<style>
  @font-face{
    font-family:myFont;
    src:url(字体所在位置);
  }

  /*使用字体自己的字体*/
   div{
    font-family：myFont；
  }
</style>
```

使用粗体文本
```
@font-face
{
   font-family: myFirstFont;
   src: url(sansation_bold.woff);
   font-weight:bold;
}
```
CSS3 字体描述
下面是所有的字体描述和里面的@font-face规则定义：
font-family: name 必需。规定字体的名称。
src:	URL	必需。定义字体文件的 URL。
font-stretch: 可选。定义如何拉伸字体。默认是 "normal"。
font-style: (normal italic oblique) 可选。定义字体的样式。默认是 "normal"。
font-weight: (normal  bold 100 200...900)可选。定义字体的粗细。默认是 "normal"。
unicode-range:可选。定义字体支持的 UNICODE 字符范围。默认是 "U+0-10FFFF"。
