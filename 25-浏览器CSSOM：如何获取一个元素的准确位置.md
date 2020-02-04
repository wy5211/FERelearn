### CSSOM

#### CSSOM
CSS中样式表的模型，也就是CSSOM的本体。

#### CSSOM View
CSSOM View 这一部分的API，可以视为DOM API的扩展，它在原本的Element接口上，添加了显示相关的功能，这些功能，又可以分成三个部分：窗口部分，滚动部分和布局部分

##### 窗口 API
窗口API用于操作浏览器窗口的位置、尺寸等。
* moveTo(x, y) 窗口移动到屏幕的特定坐标；
* moveBy(x, y) 窗口移动特定距离；
* resizeTo(x, y) 改变窗口大小到特定尺寸；
* resizeBy(x, y) 改变窗口大小特定尺寸。

##### 滚动 API
要想理解滚动，首先我们必须要建立一个概念，在PC时代，浏览器可视区域的滚动和内部元素的滚动关系是比较模糊的，但是在移动端越来越重要的今天，两者必须分开看待，两者的性能和行为都有区别。
##### 视口滚动API
可视区域（视口）滚动行为由window对象上的一组API控制
* scrollX 是视口的属性，表示X方向上的当前滚动距离，有别名 pageXOffset；
* mscrollY 是视口的属性，表示Y方向上的当前滚动距离，有别名 pageYOffset；
* scroll(x, y) 使得页面滚动到特定的位置，有别名scrollTo，支持传入配置型参数 {top, left}；
* scrollBy(x, y) 使得页面滚动特定的距离，支持传入配置型参数 {top, left}。

要想监听视口滚动事件，我们需要在document对象上绑定事件监听函数：
```
document.addEventListener("scroll", function(event){
  //......
})
```
##### 元素滚动API
在Element类（参见DOM部分），为了支持滚动，加入了以下API。
* scrollTop 元素的属性，表示Y方向上的当前滚动距离。
* scrollLeft 元素的属性，表示X方向上的当前滚动距离。
* scrollWidth 元素的属性，表示元素内部的滚动内容的宽度，一般来说会大于等于元素宽度。
* scrollHeight 元素的属性，表示元素内部的滚动内容的高度，一般来说会大于等于元素高度。
* scroll(x, y) 使得元素滚动到特定的位置，有别名scrollTo，支持传入配置型参数 {top, left}。
* scrollBy(x, y) 使得元素滚动到特定的位置，支持传入配置型参数 {top, left}。
* scrollIntoView(arg) 滚动元素所在的父元素，使得元素滚动到可见区域，可以通过arg来指定滚到中间、开始或者就近。
可滚动的元素也支持scroll事件，我们在元素上监听它的事件即可：
```
element.addEventListener("scroll", function(event){
  //......
})
```

#### 布局API
布局API，这是整个CSSOM中最常用到的部分，我们同样要分成全局API和元素上的API。
##### 全局尺寸信息
window对象上提供了一些全局的尺寸信息，它是通过属性来提供的，我们一起来了解一下来这些属性。
![avatar](https://static001.geekbang.org/resource/image/b6/10/b6c7281d86eb7214edf17069f95ae610.png)
##### 元素的布局信息
* getClientRects()
* getBoundingClientRect()

getClientRects 会返回一个列表，里面包含元素对应的每一个盒所占据的客户端矩形区域，这里每一个矩形区域可以用 x, y, width, height 来获取它的位置和尺寸。
getBoundingClientRect ，这个API的设计更接近我们脑海中的元素盒的概念，它返回元素对应的所有盒的包裹的矩形区域，需要注意，这个API获取的区域会包括当overflow为visible时的子元素区域。