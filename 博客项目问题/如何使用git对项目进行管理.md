1.先安装 Git,
	Git 各平台安装包下载地址https://git-scm.com/downloads
2.基本信息设置
	$ git config --global user.name "lbj"
	$ git config --global user.email "bingjin.liao@outlook.com"
注意：该设置后，在github仓库主页显示谁提交了文件
3.在项目目录上，初始化一个新的Git仓库
	git init
4.常用git命令
	git add .-----添加到暂存区
	git commit -m '描述'---------将文件从暂存区提交到仓库
	git status：来查看状态
5.GIt管理远程仓库
使用远程仓库的目的：
	备份、实现代码的共享集中化管理
首先，在远程创建对应仓库，
	如在github中创建，创建后，出现一个仓库的地址：https://github.com/jCodeLife/webstore.git
接着，在本地仓库设置（添加远程仓库），告诉本地仓库你所对应的远程仓库在哪：
	git remote add 远程名称 远程地址
	如：git remote add webstoreAtGithub https://github.com/jCodeLife/webstore.git
	此时，可以查查看通过命令：
		git remote   列出当前本地仓库所连接的所以远程仓库
		git remote   -v  会有详细信息
接着，将本地仓库同步到git远程仓库中（上传代码）
	git push -u 远程名 分支名
	如：git push -u webstoreAtGithub master
	master表示默认的分支名
	origin 表示默认远程仓库名称，如果没有设置远程仓库名称
当，需要将远程仓库克隆到本地时，通过：
	git clone 仓库地址
通过：git pull命令，拉取远程更新的文件
