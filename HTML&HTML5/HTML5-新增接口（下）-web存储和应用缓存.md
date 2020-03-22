在了解缓存前，先来了解web存储：
随着网络越来越进步和发展，并且应用也越来越复杂，数据也越来越大，在之前我们时使用cookie来存储，但是大小只能存储4k左右，并且cookie在解析的时候比较复杂，这样其实给开发带来了很多的不便。在H5中提出了一个新的解决方案：web存储。
##web存储
在H5中的web存储有两种存储方式：
1. sessionStorage
sessionStorage 会话存储的意思
sessionStorage的使用:存储数据到本地.存储的容量大概时5MB.

	**特点**:
		1.这个数据本质是存储在当前这一个页面的内存中.当换一个页面或者重新打开一个一样的页面,也是没有存储内容的.
		2.这个数据的生命周期:关闭当前页面结束.即关闭页面,数据会自动清除.
注意：sessionStorage是window的对象;<br>
常用方法:
	- **setItem(key,value)**:存储数据,以键值对的方式存储;
	- **getItem(key)**:获取数据,通过指定名称的key,获取对应的value值;如果找不到对应名称的key,那么获取的是null.
	- **removeItem(key)**:删除数据,通过指定名称的key来删除对那个的值;如果key值错误,不会报错,也不会删除数据.
	- **clear()**:清除,清空所有存储的内容;
```
<body>
	<input type="text" id="userName"><br/>
	<input type="button" value="设置数据" id="setData">
	<input type="button" value="获取数据" id="getData">
	<input type="button" value="删除数据" id="removeData">
	
	<script type="text/javascript">		
		//存储数据
		document.querySelector("#setData").onclick = function(){			
			var name = document.querySelector("#userName").value;
			window.sessionStorage.setItem("userName",name);
		};
		//获取数据
		document.querySelector("#getData").onclick = function(){
			var temp = window.sessionStorage.getItem("userName");
			alert(temp);
		}
		// 删除数据
		document.querySelector("#removeData").onclick = function(){
			window.sessionStorage.removeItem("userName");
			// 或者:
			// window.sessionStorage.clear();
		}
	</script>
</body>
```
2.localStorage
localStorage 本地存储的意思
- **特点**:
		1.存储的容量大概20MB.
		2.在不同浏览器也是不能共享数据的.但是在同一个浏览器的不同窗口中可以共享数据.
		3.永久生效,它的数据是存储在本地硬盘上,并不会随着页面或者浏览器的关闭而清除.
		4.如果想清除,必须手动清除
	注意:localStorage也是window的对象;
 - 常用方法与sessionStorage一致：
		
**setItem(key,value)**:存储数据,以键值对的方式存储;
		**getItem(key)**:获取数据,通过指定名称的key,获取对应的value值;如果找不到对应名称的key,那么获取的是null.
		**removeItem(key)**:删除数据,通过指定名称的key来删除对那个的值;如果key值错误,不会报错,也不会删除数据.
		**clear()**:清除,清空所有存储的内容;
```
<body>
	<input type="text" id="userName"><br/>
	<input type="button" value="设置数据" id="setData">
	<input type="button" value="获取数据" id="getData">
	<input type="button" value="删除数据" id="removeData">
	
	<script type="text/javascript">		
		//存储数据
		document.querySelector("#setData").onclick = function(){			
			var name = document.querySelector("#userName").value;
			window.localStorage.setItem("userName",name);
		};
		//获取数据
		document.querySelector("#getData").onclick = function(){
			var temp = window.localStorage.getItem("userName");
			alert(temp);
		}
		// 删除数据
		document.querySelector("#removeData").onclick = function(){
			window.localStorage.removeItem("userName");
			// 或者:
			// window.localStorage.clear();
		}
	</script>
</body>
```

#应用缓存 
一般在网络断开的时候，我们无法访问网页。但是我们想正常显示，那可以把网页缓存在本地，这样没有网络的时候我也一样可以浏览这些网页。但是浏览器的默认缓存有个问题，我们没有选择，要么缓存页面中的所有内容，要么都不缓存。H5针对类似这种问题，增加了一个应用程序缓存的概念，通过这个应用缓存，我们可以缓存我们想缓存的资源。

概念：使用HTML5，通过创建cache manifest文件，可以轻松的创建web应用的离线版本。在网络断开的时候还能看到这个页面。

优势：
1.可配置需要缓存的资源；
2.网络无连接应用任然可用；
3.本地读取缓存资源效率高，提升访问速度，增强用户体验；
4.减少请求，缓解服务器负担；

**实现应用缓存**
- Cache manifest基础：
1. 如需启动应用程序缓存，请在文档的<html>标签中包含manifest属性
```
<html manifest="demo.appcache">
```
2. manifest="应用程序缓存清单文件的路径,建议文件的扩展名时appcache,这个文件的本质就是一个文本文件" 
3. 每个指定的manifest的页面在用户对其访问时都会被缓存下来。如果未指定manifest属性，则页面不会被缓存（除非在manifest文件中直接指定了该页面）
4.  **注意，manifest文件需要配置正确的MIME-type，即：“text/cache-manifest”，必须在web服务器上进行配置。**
![image.png](https://upload-images.jianshu.io/upload_images/17785871-9298874a2333e61d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/17785871-06fcc7ecc25b024e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/17785871-89aed2030aef46e1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



- manifest文件：
1. 概念：manifest文件时简单的文本文件，它告知浏览器被缓存的内容和不缓存的内容。
2. manifest文件可以分成4个部分：
 (1) CACHE MANIFEST    开始，开头第一句
  (2)CACHE：  在此标题下列出的文件将在首次下载后进行缓存；
  (3)NETWORK：在此标题下列出的文件需要与服务器链接，且不会被缓存；
 (4)FALLBACK：在此标题下列出的文件规定，当页面无法访问时（比如404页面），使用指定文件代替。

如下demo.appcache文件，可以理解为配置文件：
```
CACHE MANIFEST
#CACHE MANIFEST这句代码，必须时当前文档的第一句。
#井号后面是用来写注释的

#需要缓存的文件清单列表
CACHE:
../images/1.jpg
../images/2.jpg
../images/3.jpg
#表示这三个资源需要缓存下来，不需要重新。

#配置每一次都要重新从服务器获取的文件清单列表
NETWORK:
../images/4.jpg
../images/5.jpg
#表示这两个资源不缓存。

#如果文件无法获取，则使用指定的文件替代
FALLBACK:
../images/5.jpg  ../images/6.jpg
#找不到../images/5.jpg，就用另外一个文件../images/6.jpg替换。
```

注：
1.如果想缓存所有文件，使用*：
```
CACHE:
*
```
2.如果想代替的时候，表示所有找不到文件、任意以文件。使用/
```
FALLBACK:
/  ../images/6.jpg
```
表示所有找不到文件，都用../images/6.jpg文件代替。

