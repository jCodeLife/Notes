**简介**
1. AJAX = 异步 JavaScript 和 XML。
2. AJAX是一种在无须重新加载整个页面的情况下，能够更新部分网页的技术。


##AJAX五部曲
1. **创建一个异步对象xmlhttp；**
```
var xmlhttp= new XMLHttpRequest(); 
```
XMLHttpRequest 的对象的三个重要的属性：
- onreadystatechange：请求状态改变事件
- readyState：请求状态码
- status：http状态码
- responseText：获得字符串形式的响应数据
- responseXML：或者XML形式的响应数据
2. **设置请求方式和请求地址**；
通过异步对象的open(method,url,async)
第一个参数：method：请求的类型；GET 或 POST
第二个参数：url：文件在服务器上的位置
第三个参数：async：true（异步）或 false（同步）,这个永远传true，因为AJAX存在的意义就是发异步请求。  
```
xmlhttp.open("GET","01-ajax-get.php",true);
```
3. **发送请求**；
通过异步对象的send()发送请求
```
xmlhttp.send();
```
4. **监听状态的变化**；
通过异步对象的onreadystatechange 事件来监听发送的状态变化：
当发送一个请求后，客户端需要确定这个请求什么时候会完成，因此，XMLHttpRequest对象提供了onreadystatechange事件机制来捕获请求的状态，继而实现响应。
当请求被发送到服务器时，我们需要执行一些基于响应的任务。
每当readyState改变时，就会触发onreadystatechange事件。
readyState存有 XMLHttpRequest 的状态。总共5个状态：从0到4发生变化：
	- 0: 请求未初始化，还没有调用 open()。 
	- 1: 服务器连接已建立**，但是还没有发送，还没有调用 send()。    
	- 2: 请求已接收，正在处理中（通常现在可以从响应中获取内容头）。  
	- 3: 请求处理中，通常响应中已有部分数据可用了，没有全部完成。  
	- 4: 请求已完成，且响应已就绪
当状态为4时，此阶段确认全部数据都已经解析为客户端可用的格式，解析已经完成。值为4表示数据解析完毕，可以通过的XMLHttpRequest对象的属性取得数据。

5. **处理返回的结果**；
根据状态的变化，处理返回的结果，但在处理结果之前得判断一下，我们请求是否是成功的。通过异步对象的另一个属性status，表示http状态码，通过这个状态码来判断请求是否成功，当成功的时候处理成功返回的的结果。
```
//4.监听状态变化
xmlhttp.onreadystatechange = function(){
 // 判断当前状态改变是请求完毕的状态吗
 if (xmlhttp.readyState === 4) {
	if (xmlhttp.status >= 200 && xmlhttp.status < 300 || xmlhttp.status == 304) {
		// 	5.处理返回的结果；
		//console.log("成功的接收到服务器返回的数据");
       //通过异步对象的responseText属性来获取服务器返回的字符串
       console.log(xmlhttp.responseText);
	}else{
		console.log("不成功！");
	}	
 }
}		
```
Ajax-GET基本使用：
```
<script type="text/javascript">
	window.onload = function(ev){
		var oBtn = document.querySelector("button");
		oBtn.onclick = function(ev1){
		// AJAX五部曲：
		// 	1.创建一个异步对象xmlhttp；
		var xmlhttp; 
		if (window.XMLHttpRequest) 
		  {// code for IE7+, Firefox, Chrome, Opera, Safari 
		  xmlhttp=new XMLHttpRequest(); 
		  } 
		else 
		  {// code for IE6, IE5 
		  xmlhttp=new ActiveXObject("Microsoft.XMLHTTP"); 
		  }
			   // 
		// 	2.设置请求方式和请求地址；				
			xmlhttp.open("GET","01-ajax-get.php",true);
		// 	3.发送请求；
			xmlhttp.send();
		// 	4.监听状态的变化；
		xmlhttp.onreadystatechange = function(){
		// 判断当前状态改变是请求完毕的状态吗
			if (xmlhttp.readyState === 4) {
				if (xmlhttp.status >= 200 && xmlhttp.status < 300 || xmlhttp.status == 304) {
					// 	5.处理返回的结果；
					console.log("成功的接收到服务器返回的数据");
				}else{
					console.log("不成功！");
				}					
			}
		}			
	}
</script>
```
##Ajax-GET-IE兼容问题：
1. 在IE中创建异步对象的问题：
所有现代浏览器（IE7+、Firefox、Chrome、Safari 以及 Opera）均内建 XMLHttpRequest 对象。
但老版本的 Internet Explorer （IE5 和 IE6）使用 ActiveX 对象： 
```
var xmlhttp; 
if (window.XMLHttpRequest) {// code for IE7+, Firefox, Chrome, Opera, Safari 
  xmlhttp=new XMLHttpRequest(); 
}else {// code for IE6, IE5 
  xmlhttp=new ActiveXObject("Microsoft.XMLHTTP"); 
}
```
2. AJAX在IE中的缓存问题：
在IE浏览器中，如果通过Ajax发送GET请求，那么IE浏览器认为，同一个URL只有一个结果。如果地址没有发生变化，它就会把上一次返回的结果，直接返回。这样我们不能实时的拿到变化后的数据。所以要想我们拿到数据是实时的，必须保证每次的URL都是不一样的，如百度的：
```
htttps://www.baidu.com/?t=46541324685741135456
```
后面这个参数就是为了保证每次的url不一样，兼容低版本的IE。
那么
我们自己来实现动态的URL我们可以使用如下两个方法：
- Math.random();随机数
- new Date().getTime();1970.01.01至当前的毫秒数。

