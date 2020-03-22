CSS3 主要可以分为以下几个模块：
边框和背景，渐变，文字特效，选择器，盒模型，2D/3D转换，动画，多列布局，用户界面
下面接着是文字特效新增：
- text-shadow 文本阴影
可指定水平阴影，垂直阴影，模糊的距离，以及阴影的颜色
```
h1{
    text-shadow: 5px 5px 5px #FF0000;
}
```
- box-shadow 盒子阴影
```
div { box-shadow: 10px 10px;}
div { box-shadow: 10px 10px grey;}
div { box-shadow: 10px 10px 5px grey;}

div{
	width:300px;
	height:100px;
	background-color:yellow;
	box-shadow: 10px 10px 5px #888888;
}
```
也可以在 ::before 和 ::after 两个伪元素中添加阴影效果
```
#boxshadow::after { 
    content: ''; 
    position: absolute; 
    z-index: -1; /* hide shadow behind image */ 
    box-shadow: 0 15px 20px rgba(0, 0, 0, 0.3); 
    width: 70%; 
    left: 15%; /* one half of the remaining 30% */ 
    height: 100px; 
    bottom: 0;
}
```
阴影的使用场景：如-卡片效果
```
.card { 
    width: 250px; 
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19); 
    text-align: center;
}
```
- text-overflow 文本溢出,指定应向用户如何显示溢出内容
```
p.test1 { 
    white-space: nowrap; 
    width: 200px; 
    border: 1px solid #000000; 
    overflow: hidden; 
    text-overflow: clip; 
} 
p.test2 { 
    white-space: nowrap; //空白：不换行。超出文本不换行
    width: 200px; 
    border: 1px solid #000000; 
    overflow: hidden; 
    text-overflow: ellipsis; 
}
```
- word-wrap 单词换行
```
p {word-wrap:break-word;}长单词允许打断换行
```
- word-break 单词拆分换行
```
p.test2 { word-break: break-all;}打断所有
p.test1 { word-break: keep-all;} 保持所有
```

除上述，大概知道一下几个新增属性，不过兼容性特别差，仅做了解吧：
hanging-punctuation 标点字符是否位于线框之外,目前主流浏览器都不支持该属性。
punctuation-trim 规定是否对标点字符进行修剪。目前主流浏览器都不支持 该属性。
text-align-last 设置如何对齐最后一行或紧挨着强制换行符之前的行，只有 Internet Explorer 支持 text-align-last 属性。
text-emphasis 向元素的文本应用重点标记以及重点标记的前景色，兼容性可查can i use
text-justify 对齐方法 字与字之间的间隙。只有ie支持
text-outline	规定文本的轮廓。主流浏览器都不支持text-outline属性。

