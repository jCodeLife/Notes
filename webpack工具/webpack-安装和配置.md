1. 安装
1.1全局安装
全局安装，安装的版本是最近的，如下正在安装：
```
C:\Users\asus>npm i webpack@latest -g
[   ...............] - fetchMetadata: sill resolveWithNewModule chokidar@2.1.6
```
通过webpack 
1.2 局部安装
进入到该项目的项目目录，npm init -y，先生成一个package.json,只要有package.json，npm就认为整个目录就是一个项目，就是个模块了。
然后npm i webpack -D
2. 怎么在本地跑webpack
node_modules下有个.bin文件夹（binary 二进制的，可执行的东西），bin里面有个webpack
```
node_modules/.bin/webpack a.js bundle.js;
```
这样可以把a文件打包成boundle.js文件。
路径太长可以将路径写到package.json里面，
```
"scripts":{
  "pack":"node_modules/.bin/webpack a.js bundle.js"
}
```
那我们可以npm run 键名执行命令
```
npm run pack
```
相当于快捷方式
一般这种配置不太好，可能有些太长。那我们可以写一个独立的配置文件叫：webpack.config.js
2. 配置文件webpack.config.js
```
module.exports = {
  entry:'./a.js';//入口文件
  output:{
    filename:"pack.js",
    path:__dirname,//__dirname特殊变量表示当前目录
    ....
  }
}
```

