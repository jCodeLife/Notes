#常用操作
1. **npm init -y** 初始化 npm
-y是为了不让他提很多问题让我们回复。
```
Microsoft Windows [版本 6.1.7601]
版权所有 (c) 2009 Microsoft Corporation。保留所有权利。

C:\Users\asus>cd Desktop

C:\Users\asus\Desktop>cd demo

C:\Users\asus\Desktop\demo>npm init -y
Wrote to C:\Users\asus\Desktop\demo\package.json:

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
初始化后在当前目录生成一个package.json
![image.png](https://upload-images.jianshu.io/upload_images/17785871-031b7ac442ec24ed.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
里面内容就是一个json
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
2. **npm i 包名称 **安装对应包名称的插件
npm i jquery 表示安装jQuery
i就是install的缩写
```
C:\Users\asus\Desktop\demo>npm i jquery
npm notice created a lockfile as package-lock.json. You should commit this file.

npm WARN demo@1.0.0 No description
npm WARN demo@1.0.0 No repository field.

+ jquery@3.4.1
added 1 package from 1 contributor and audited 1 package in 3.832s
found 0 vulnerabilities

```
npm i jquery 步骤：
1先去找npm里面有没有jquery，
2如果没有该名的插件，发出警告！
 如果找到有的话，会下载下来并安装到一个目录node_modules
![image.png](https://upload-images.jianshu.io/upload_images/17785871-43fbc499513aa449.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![node_modules文件内就是安装好的插件](https://upload-images.jianshu.io/upload_images/17785871-812271811d403bfb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

同理可以安装vue、bootstrap等
![安装vue和bootstrap](https://upload-images.jianshu.io/upload_images/17785871-95d2ad57b5e38344.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![安装成功](https://upload-images.jianshu.io/upload_images/17785871-98a420e94691d366.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


那么这样依赖，我们便不需要CDN了。只需要在node_modules\vue|jquery|bootstrap\dist里面找对应的插件即可，当在引用的时候将路径拿过去就行。

另外在安装的时候，对应的信息会写到package.json里面。
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
  "license": "ISC",
  "dependencies": {
    "bootstrap": "^4.3.1",
    "jquery": "^3.4.1",
    "vue": "^2.6.10"
  }
}

```
当node_modeles被删除时，要找回来，可以根据这个json里面的信息，重新安装下载：
使用npm i命令
npm i后面什么都不加，表示把所有库重新安装。

以上就是添加一个包或者叫添加一个依赖。
3. **npm uninstall 包名称**，删除对应名称依赖
npm uninstall vue 删除vue
对应插件会在node_modules内移除
package.json的dependencies内对应的依赖也会移除。
```
C:\Users\asus\Desktop\demo>npm uninstall vue
npm WARN bootstrap@4.3.1 requires a peer of popper.js@^1.14.7 but none is instal
led. You must install peer dependencies yourself.
npm WARN demo@1.0.0 No description
npm WARN demo@1.0.0 No repository field.

removed 1 package and audited 2 packages in 1.009s
found 0 vulnerabilities

```
4. **npm update 包名称**更新
npm update jquery表示更新jquery
如果要更新成旧的版本
可以指定版本号：
npm update jquery@3.0.0
