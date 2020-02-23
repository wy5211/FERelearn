### CSS动画与交互

##### CSS animation属性和transition属性
animation基本用法
```
@keyframes mykf {
  from {background: red;}
  to {background: yellow;}
}

div {
  animation:mykf 5s infinite;
}
```
实际上animation分成六个部分：
* animation-name 动画的名称，这是一个keyframes类型的值（我们在第9讲“CSS语法：除了属性和选择器，你还需要知道这些带@的规则”讲到过，keyframes产生一种数据，用于定义动画关键帧）；
* animation-duration 动画的时长；
* animation-timing-function 动画的时间曲线；
* animation-delay 动画开始前的延迟；
* animation-iteration-count 动画的播放次数；
* animation-direction 动画的方向。

transition与animation相比来说，是简单得多的一个属性。
* transition-property 要变换的属性；
* transition-duration 变换的时长；
* transition-timing-function 时间曲线；
* transition-delay 延迟。

##### 三次贝塞尔曲线
你能从很多CSS的资料中都找到了贝塞尔曲线，但是为什么CSS的时间曲线要选用（三次）贝塞尔曲线呢？
贝塞尔曲线是一种插值曲线，它描述了两个点之间差值来形成连续的曲线形状的规则。
浏览器中一般都采用了数值算法，其中公认做有效的是牛顿积分，我们可以看下JavaScript版本的代码：