所以在IE中发送ajax请求，当设置请求地址的时候，我们可以改成：
```
xmlhttp.open("GET","ajax-get.txt?t=" + (new Date().getTime()),true);
```
##Ajax-GET封装
一、
```
function ajax(url,obj,success,error){
		// 	0.将对象转换成字符串
		var str = objToString(obj); //obj就是为了将url和传递的数据分开，可以把它当成一个对象，在传递的过程中，将obj变成对应的字符串拼接到url的后面。这样数据也传进去了。另外为了兼容IE,可以在obj转换的过程中加个obj.t = new Date().getTime();
		// 	1.创建一个异步对象xmlhttp；
		var xmlhttp; 
		if (window.XMLHttpRequest){// code for IE7+, Firefox, Chrome, Opera, Safari 
		  xmlhttp=new XMLHttpRequest(); 
		} else{// code for IE6, IE5 
		  xmlhttp=new ActiveXObject("Microsoft.XMLHTTP"); 
		}
		// 	2.设置请求方式和请求地址；	
			//xmlhttp.open("GET",url,true);
			xmlhttp.open("GET",url+"?t=" +str;	
		// 	3.发送请求；
			xmlhttp.send();
		// 	4.监听状态的变化；
		xmlhttp.onreadystatechange = function(){
			if (xmlhttp.readyState === 4) {
				if (xmlhttp.status >= 200 && xmlhttp.status < 300 || xmlhttp.status == 304) {
					// 	5.处理返回的结果；
					success(xmlhttp);//成功后回调；
				}else{
					error(xmlhttp);//失败后回调；
				}					
			}
		}
}
function objToString(obj){
  obj.t = new Date().getTime();
  var res =[];
  for(var key in obj){
    res.push(key + " = " +obj.[key]);
  }
  return res.join("&");
}
```
注意：
1. IE中的兼容问题
2. 我们传递url的时候需要传递我们添加的数据，但是那样写不太好，我们可以加传递一个参数obj，这个obj就是为了将url和传递的数据分开，可以把它当成一个对象，在传递的过程中，将obj变成对应的字符串拼接到url的后面。这样数据也传进去了。另外为了兼容IE,可以在obj转换的过程中加个obj.t = new Date().getTime();

