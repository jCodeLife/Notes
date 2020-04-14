需求：点击注册按钮时，显示出注册页面
问题：地址正常跳转，但对应组件在对应位置没显示、也没报错？
```
<router-link to='./sign_up'>
    <el-button type="danger" size="small">注册</el-button> 
</router-link>
<!--显示位置 -->
<router-view></router-view>   
```
解决：通过反复测试，后面发现有一条不显眼的警告消息：
[vue-router] Non-nested routes must include a leading slash character. Fix the following routes:...
大概意思是
非嵌套路由必须包含一个前导斜杠字符。
于是我在在定义路由路径path处修改了一下，解决成功！即：**在填写path时，前面需要将添加一个斜杠字符**
```
export default new Router({
routes: [
    {
      path: '/sign_in',           //原本是path: './sign_in',
      name: 'sign_in',
      component: {
        template: `<h1>sign_in page</h1>`
     }
]
})
```
