### 页面元信息类标签
元信息多数情况下是给浏览器、搜索引擎等机器阅读的，有时候这些信息会在页面之外显示给用户，有时候则不会。

### Head
主要作为容器存放其他语义化标签

### title
表示文档标题，
语义类标签中也有一组表示标题的标签：h1-h6。
heading和title之前的区别
**title**表示整个页面的标题，而**heading**则是用于页面的展示，默认具有上下文，并且有链接辅助，所以可以简写

### base
为URL的相对地址提供一个基础

### meta
meta标签是一组键值对，它是一种通用的元信息表示标签
在head中可以出现多次，基本用法如下：
```
  <meta name=application-name content=lsForums>
```
这个标签表示页面所在的web-application，名为IsForums。
常见meta标签如下：
```
<!-- 编码 -->
<meta charset="UTF-8">

<!-- 移动端缩放 -->
<meta name="viewport" content="width=device-width,initial-scale=1,minimum-scale=1,maximum-scale=1,user-scalable=no">

<!-- 默认使用最新浏览器 -->
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">

<!-- 搜索引擎抓取 -->
<meta name="robots" content="index,follow">

<!-- 不被网页(加速)转码 -->
<meta http-equiv="Cache-Control" content="no-siteapp">

<!-- 删除苹果默认的工具栏和菜单栏 -->
<meta name="apple-mobile-web-app-capable" content="yes">

<!-- 设置苹果工具栏颜色 -->
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">