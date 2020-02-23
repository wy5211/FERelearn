### HTML替换型元素

##### script
```
<script type="text/javascript">
console.log("Hello world!");
</script>

<script type="text/javascript" src="my.js"></script>
```
凡是替换型元素，都是使用src属性来引用文件的，而我们之前的课程中已经讲过，链接型元素是使用href标签的

##### img
img标签的作用是引入一张图片。
如果一定不想要引入独立文件，可以使用data uri
```
<img src='data:image/svg+xml;charset=utf8,<svg version="1.1" xmlns="http://www.w3.org/2000/svg"><rect width="300" height="100" style="fill:rgb(0,0,255);stroke-width:1;stroke:rgb(0,0,0)"/></svg>'/>
```
img标签可以使用width和height指定宽度和高度，从性能的角度考虑，建议你同时给出图片的宽高，因为替换型元素加载完文件后，如果尺寸发生变换，会触发重排版。
alt属性，这个属性很难被普通用户感知，对于视障用户非常重要，可以毫不夸张地讲，给img加上alt属性，已经做完了可访问性的一半
img标签还有一组重要的属性，那就是srcset和sizes，它们是src属性的升级版
```
<img srcset="elva-fairy-320w.jpg 320w,
             elva-fairy-480w.jpg 480w,
             elva-fairy-800w.jpg 800w"
     sizes="(max-width: 320px) 280px,
            (max-width: 480px) 440px,
            800px"
     src="elva-fairy-800w.jpg" alt="Elva dressed as a fairy">
```

##### picture
picture元素可以根据屏幕的条件为其中的img元素提供不同的源
```
<picture>
  <source srcset="image-wide.png" media="(min-width: 600px)">
  <img src="image-narrow.png">
</picture>
```

##### video
video标签可以使用source标签来指定接入多个视频源。
```
<video controls="controls" >
  <source src="movie.webm" type="video/webm" >
  <source src="movie.ogg" type="video/ogg" >
  <source src="movie.mp4" type="video/mp4">
  You browser does not support video.
</video>
```
video中还支持一种标签：track。track是一种播放时序相关的标签，它最常见的用途就是字幕。track标签中，必须使用 srclang 来指定语言，此外，track具有kind属性，共有五种。
* subtitles：就是字幕了，不一定是翻译，也可能是补充性说明
* captions：报幕内容，可能包含演职员表等元信息，适合听障人士或者没有打开声音的人了解音频内容
* descriptions：视频描述信息，适合视障人士或者没有视频播放功能的终端打开视频时了解视频内尔用
* chapters：用于浏览器视频内容。
* metadata：给代码提供的元信息，对普通用户不可见。
##### audio
```
<audio controls>
  <source src="song.mp3" type="audio/mpeg">
  <source src="song.ogg" type="audio/ogg">
  <p>You browser does not support audio.</p>
</audio>
```

##### iframe
不推荐使用
```
<iframe src="http://time.geekbang.org"></iframe>
```
在新标准中，为iframe加入了sandbox模式和srcdoc属性
```
<iframe sandbox srcdoc="<p>Yeah, you can see it <a href="/gallery?mode=cover&amp;amp;page=1">in my gallery</a>."></iframe>
```
