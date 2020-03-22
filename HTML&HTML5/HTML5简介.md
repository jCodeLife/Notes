1. H5并不是新的语言，而是html语言的第五次重大修改版本；2014年10月由万维网联盟（W3C）完成标准制定，设计目的是为了在移动设备上支持多媒体。
2. 支持：所有的主流浏览器都支持H5。IE9以下不支持；
3. 改变了用户的文档交互形式：多媒体：video audio canvas；
4. 新增了其他新的特性：语义特性，本地存储，网页多媒体，二维三维，特效（过渡、动画）；
5. 相对于H4：
- 进步：抛弃了一些不合理不常用的标记和属性
- 新增了一些标记和属性
- 从代码角度而言，h5网页结构更简洁
6. 兼容性处理
对于IE9以下的浏览器，不可能手动创建标签，因为太麻烦。我们可以引入第三方插件。
```
<head>
<meta charset="utf-8">
<title>Styling HTML5</title>
  <!--[if lt IE 9]>
  <script src="http://apps.bdimg.com/libs/html5shiv/3.7/html5shiv.min.js"></script>
  <![endif]-->
</head>
```
7. HTML5文档声明更加简单了:
```
<!DOCTYPE html>
```
8. HTML5 中的一些有趣的新特性：
- 用于绘画的 canvas 元素
- 用于媒介回放的 video 和 audio 元素
- 对本地离线存储的更好的支持
- 新的特殊内容元素，比如 article、footer、header、nav、section
- 新的表单控件，比如 calendar、date、time、email、url、search
9. HTML5的改进
- 新元素
- 新属性
- 完全支持 CSS3
- 多媒体Video 和 Audio
- 2D/3D 制图
- 本地存储
- 本地 SQL 数据
- Web 应用
10. 使用 HTML5 你可以简单地开发应用
- 本地数据存储
- 访问本地文件
- 本地 SQL 数据
- 缓存引用
- Javascript 工作者
- XHTMLHttpRequest 2
11. 使用 HTML5 你可以简单的绘制图形:
- 使用 <canvas> 元素
- 使用内联 SVG
- 使用 CSS3 2D/CSS 3D
12. HTML5 使用 CSS3
- 新选择器
- 新属性
- 动画
- 2D/3D 转换
- 圆角
- 阴影效果
- 可下载的字体
13. HTML5 添加了很多语义元素如下所示：
```
<article>	定义页面独立的内容区域。
<aside>	定义页面的侧边栏内容。
<bdi>	允许您设置一段文本，使其脱离其父元素的文本方向设置。
<command>	定义命令按钮，比如单选按钮、复选框或按钮
<details>	用于描述文档或文档某个部分的细节
<dialog>	定义对话框，比如提示框
<summary>	标签包含 details 元素的标题
<figure>	规定独立的流内容（图像、图表、照片、代码等等）。
<figcaption>	定义 <figure> 元素的标题
<footer>	定义 section 或 document 的页脚。
<header>	定义了文档的头部区域
<mark>	定义带有记号的文本。
<meter>	定义度量衡。仅用于已知最大和最小值的度量。
<nav>	定义导航链接的部分。
<progress>	定义任何类型的任务的进度。
<ruby>	定义 ruby 注释（中文注音或字符）。
<rt>	定义字符（中文注音或字符）的解释或发音。
<rp>	在 ruby 注释中使用，定义不支持 ruby 元素的浏览器所显示的内容。
<section>	定义文档中的节（section、区段）。
<time>	定义日期或时间。
<wbr>	规定在文本中的何处适合添加换行符。
```
14. HTML5 表单
新表单元素, 新属性，新输入类型，自动验证。
新的表单控件，比如 calendar、date、time、email、url、search
