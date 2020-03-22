CSS3 主要可以分为以下几个模块：
边框和背景，渐变，文字特效，字体，2D/3D转换，动画(过渡动画和动画)，选择器，盒模型，多列布局，用户界面
下面是动画中的过渡动画：
**transition**：过渡，是复合属性，用于在一个属性中设置四个过渡属性：

- transition-property：CSS的属性名，默认值：all
```
div{
  transition-property:width;
  -moz-transition-property:width;/* Firefox */
  -webkit-transition-property:width;/* Safari and Chrome */
  -o-transiton-property:width;/* Opero*/
}
div:hover{
  width:300px;
}
```

- transition-duration：duration持续的意思，表示过渡时间；默认是 0
```
div{
  width:100px;
  height:100px;
  background:red;
  transition-property:all;
  transtion-duration:2s;
  -webkit-transition-property:all;/* Safari */
  -webkit-transition-duration:2s;/* Safari */
}
```
- transition-timing-function：timing调速的意思，过渡效果速度，默认是 "ease"
语法：
transition-timing-function: linear|ease|ease-in|ease-out|ease-in-out|cubic-bezier(n,n,n,n);
linear 线性的，匀速；
ease 轻松 悠闲的；慢速开始，然后变快，然后慢速结束；
ease-in 以慢速开始
ease-out	以慢速结束
ease-in-out 慢速开始和慢速结束
cubic-bezier(n,n,n,n)	立方贝塞尔曲线；在 cubic-bezier 函数中定义值。可能的值0 至 1 之间
```
#div1{transition-timing-function:linear};
#div2{transition-timing-function:ease};
#div3{transition-timing-function:ease-in};
#div4{transition-timing-function:ease-out};
#div5{transition-timing-function:ease-in-out};

/*  Safari */
#div1{-webkit-transition-timing-function:linear};
#div2{-webkit-transition-timing-function:ease};
#div3{-webkit-transition-timing-function:ease-in};
#div4{-webkit-transition-timing-function:ease-out};
#div5{-webkit-transtion-timing-function:ease-in-out};
```
和上面的例子一样，但指定速度曲线立方贝塞尔曲线函数：
```
#div1 {transition-timing-function: cubic-bezier(0,0,1,1;} 
#div2 {transition-timing-function: cubic-bezier(0.25,0.1,0.25,1);} 
#div3 {transition-timing-function: cubic-bezier(0.42,0,1,1);} 
#div4 {transition-timing-function: cubic-bezier(0,0,0.58,1);} 
#div5 {transition-timing-function: cubic-bezier(0.42,0,0.58,1);} 
/* Safari */ 
#div1 {-webkit-transition-timing-function: cubic-bezier(0,0,1,1;} 
#div2 {-webkit-transition-timing-function: cubic-bezier(0.25,0.1,0.25,1);} 
#div3 {-webkit-transition-timing-function: cubic-bezier(0.42,0,1,1);} 
#div4 {-webkit-transition-timing-function: cubic-bezier(0,0,0.58,1);} 
#div5 {-webkit-transition-timing-function: cubic-bezier(0.42,0,0.58,1);} 
```

- transition-delay：延迟、推迟、耽搁；默认是 0。
```
div{
  transition-delay:2s;
  -moz-transition-delay:2s;/* Firefox 4 */
  -webkit-transition-delay:2s;/* Safari 和 Chrome */
  -o-transition-dalay:2s;/* Opera */
}
```
transition：过渡，是复合属性，用于在一个属性中设置四个过渡属性：
transition ： transition-property transition-duration transition-timing-function transition-delay
```
div{
  transition: all 2s ease 1s;
  -webkit-transition: all 2s ease 1s;
}
```
也可以设置多个：
```
div 
{ 
transition: width 2s, height 2s, transform 2s; 
-webkit-transition: width 2s, height 2s, -webkit-transform 2s; 
}  
```

