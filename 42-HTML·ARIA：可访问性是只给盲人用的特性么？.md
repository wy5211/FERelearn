### HTML·ARIA


#### 综述
ARIA给HTML元素添加的一个核心属性就是role
```
<span role="checkbox" aria-checked="false" tabindex="0" aria-labelledby="chk1-label">
</span> <label id="chk1-label">Remember my preferences</label>
```
这里我们给一个span添加了checkbox角色，这样，表示我们这个span被用于checkbox，这意味着，我们可能已经用JS代码绑定了这个span的click事件，并且以checkbox的交互方式来处理用户操作。
同时，ARIA系统还提供了一系列ARIA属性给checkbox这个role，这意味着，**我们可以通过HTML属性变化来理解这个JavaScript组件的状态**，读屏软件等三方客户端，就可以理解我们的UI变化，这正是ARIA标准的意义。
role的定义是一个树形的继承关系，我们先来理解一下它的整体结构：
![avatar](https://static001.geekbang.org/resource/image/ae/69/aeccf64871b309735054912fbbb18a69.jpg)
widget表示一些可交互的组件，structure表示文档中的结构，window则代表窗体。

#### Widget角色
表示一个可交互的组件
![avatar](https://static001.geekbang.org/resource/image/10/dd/10ea9eb62d60fb4bfb18c27da50836dd.jpg)
按照继承关系给出一份列表和简要说明：
![avatar](https://static001.geekbang.org/resource/image/03/f1/038e1152c9bddc7ed864d271691d17f1.jpeg)

#### structure角色
结构角色其实跟HTML5中不少新标签作用重合了，这里建议优先使用HTML5标签。这部分角色的作用类似于语义化标签
![avatar](https://static001.geekbang.org/resource/image/b2/7a/b21a82fd68a885f751123f48a7e26b7a.jpg)
这里我们需要特别提出Landmark角色这个概念，Landmark角色直接翻译是地标，它是ARIA标准中总结的Web网页中最常见的8个结构，Landmark角色实际上是section的子类，这些角色在生成页面摘要时有很大可能性需要被保留，它们是：
![avatar](https://static001.geekbang.org/resource/image/9a/75/9aee7029d4bf684a8679a6776d6e9075.jpg)

#### window角色
* window
* dialog：可能会产生“焦点陷阱”，也就是说，当这样的角色被激活时，焦点无法离开这个区域。
* alertdialog
