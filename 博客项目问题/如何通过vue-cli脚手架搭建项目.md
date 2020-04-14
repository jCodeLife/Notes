1.安装nodejs
2.通过node自带的npm，安装淘宝镜像cnpm
	npm install -g cnpm --registry=https://registry.npm.taobao.org
3.通过cnpm安装vue-cli
	cnpm install vue-cli -g
	安装输入：vue -V
	2.9.6
	出现版本 表示安装成功
4.创建基于webpack模板的项目
	vue init webpack WEBSTORE
5.  进入项目目录，运行项目
	cd WEBSTORE
	npm run dev
注意：在安装过程中可能网络不好导致数据丢失，造成很多报错信息，
可以在项目目录输入：cnpm instal，安装项目所需要的依赖文件。

运行会见到如下信息：
 	DONE  Compiled successfully in 5134ms
	 I  Your application is running here: http://localhost:8080
表示搭建成功！
6.目录简介：
build------------------webpack相关配置文件（都已经配置好，一般无需再配置）
config-----------------vue基本的配置文件（可配置箭筒端口，打包输出等）
node_modules--------依赖
src----------------------项目核心文件
	src/assets---------------静态资源（如css,less,sass和一些外部js文件）
	src/components--------公共组件
	src/router---------------路由
	App.vue-----------------根组件*
	main.js-------------------入口*
static-----------------------纯静态资源（一般放置图片类）
.babelrc--------------------babel编译相关参数设置
.editorconfig---------------代码格式
.gitignore-------------------git上传需要忽略的文件配置
.postcssrc.js-----------------转化css的工具
index.html------------------主页*
package.json---------------项目基本信息
README.md----------------项目说明