二、
当前我们封装的ajax方法还有两个细节需要处理一下：
1. 当我们利用我们的ajax放的发送一个请求到远处服务器时，我们需要等待远程服务器去响应我们的请求，等待远程服务器将响应的结果返回给我们，但是这个响应的速度是不确定的，因为响应的速度是由本地网络和远程服务器的网速等共同决定的，所以我们不可能一直等待服务器的响应。那么这里我们需要新增另外一个功能：设置超时时间的功能，即告诉它我的请求会等待多长的时间，如果这么长的时间内都没有响应我们发送的请求，那我就在这里自动的终止这次请求；
```
function ajax(url,obj,timeout,success,error){
        //  0.将对象转换成字符串
        var str = objToString(obj); 
        //  1.创建一个异步对象xmlhttp；
        var xmlhttp,timer; 
        if (window.XMLHttpRequest){// code for IE7+, Firefox, Chrome, Opera, Safari 
          xmlhttp=new XMLHttpRequest(); 
        } else{// code for IE6, IE5 
          xmlhttp=new ActiveXObject("Microsoft.XMLHTTP"); 
        }
        //  2.设置请求方式和请求地址；  
            //xmlhttp.open("GET",url,true);
            xmlhttp.open("GET",url+"?t=" +str;  
        //  3.发送请求；
            xmlhttp.send();
        //  4.监听状态的变化；
        xmlhttp.onreadystatechange = function(){
        	clearInterval(timer);
            if (xmlhttp.readyState === 4) {
                if (xmlhttp.status >= 200 && xmlhttp.status < 300 || xmlhttp.status == 304) {
                    //  5.处理返回的结果；
                    success(xmlhttp);//成功后回调；
                }else{
                    error(xmlhttp);//失败后回调；
                }                   
            }
        }
	}
	function objToString(obj){
	  obj.t = new Date().getTime();
	  var res =[];
	  for(var key in obj){
	    res.push(key + " = " +obj.[key]);
	  }
	  return res.join("&");
	}
	//判断外界是否传入了超时时间
	if(timeout){
		timer = setInterval(function(){
			xmlhttp.abort();//中断请求
			clearInterval(timer);
		},timeout);
	}
```
2. 上面的情况还有一个问题，在我们发送一个请求的时候，我们的URL当中是不能出现中文的。
我们在百度上面搜索关键字时，如张三，通常会看到地址栏那里是：https://www.baidu.com/s?wd=张三；但是我们如果复制到编辑器，会变成https://www.baidu.com/s?wd=%E5%BC%AO%E4%B8%90这样的。其实在它提交请求的时候，并不是中文的张三，而是用%E5%BC%AO%E4%B8%90这段字符表示张三。而张三这个中文是浏览器显示给你的，真正提交的是%E5%BC%AO%E4%B8%90这段字符串。
那么我们需要在专门处理obj的函数里面，将中文处理了在传入服务器。
需要将key和value转成非中文的形式，因为url不能有中文。使用encodeURIComponent()转码;URL中只能出现字母 数字 下划线和ASCII码

最后完善ajax：
```
function ajax(url,obj,timeout,success,error){
        //  0.将对象转换成字符串
        var str = objToString(obj); 
        //  1.创建一个异步对象xmlhttp；
        var xmlhttp,timer; 
        if (window.XMLHttpRequest){// code for IE7+, Firefox, Chrome, Opera, Safari 
          xmlhttp=new XMLHttpRequest(); 
        } else{// code for IE6, IE5 
          xmlhttp=new ActiveXObject("Microsoft.XMLHTTP"); 
        }
        //  2.设置请求方式和请求地址；  
            //xmlhttp.open("GET",url,true);
            xmlhttp.open("GET",url+"?t=" +str;  
        //  3.发送请求；
            xmlhttp.send();
        //  4.监听状态的变化；
        xmlhttp.onreadystatechange = function(){
        	clearInterval(timer);
            if (xmlhttp.readyState === 4) {
                if (xmlhttp.status >= 200 && xmlhttp.status < 300 || xmlhttp.status == 304) {
                    //  5.处理返回的结果；
                    success(xmlhttp);//成功后回调；
                }else{
                    error(xmlhttp);//失败后回调；
                }                   
            }
        }
	}
	function objToString(obj){
	  obj.t = new Date().getTime();
	  var res =[];
	  for(var key in obj){
	  	//需要将key和value转成非中文的形式，因为url不能有中文。使用encodeURIComponent()转码;URL中只能出现字母 数字 下划线和ASCII码
	    res.push(encodeURIConponent(key) + " = " +encodeURIConponent(obj.[key]));
	  }
	  return res.join("&");
	}

	//判断外界是否传入了超时时间
	if(timeout){
		timer = setInterval(function(){
			xmlhttp.abort();//中断请求
			clearInterval(timer);
		},timeout);
	}
```

