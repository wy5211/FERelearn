### CSS语法
CSS 的顶层样式表由两种规则组成的规则列表构成，一种被称为 at-rule，也就是 at 规则，另一种是 qualified rule，也就是普通规则。
#### at规则
* @charset
* @import 
* @media 
* @page
* @counter-style
* @keyframes
* @fontface
* @supports
* @namespace 

#### 普通规则
qualified rule 主要是由选择器和声明区块构成。声明区块又由属性和值构成。
* 普通规则
  * 选择器
  * 声明列表
    * 属性
    * 值
      * 值的类型
      * 函数

##### 选择器
对每一个选择器来说，如果它不是伪元素的话，由几个可选的部分组成，标签类型选择器，id、class、属性和伪类，它们中只要出现一个，就构成了选择器。
![avatar](https://static001.geekbang.org/resource/image/d5/00/d56974c0265982b9ac84b067cd623e00.png)

##### 声明：属性和值
值的部分，主要在标准 CSS Values and Unit，根据每个 CSS 属性可以取到不同的值，这里的值可能是字符串、标识符。
CSS 属性值可能是以下类型。
* CSS 范围的关键字：initial，unset，inherit，任何属性都可以的关键字。
* 字符串：比如 content 属性。
* URL：使用 url() 函数的 URL 值。
* 整数 / 实数：比如 flex 属性。
* 维度：单位的整数 / 实数，比如 width 属性。
* 百分比：大部分维度都支持。
* 颜色：比如 background-color 属性。
* 图片：比如 background-image 属性。
* 2D 位置：比如 background-position 属性。
* 函数：来自函数的值，比如 transform 属性。

CSS 支持一批特定的计算型函数：
* calc()
* max()
* min()
* clamp()
* toggle()
* attr()