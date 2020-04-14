在遍历数据的时候，发现
报错信息： [Vue warn]: Avoid using non-primitive value as key, use string/number value inst....
大概意思：避免使用非基值作为键，应使用字符串/数字值
原错误代码
```
<div id="main">
    <div v-for="(v,k) in articles" :key="articles[k]" :name="k">
      <el-link href="#" target="_blank">{{articles[k].question}}</el-link>
      <br />
    </div>
  </div>
```
经过实践发现：
在v-for遍历时，如果将遍历出来的值作为:key的值时，并且这个值恰巧是一个对象就会报错。
解决：
可以将该对象中的某一项的值作为key或者循环时添加index，将index作为key
```
<div id="main">
    <div v-for="(v,k) in articles" :key="articles[k].number" :name="k">
      <el-link href="#" target="_blank">{{articles[k].question}}</el-link>
      <br />
    </div>
  </div>
```
