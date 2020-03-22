CSS3 主要可以分为以下几个模块：
边框和背景，渐变，文字特效，字体，2D/3D转换，动画(过渡动画和动画)，选择器，盒模型，多列布局，用户界面
下面是动画animation：
1. **@keyframes创建动画**
@keyframes规则是创建动画。
@keyframes规则内指定一个CSS样式和动画将逐步从目前的样式更改为新的样式。
```
@keyframes myfirst{
  from{background:red}
  to{background:yellow}
}
@-webkit-keyframes myfirst{ /* Safari and Chrome*/
  from{background:red}
  to{background:yellow}
}
```
2. 绑定动画
@keyframe是创建动画，我们需要把创建好的动画，通过animation属性绑定到一个选择器，否则动画不会有任何效果。
如下：把 "myfirst" 动画捆绑到 div 元素，动画时长5 秒：
```
格式：animation:动画名 动画时长；
div{
  animation:myfirst 5s;
}
```
动画是使元素从一种样式逐渐变化为另一种样式的效果。
可以改变任意多的样式任意多的次数。
请用百分比来规定变化发生的时间，或用关键词 "from" 和 "to"，等同于 0% 和 100%。0% 是动画的开始，100% 是动画的完成。
一般为了得到最佳的浏览器支持，应该始终定义 0% 和 100% 
```
改变背景色和位置：
@keyframes two
{
0%   {background: red; left:0px; top:0px;}
25%  {background: yellow; left:200px; top:0px;}
50%  {background: blue; left:200px; top:200px;}
75%  {background: green; left:0px; top:200px;}
100% {background: red; left:0px; top:0px;}
}

@-webkit-keyframes two/* Safari and Chrome */
{
0%   {background: red; left:0px; top:0px;}
25%  {background: yellow; left:200px; top:0px;}
50%  {background: blue; left:200px; top:200px;}
75%  {background: green; left:0px; top:200px;}
100% {background: red; left:0px; top:0px;}
}
```

3. @keyframes 规则和所有动画属性
@keyframes	规定动画
animation	所有动画属性的简写属性，除 animation-play-state
animation-name	@keyframes 动画名称
animation-duration	动画完成一个周期所花秒或毫秒数。默认是 0
animation-timing-function	动画的速度曲线。默认是 "ease"
animation-delay	动画延迟多久开始。默认是 0
animation-iteration-count	规定动画被播放的次数。默认是 1
animation-direction	规定动画是否在下一周期逆向地播放。默认是 "normal"
animation-play-state	规定动画是否正在运行或暂停。默认是 "running"。
```
div
{
animation-name: myfirst;
animation-duration: 5s;
animation-timing-function: linear;
animation-delay: 2s;
animation-iteration-count: infinite;
animation-direction: alternate;
animation-play-state: running;
/* Safari and Chrome: */
-webkit-animation-name: myfirst;
-webkit-animation-duration: 5s;
-webkit-animation-timing-function: linear;
-webkit-animation-delay: 2s;
-webkit-animation-iteration-count: infinite;
-webkit-animation-direction: alternate;
-webkit-animation-play-state: running;
}
```
与上面的动画相同，使用简写的 animation 动画属性：
```
div
{
animation: myfirst 5s linear 2s infinite alternate;
/* Safari and Chrome: */
-webkit-animation: myfirst 5s linear 2s infinite alternate;
}
```
