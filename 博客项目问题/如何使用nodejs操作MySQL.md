默认情况下nodejs是不支持MySQL的，但可以用第三方的模块来完成操作。
使用npm下载mysql模块，用来帮我们操作数据库。
（node的mysql模块是客户端）
```
cnpm install mysql
```
0. 引入模块
```
const mysql = require('mysql')
```
1. 创建连接 (创建数据库对象)
createConnection(哪台服务器，用户名，密码，库)
```
let db = mysql.createConnection({
  host:'localhost',
  user:'root',
  password:'root',
  database:'2020'
});
```
2. 查询
query(SQL语句，回调)
```
db.query('SELECT * FROM user_table ',(err,data)=>{
  if(err)
    console.log(err);
  else
    console.log('成功了');
    console.log(JSON.stringify(data));
})
```

#简单了解SQL语句
四大查询语句--增删改查
- 增----INSERT
INSERT INTO 表（字段列表） VALUES(值类型)
如：
INSERT INTO user_table (id,username,password) VALUES (0,'zhansan','345')
可以测试语句正确否，成功如下
![](https://upload-images.jianshu.io/upload_images/17785871-6f06e4ad0102dd11.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- 删----DELETE
- 改----UPDATE
- 查----SELECT
SELECT 什么 FROM 表
如：
SELECT * FROM user_table 
![](https://upload-images.jianshu.io/upload_images/17785871-f8c17e2e151a0cde.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
