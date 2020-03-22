在HTML5中添加了data-\*的方式来自定义属性，所谓data-*实际上上就是data-前缀加上自定义的属性名，使用这样的结构可以进行数据存放。  
格式：
(1)在行间上定义自定义属性
```
<div id="test" data-first-name="liao">
  there is codes
 </div>
```
(2)通过js来设置自定义属性或者读取自定义属性值
```
<script>
var temp = document.getElementById('test');
//1.设置自定义属性
temp.dataset.lastname= 'xiaojin'; //或者temp.dataset['lastname'] = 'xiaojin';
//2.读取自定义属性值
temp.dataset.lastname;//或者temp.dataset['lastname'] 
temp.dataset.firstName;//或者temp.dataset['firstName'] 
</script>      
```
自定义属性规范：
1.data-开头；
2.data-后必须至少有一个字符，多个单词使用-连接；
建议：
1.名称应该都使用小写；
2.名称中不要包含任何的特殊符号；
3.名称不要纯数值


data-/dataset与getAttribute/setAttribute相比
1.两者都把属性设置到了attribute上
2.用data-*，一个最大的好处是我们可以把所有自定义属性在dataset对象中统一管理，遍历什么的很方便
