### CSS选择器

#### 选择器的基本意义：根据特征选中元素树上的一批元素
* 简单选择器：针对某一特征判断是否选中元素。
* 复合选择器：连续写在一起的简单选择器，针对元素自身特征选择单个元素。
* 复杂选择器：由“（空格）”“ >”“ ~”“ +”“ ||”等符号连接的复合选择器，根据父元素或者前序元素检查单个元素。
* 选择器列表：由逗号分隔的复杂选择器，表示“或”的关系。

#### 简单选择器
![avatar](https://static001.geekbang.org/resource/image/4c/ce/4c9ac78870342dc802137ea9c848c0ce.png)
svg和html中都有a元素，我们若要想区分选择svg中的a和html中的a，就必须用带命名空间的类型选择器。
```
@namespace svg url(http://www.w3.org/2000/svg);
@namespace html url(http://www.w3.org/1999/xhtml);
svg|a {
  stroke:blue;
  stroke-width:1;
}

html|a {
  font-size:40px
}
```

#### id选择器与class选择器
#### 属性选择器
#### 伪类选择器
##### 树结构关系伪类选择器
* :root 伪类表示树的根元素
* :empty 伪类表示没有子节点的元素，这里有个例外就是子节点为空白文本节点的情况。
* :nth-child 和 :nth-last-child 这是两个函数型的伪类，CSS的An+B语法设计的是比较复杂的，我们这里仅仅介绍基本用法。
![avatar](https://static001.geekbang.org/resource/image/1e/a9/1ebdba2978a22c13844d108318b271a9.png)
* :nth-last-child的区别仅仅是从后往前数。
* :first-child :last-child 分别表示第一个和最后一个元素。
* :only-child 按字面意思理解即可，选中唯一一个子元素。

of-type系列，是一个变形的语法糖，S:nth-of-type(An+B)是:nth-child(|An+B| of S)的另一种写法。

##### 链接与行为伪类选择器
* :any-link 表示任意的链接，包括a、area和link标签都可能匹配到这个伪类。
* :link 表示未访问过的链接， 
* :visited 表示已经访问过的链接。
* :hover 表示鼠标悬停在上的元素，
* :active 表示用户正在激活这个元素，如用户按下按钮，鼠标还未抬起时，这个按钮就处于激活状态
* :focus 表示焦点落在这个元素之上。
* :target 用于选中浏览器URL的hash部分所指示的元素。

##### 逻辑伪类选择器
伪类是个函数型伪类，它的作用时选中内部的简单选择器命中的元素。
```
*|*:not(:hover)
```

##### 其它伪类选择器
