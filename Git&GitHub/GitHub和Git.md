目的：
1.  借助github托管项目代码
2.  通过git管理github项目代码
##git常用命令

![image.png](https://upload-images.jianshu.io/upload_images/17785871-ad9a943cc72cf802.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)




###基本概念
Repository：仓库
仓库用来存放的项目代码，每个项目对应一个仓库，多个开源项目则有多个仓库。

Star：星星
收藏项目，方便下次查看。

Fork：叉子
复制克隆项目，独立存在

Pull request:发送请求

Watch：关注
关注项目，当项目有跟新的时候会收到通知

Issue：问题
发现代码bug，但是目前没成型代码，需要讨论时用。

使用邮箱注册Github账号
###仓库主页

1. 仓库创建

2. 仓库管理
新建文件 new
编辑文件 creating a new file
删除文件 delete this file
上传文件 upload files
搜索仓库文件 find file
下载/检出项目 clone or download
...

###操作初试
```
初试以上等相关操作 ok
```
###开源项目贡献流程
1. 新建Issue
提交使用问题或者想法
2. Pull request
步骤
（1）fork项目
（2）修改自己仓库的项目代码
（3）新建Pull request
（4）等作者同步好即可

#Git
## Git 安装配置
在使用Git前我们需要先安装 Git,
[window系统](https://msysgit.github.io/)
[Git 各平台安装包下载地址](https://git-scm.com/downloads)

完成安装之后，就可以使用命令行的 git 工具（已经自带了 ssh 客户端）了
另外还有一个图形界面的 Git 项目管理工具。
在开始菜单里找到"Git"->"Git Bash"，会弹出 Git 命令窗口，可以在该窗口进行 Git 操作。
##Git 工作流程
工作区 working directory
添加 编辑 修改等

暂存区
暂存文件于此，统一一起提交到git仓库

版本库 git仓库 git repository
最终确定的文件保存到仓库，成为新的版本，对他人可见

一般工作流程如下：
1.克隆 Git 资源作为工作目录。
2.在克隆的资源上添加或修改文件。
3.如果其他人修改了，你可以更新资源。
4.在提交前查看修改。
5.提交修改。
6.在修改完成后，如果发现错误，可以撤回提交并再次修改并提交。
##Git初始化和仓库创建操作
（1）基本信息设置
设置用户名
  git config --global user.name "Your Name"

设置用户邮箱
  git config --global user.email "you@example.com"

注意：改设置在github仓库主页显示谁提交了文件


（2）初始化一个新的Git仓库
1.创建文件夹
命令:mkdir test,(直接右键新建也行）

2.在文件内初始化git(创建git仓库)
命令：git init

3.添加到暂存区
git add 文件名;

4.将文件从暂存区提交到仓库
git commit -m '描述'

（3）修改仓库文件
1.通过vi命令修改文件
2.通过git add 文件名，命令来添加到暂存区
3.通过git commit -m '描述'命令，将文件文件从暂存区提交到仓库
*其他常用的命令

（4）删除仓库文件
1.删除文件
直接文件夹中操作或者通过命令rm -rf fileName，来删除；rm test.php
rm 是 linux 系统下删除文件的命令。-r 代表删除这个下面的一切,f 表示不需要用户确认,直接执行
2.从git中删除文件
git rm test.php
3.提交操作
git commit -m '提交的描述'

git status：来查看状态
ls：显示目录
cd:下个目录
vi：改进版本，进入vi全屏幕编辑画面
cat：查看某个文件的内容
git config --list:查看用户名和邮箱列表
##GIt管理远程仓库
git除了可以操作本地仓库，还可以操作远程仓库。
使用远程仓库的目的：
备份、实现代码的共享集中化管理
```
将本地仓库同步到git远程仓库中

Git克隆操作
目的：将远程仓库（github对应的项目）复制到本地
代码：git clone 仓库地址
仓库地址由来：来自仓库中的 clone or download中...https://github.com/jCodeLife/Web-1.git

将本地仓库同步到git远程仓库中
git push
小结：
1.创建文件
2.将文件添加到暂存区 git add 文件名
3.添加到本地仓库 git commit -m '描述'
4.添加到远程仓库 git push
```
##Github Pages 搭建网站
1. 个人站点
访问
https：//用户名.github.io
搭建步骤：
（1）创建个人站点 -->新建仓库（注：仓库名必须是：用户名.github.io）
（2）在仓库下新建index.html的文件即可;
![1](https://upload-images.jianshu.io/upload_images/17785871-57641b1022a62e7f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![2](https://upload-images.jianshu.io/upload_images/17785871-0566fe8003b123af.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

注意：
1.github pages仅支持静态网页
2.仓库里面只能是.html文件


什么是github
Github是全球最大的社交编程及代码托管网站
Github可以托管各种git库，并提供一个web界面（用户名.github.io/仓库名）

##Project Pages 项目站点
访问：
https://用户名.github.io/仓库名
搭建步骤：
1. 进入项目主页，点击settings
2. 在settings页面点击点击 source 中的本来的 None ，使其变成 master 分支，
也就是作为部署github pages 的分支，然后点击 save。
页面会刷新，回到GitHub Pages，会发现多了一行链接，这就是你的 github pages 的网址了。
  其实网站就是：https://用户名.github.io/仓库名
![image.png](https://upload-images.jianshu.io/upload_images/17785871-90457a1df048608e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)











