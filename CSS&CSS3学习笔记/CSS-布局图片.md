通过CSS 布局图片
1. 圆角图片
```
.img1 {
    border-radius: 8px;
}
.img2 {
    border-radius: 50%;
}
```
2. 缩略图
```
img {
    border: 1px solid #ddd;
    border-radius: 4px;
    padding: 5px;
}
```
3. 响应式图片
即会自动适配各种尺寸的屏幕,也就是宽高auto，图片放大的尺寸不大于原始大小。
```
img {
    max-width: 100%;
    height: auto;
}
```
4. 卡片式图片
```
.cade {
  width: 80%;
  background-color: white;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}
```
5. 图片滤镜 
filter(滤镜) 属性,IE不支持
```
img {
    -webkit-filter: grayscale(100%); /* Chrome, Safari, Opera */
    filter: grayscale(100%);
}
```
6. 响应式图片相册
```
* {
    box-sizing: border-box;
}

.responsive {
    padding: 0 6px;
    float: left;
    width: 24.99999%;
}

@media only screen and (max-width: 700px){
    .responsive {
        width: 49.99999%;
        margin: 6px 0;
    }
}

@media only screen and (max-width: 500px){
    .responsive {
        width: 100%;
    }
}

.clearfix:after {
    content: "";
    display: table;
    clear: both;
}

```
7. 图片 Modal(模态)
```
<style>
.modal {
    display: none; /* Hidden by default */
    position: fixed; /* Stay in place */
    z-index: 1; /* Sit on top */
    padding-top: 100px; /* Location of the box */
    left: 0;
    top: 0;
    width: 100%; /* Full width */
    height: 100%; /* Full height */
    overflow: auto; /* Enable scroll if needed */
    background-color: rgb(0,0,0); /* Fallback color */
    background-color: rgba(0,0,0,0.9); /* Black w/ opacity */
}
</style>
<script>
img.onclick = function(){
    modal.style.display = "block";
    ...
}
span.onclick = function() { 
    modal.style.display = "none";
}
</script>
```
