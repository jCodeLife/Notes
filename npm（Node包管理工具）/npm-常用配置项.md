初始化npm的时候，我们用了npm init -y或者npm init --yes；
-y或者--yes表示所有的配置项都是使用默认值。
如果不添加-y或者--yes，就会问很多问题，这些问题，我们叫npm的配置项。
- package name:
当npm初始化了，在我们看来是一个项目，在它眼里是一个包，所以这里要输入这个包的名称。
注意：包名中间不能有空格，并且必须要小写。
- version：
包的版本号，默认是1.0.0
- description：
描述，可以写也可以不写
- entry point:
包的入口文件
- test command：
命令
- git repository：
git 仓库
- keywords：
关键词
- author：
作者
之后就会创建一个package.json,这个json文件里面就是上面填写的配置项。
如果用npm init -y或者npm init --yes来初始化，我可以在这个json文件里面更改。
```
{
  "name": "demo",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```
注意：
这个json里面有一项scripts，用于指定一些命令的快捷方式。
如上面有个
```
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  }
```
那我们可以运行上面定义的命令。
```
 npm run test
```
一般我们也可以在这个script里面自定义一些命令，指定了什么命令就可以跑什么命令。


