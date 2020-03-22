通过使用 CSS 来创建分页的实例
1. 简单分页
```
ul{
  display:inline-block;
  padding:0;
  margin:0;
}
ul li{
  display:inline-block;
}
ul li a{
  color:black;
  float:left;
  padding:8px 16px;
  text-decoration:none;
}
```
可以通过css其他属性来美化简单分页
- 使用 .active 来设置当期页样式，鼠标悬停可以使用 :hover 选择器来修改样式：
```
ul{
  display:inline-block;
  padding:0;
  margin:0;
}
ul li{
  display:inline-block;
}
ul li a{
  color:black;
  float:left;
  padding:8px 16px;
  text-decoration:none;
}

ul li a.active {
    background-color: #4CAF50;
    color: white;
}
ul li a:hover:not(.active) {/*通过hover来设置背景*/ 
  background-color: #ddd;
}
```
- 使用 border-radius 属性为选中的页码来添加圆角样式:
```
ul{
  display:inline-block;
  padding:0;
  margin:0;
}
ul li{
  display:inline-block;
}
ul li a{
  color:black;
  float:left;
  padding:8px 16px;
  text-decoration:none;
  border-radius: 5px; /*使用 border-radius 添加圆角样式:*/
}

ul li a.active {
    background-color: #4CAF50;
    color: white;
    border-radius: 5px;  /*使用 border-radius 添加圆角样式:*/
}
ul li a:hover:not(.active) {
  background-color: #ddd;
}
```
- 通过 transition添加过度效果
```
ul li a { 
    transition: background-color .3s; 
}
```
- 通过border来添加边框分页
```
ul li a { 
    border: 1px solid #ddd; /* Gray */ 
} 
```
- 使用 margin 来为每个页码添加空格
```
ul li a{
  margin:0 4px;
}
```
- 通过font-size来设置分页字体大小
```
ul li a{
  font-size:22px;
}
```
- 通过text-align:center让分页中的文本居中，可以设置在外层div
```
div{
  text-align: center;
}
```
- 分页导航:
```
ul.pagination {
    display: inline-block;
    padding: 0;
    margin: 0;
}

ul.pagination li {display: inline;}

ul.pagination li a {
    color: black;
    float: left;
    padding: 8px 16px;
    text-decoration: none;
    transition: background-color .3s;
    border: 1px solid #ddd;
    font-size: 18px;
}

ul.pagination li a.active {
    background-color: #eee;
    color: black;
    border: 1px solid #ddd;
}

ul.pagination li a:hover:not(.active) {background-color: #ddd;}
```
- 面包屑导航
面包屑导航(BreadcrumbNavigation)这个概念来自童话故事"汉赛尔和格莱特"，当汉赛尔和格莱特穿过森林时，不小心迷路了，但是他们发现在沿途走过的地方都撒下了面包屑，让这些面包屑来帮助他们找到回家的路。所以，面包屑导航的作用是告诉访问者他们目前在网站中的位置以及如何返回。
