视频Video 和 音频Audio

1. **视频Video**

(1)<video>：定义视频

video可选属性
- **autoplay**： 自动播放。值是autoplay
- **controls**： 控制/控件。值是controls
- **height**： 视频播放器的高度。值是pixels
- **width** ：宽度。值是pixels
- **loop**：环、圈、循环播放的意思。值是loop
- **muted**：视频的音频输出为静音。值是muted
- **poster**：贴画、海报，表示点击播放前的图片。值是URL
- **preload**：预加载，视频在页面加载时加载，并预备播放。使用 "autoplay"，忽略该属性。值auto/metadata/none
- **src**：视频的 URL。值是URL

(2)**<source>：定义多种媒体资源**
**目前，<video> 元素支持三种视频格式：MP4、WebM、Ogg。**
- **MP4 = MPEG 4文件使用 H264 视频编解码器和AAC音频编解码器**
- **WebM = WebM 文件使用 VP8 视频编解码器和 Vorbis 音频编解码器**
- **Ogg = Ogg 文件使用 Theora 视频编解码器和 Vorbis音频编解码器**

三种视频格式对应的 MIME 类型
- **MP4是：video/mp4**
- **WebM是：video/webm**
- **Ogg是：video/ogg**

source标签属性有：src和type，分别表示视频资源url和视频的MIME 类型
```
<!--
<video> 标签可以将视频内容嵌入到HTML文档中:
<source>标签可以定义多种媒体资源，对应不同浏览器支持的视频格式
-->
<video width="320" height="240" controls> 
<source src="movie.mp4" type="video/mp4"> 
<source src="movie.ogg" type="video/ogg"> 
您的浏览器不支持 video 标签。 
</video>

提示：可以在 <video> 和 </video> 标签之间放置文本内容，这样不支持 <video> 元素的浏览器就可以显示出该标签的信息。
```

2. **音频Audio**

(1) 音频格式
**目前, <audio>元素支持三种音频格式文件: MP3, Wav, 和 Ogg:**

(2) 音频格式的MIME类型
MP3:audio/mpeg
Ogg:audio/ogg
Wav:audio/wav
```
<audio controls> 
  <source src="horse.ogg" type="audio/ogg"> 
  <source src="horse.mp3" type="audio/mpeg"> 
  您的浏览器不支持 audio 元素
<!--
可以在 <audio> 和 </audio> 之间放置文本内容，
这些文本信息将会被显示在那些不支持 <audio> 标签的浏览器中。
-->
</audio>

```
(3)   audio可选属性
- **autoplay**： 自动播放。值是autoplay
- **controls**： 控制/控件。值是controls
- **loop**：环、圈、循环播放的意思。值是loop
- **muted**：视频的音频输出为静音。值是muted
- **preload**：预加载，视频在页面加载时加载，并预备播放。使用 "autoplay"，忽略该属性。值auto/metadata/none
- **src**：视频的 URL。值是URL

(4) audio里的source标签跟video里的用法一致
```
<>
<audio controls> 
<source src="horse.ogg" type="audio/ogg"> 
<source src="horse.mp3" type="audio/mpeg"> 
您的浏览器不支持 audio 元素。 
</audio>
```

另外了解：<track>标签
<track>标签定义在媒体播放器文本轨迹
<track> 标签用作 <audio> 元素和 <video> 元素的子级，它允许您指定定时文本轨道（或基于时间的数据），采用 WebVTT 格式（.vtt 文件）
Firefox and Safari不支持该属性
```
带有两个字幕轨道的视频：
<video width="320" height="240" controls> 
<source src="forrest_gump.mp4" type="video/mp4"> 
<source src="forrest_gump.ogg" type="video/ogg"> 
<track src="subtitles_en.vtt" kind="subtitles" srclang="en" 
label="English"> 
<track src="subtitles_no.vtt" kind="subtitles" srclang="no" 
label="Norwegian"> 
</video> 
```
可选的属性:default默认轨道、kind文本轨道的文本类型、label文本轨道的标签和标题、src轨道文件的 URL、srclang轨道文本数据的语言（必需）
