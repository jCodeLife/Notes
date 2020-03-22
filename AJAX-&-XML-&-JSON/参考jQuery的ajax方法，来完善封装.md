官方传值
```
$.ajax({
   type: "post",
   url: "some.php",
   data: "name=John&location=Boston",
   success: function(msg){
     alert( "Data Saved: " + msg );
   }
});
```
在使用自己封装的代码的时候，感觉跟jQuery官方的ajax还是有一定的差异，所以进一步完善
首先，传递请求类型的大小写，官方的是都可以传递成功：
第二，我们传递的是很多个参数，参数的顺序必须保持一致。官方传递的是一个对象，对象里面的值，不要求先后顺序。
第三，我们穿的数据用的名字是obj，官方用的是data，语义更适合。

解决第一个问题使用toLowerCase()或者toUpperCase()将类型转成大写或小写在对比;
解决第二个问题将传参换成一个对象；之前里面用的参数通过：对象名.属性名的形式获取。
解决第三个问题，数据换名称data

这样基本差不多了：
```
function ajax(option){//type,url,obj,timeout,success,error将所有参数换成一个对象{}
        //  0.将对象转换成字符串
        var str = objToString(option.data); 

        //  1.创建一个异步对象xmlhttp；
        var xmlhttp,timer; 
        if (window.XMLHttpRequest){
          xmlhttp=new XMLHttpRequest(); 
        } else{// code for IE6, IE5 
          xmlhttp=new ActiveXObject("Microsoft.XMLHTTP"); 
        }

        //  2.设置请求方式和请求地址； 
        // 判断请求的类型是POST还是GET
        if (option.type.toLowerCase() === 'get') {
            xmlhttp.open(option.type,option.url+"?t=" +str,true);
        //  3.发送请求；
            xmlhttp.send();
        }else{
                xmlhttp.open(option.type,option.url,true);
                // 注意：在post请求中，必须在open和send之间添加HTTP请求头：setRequestHeader(header,value);
                xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded"); 
            //  3.发送请求；
                xmlhttp.send(str);

        }   

        //  4.监听状态的变化；
        xmlhttp.onreadystatechange = function(){
            clearInterval(timer);
            if (xmlhttp.readyState === 4) {
                if (xmlhttp.status >= 200 && xmlhttp.status < 300 || xmlhttp.status == 304) {
                    //  5.处理返回的结果；
                    option.success(xmlhttp);//成功后回调；
                }else{
                   option. error(xmlhttp);//失败后回调；
                }                   
            }
        }
    }

    //处理obj 
    function objToString(data){
      data.t = new Date().getTime();
      var res =[];
      for(var key in data){
        //需要将key和value转成非中文的形式，因为url不能有中文。使用encodeURIComponent();
        res.push(encodeURIConponent(key) + " = " +encodeURIConponent(data.[key]));
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
