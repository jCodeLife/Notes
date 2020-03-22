1. charset 编码字符集
（1）gb2312：中国的国家标准第2312条，包括了亚洲国家，不能识别繁体字符；
（2）gbk：国家标准扩展版本，包括了繁体；
（3）Unicode：万国码，包括了所有国家；
（4）utf-8：是Unicode的升级版，也称万国码；
2. lang = ‘en’
告诉搜索引擎爬虫，我们的网站内容是关于什么内容的。en表示英文，zh表示中文。
3. <div>和<span>
充当容器
（1）让页面更加结构化；
（2）绑定操作，更加便捷；
4. 空格
表示英文字母的分隔符，不能当文本。
用&nbsp，表示空格文本；
5. 尖括号<>
```
（1）<  --  &lt  --  less than 小于
（2）>  --  &gt  --  great than 大于
&copy; 等同于 ©
```
6. 换行
br
7. 水平线
hr
8. 有序列表 ol 
order list
```
<ol type="A" reversed = “reversed” start = ‘2’> --列表架
  <li></li>--列表项
  <li></li>
  <li></li>
</ol>
type可以是1，a，A，i，I
reversed = “reversed” 倒序
start = ‘2’ 从第2个开始。

```
9. 无序列表 ul
unorder list
```
<ul type = "disc"> --列表架
  <li></li>--列表项
  <li></li>
  <li></li>
</ul>
type可以为disc\square\circle

```
10. 自定义列表
```
<dl>
   <dt>项目 1</dt>
     <dd>描述项目 1</dd>
   <dt>项目 2</dt>
     <dd>描述项目 2</dd>
 </dl>
```
11. 图片
```
<img src="URL" alt="替换文本" height="42" width="42" title="">
```
（1）src：source的缩写，表示源文件，源头。可以是网上url也可以是本地的绝对或相对路径；
（2）alt：当图片不行时，加载这里的文字信息；
（3）title：图片提示符

12. 链接
<a>  
```
<a href="" target= "_blank"></a>

普通的链接：<a href="链接地址">链接文本</a>
图像链接： <a href="http://www.example.com/"><img src="URL" alt="替换文本"></a> 
邮件链接： <a href="mailto:webmaster@example.com">发送e-mail</a>
书签： <a id="tips">
提示部分</a> <a href="#tips">跳到提示部分</a>
```
（1）a   --anchor 锚
（2）href--hyperText reference 超文本引用；
（3）a标签的作用：
- 超链接  <a href="http://www.w3school.com.cn">
- 锚头 <a href="#xxx">
- 带电话 <a href = "tel:123456789".
- 协议限定符 <a href="javascript:...">
13.  表单标签
<form>
```
<form action="demo_form.php" method="post/get"> 
action：表单发送给谁（数据接收方的地址）
method：通过哪种方式发送数据

<input type="text" name="email" size="40" maxlength="50"> 文本框
<input type="password"> 密码
<input type="checkbox" checked="checked"> 复选框
<input type="radio" checked="checked"> 单选框
<input type="submit" value="Send"> 提交按钮
<input type="reset"> 重置
<input type="hidden"> 隐藏

<select> 下拉框
<option>苹果</option> 下拉选项
<option selected="selected">香蕉</option> 
<option>樱桃</option> 
</select>

<textarea name="comment" rows="60" cols="20">文本区域
</textarea> 
</form>
```
14. html注释：
```
<!-- 这是注释 -->
```
15. 产品符合三个特点：
（1）解决钢需问题；
（2）用户体验，培养用户的懒习惯；
（3）提高用户粘性；
16. 主流浏览器及其内核：
主流浏览器标准：市场份额和独立内核
IE trident
firfox  Gecko 
Chrome  webkit/blink
Safari  webkit
Opera  presto

16. 文本格式化（Formatting）
```
 <b>粗体文本</b>
 <code>计算机代码</code>
 <em>强调文本</em>
 <i>斜体文本</i>
 <kbd>键盘输入</kbd> 
 <pre>预格式化文本</pre>
 <small>更小的文本</small>
 <strong>重要的文本</strong>
 
 <abbr> （缩写）
 <address> （联系信息）
 <bdo> （文字方向）
 <blockquote> （从另一个源引用的部分）
 <cite> （工作的名称）
 <del> （删除的文本）
 <ins> （插入的文本）
 <sub> （下标文本）
 <sup> （上标文本）
```
18. 表格
```
<table border="1">
   <tr>
     <th>表格标题</th>
     <th>表格标题</th>
   </tr>
   <tr>
     <td>表格数据</td>
     <td>表格数据</td>
   </tr>
 </table>
```
