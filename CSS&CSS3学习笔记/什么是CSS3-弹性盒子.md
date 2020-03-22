
***
1.  简介
`弹性盒子`是一种新的布局方式，也被成为`flex布局`或者`弹性布局`，其利用具有自适应伸缩特性的容器实现栏目或组件的弹性布局。
- 目的：提供一种更加有效的方式来对一个容器中的子元素进行排列、对齐和分配空白空间。
- 组成：弹性盒子由弹性容器(Flex container)和弹性子元素(Flex item)（也叫弹性项目）组成。一个弹性容器内包含了一个或多个弹性子元素。
- 实现：弹性容器通过设置 display = flex 或 inline-flex，将其定义为弹性容器。
- 注意：
 （1）弹性容器外及弹性子元素内是正常渲染的。
 （2）弹性盒子只定义了弹性子元素如何在弹性容器内布局。
 （3）弹性子元素通常在弹性盒子内一行显示。默认情况每个弹性容器只有一行，如：

2. Flex布局的基础概念
`布局结构：双层html结构` 
指定一个外部容器为flex布局，容器内部的第一层级元素就可以使用flex布局
外围的flex区域称为flex容器【flex container】，目的是用来激活flex的弹性机制
里面的第一层级子集元素称为flex项目【flex item】，自动获得flex相关特性和控制能力
flex特性仅附加于flex容器和flex项目，容器外部或项目内部的元素不受影响  
`flex机制：`
给需要采用flex布局的外围容器，定义display显示模式进行激活(弹性容器通过设置 display = flex 或 inline-flex，将其定义为弹性容器。)
任何一个容器都可以指定为 Flex 布局，一旦指定则内部第一层级的子项自动变成flex项目
一旦激活Flex机制，则子项的float、clear和vertical-align属性将失效.
`Flex轴向：项目的排列对齐以轴向为基准`
容器默认存在两条轴：主轴和侧轴，由flex容器属性来设定
轴的两端分别称为起点和终点
flex项目依据主轴的方向定义进行排列
默认设置下：主轴为水平方向，起点在左，终点在右，flex项目按从左至右排列


**3. flex相关属性：**
flex属性可分为两大类：外围外围容器上的属性和子项属性
2.1 外围容器上的属性：
外围容器的相关属性,主要控制flex布局中项目的排列与对齐
3个排列相关属性：
- **`flex-direction`** 
定义容器的主轴方向，即子项的排列方向
flex-direction的值：
`row`：行，从左往右，默认的排列方式
`row-reverse`：行反转，从右往左
`column`：列，从上到下
`column-reverse`：列反转，从下往上

- **`flex-wrap `** 
定义容器的换行方式（子项是单行显示还是多行显示）
即：弹性盒子的子元素超出父容器时是否换行。
3个值：`nowrap`（不换行） / `wrap`（换行） / `wrap-reverse`（换行并反转行顺序）
默认为nowrap，不换行
换行反转：新行的内容呈现在前面

- **`flex-flow `**
定义容器的“文档流”
是flex-direction 和 flex-wrap 的简写
2个值之间，空格隔开，顺序不限
```
display:flex;
flex-flow:row-reverse wrap;
```

3个对其相关属性：
- **`justify-content `** 
定义子项在主轴上的对齐方式
5个值分别是：
`flex-start`	起点对齐
`flex-end`	终点对齐
`center`	中间对齐
`space-round`	平均分布，留白环绕子项元素
`space-between`	平均分布，留白只存在于子项元素之间
![2019-6-3 15:25:32](https://upload-images.jianshu.io/upload_images/17785871-69e72b5c6f0a8c69.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- **`align-items`**
定义子项在侧轴上的对齐方式
5个值分别是：
`flex-start`：起点对齐
`flex-end`：终点对齐
`center`：居中对齐
`baseline`：基线对齐（子项的第一行文本）（无文本则底部对齐）
`stretch`：拉伸对齐（子项未设置尺寸的情况下占满容器侧轴向空间），默认值



- **`align-content `**
定义容器在多行排列下，子项在侧轴上的对齐方式
容器只有单行时，此属性无效
属性的值有：
`flex-start`	起点对齐
`flex-end`	终点对齐
`center`	中间对齐
`stretch`	拉伸对齐（多行子项平均分布，自身拉伸）默认。
`space-round`	留白环绕子项元素
`space-between`留白只存在于子项元素之间

2.2  **flex子项的相关属性**  
主要控制flex布局中子项的自适应伸缩及分配
`自适应伸缩 = 按比例分配容器的剩余空间`

- **`flex-grow`**
定义子项（item）的扩展比例
默认值为0，即无扩展
仅当存在可用的分配空间时有效
对于多行的子项，剩余空间以“行”为单位
值为纯数字，没有负值，没有单位

- **`flex-shrink`**
定义子项（item）的收缩比例
值表示的是空间分配比例，纯数字，无单位；
默认值为1，即等比缩小
当容器空间不足时有效（nowrap状态下）
- **`flex-basis`**
定义子项（item）在主轴上的基准尺寸（初始大小）
值为长度值或者百分比
默认值：auto，即项目原定大小；如果设定值，则优先于项目原定大小
配合 flex-grow 和 flex-shrink 配合使用才能发挥效果
- **`flex`**
复合属性：flex-grow, flex-shrink 和 flex-basis的简写
语法
flex：none | [ flex-grow ] || [ flex-shrink ] || [ flex-basis ]
多个值以空格隔开，按既定顺序排列（grow、shrink、basis），可省略
值的写法有多种形式
flex的常见取值：
默认值：【flex：0 1 auto】 （三个属性值的组合），简写为【flex：0 auto】
快捷值：auto = 【flex：1 1 auto】（子项可扩展可收缩）
快捷值：none = 【flex：0 0 auto】（子项固定）
比例值：只定义比例，按顺序为grow、shrink值 ， basis值变auto为0%
尺寸值：只定义尺寸，值为basis的值， grow值变0为1
速记注意：
只定义比例，basis值会改变（子项原定尺寸会被覆盖）
只定义尺寸，则子项可扩展可收缩（更改默认不扩展特性）

子项核心属性的特点总结：
扩展（grow）/收缩（ shrink）是按比例操作子项的适配方式，值为纯数字类型无单位无负值
一个flex布局中， flex-shrink 和 flex-grow 只会有一个能起作用
优先使用flex复合属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。
基准尺寸（ basis ）在flex模块中，替代了主轴方向上的width或height值
要保证子项的尺寸固定，通常需要在设定basis的基础上，定义grow和shrink为0。常见写法有：
 width/height  配合 【flex：none】
【flex：0 0 尺寸】

- **`align-self`**
和align-item一样，定义子项在侧轴上的对齐方式
优先级高于align-item，用于为特殊的子项定义不一样的对齐方式
值：
flex-start	起点对齐
flex-end	终点对齐
center	中间对齐
baseline	基线对齐（子项的第一行文本）（无文本则底部对齐）
stretch	默认值，拉伸对齐（子项未设置尺寸的情况下占满容器侧轴向空间）
auto：自动

- **`order`**
定义子项在容器中的排列顺序
值为整数，数值小的排在前面。可以为负值，默认值为 0。









