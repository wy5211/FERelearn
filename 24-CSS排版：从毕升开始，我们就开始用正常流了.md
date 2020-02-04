### CSS 排版

#### 正常流的行为

正常流的排版行为，那就是：依次排列，排不下了换行。
vertical-align：只针对于行内元素
![avatar](https://static001.geekbang.org/resource/image/aa/e3/aa6611b00f71f606493f165294410ee3.png)

#### 正常流的原理

在 CSS 标准中，规定了如何排布每一个文字或者盒的算法，这个算法依赖一个排版的“当前状态”，CSS 把这个当前状态称为“格式化上下文（formatting context）”。

```
格式化上下文 + 盒/文字 = 位置
formatting context + boxes/charater = positions
```

块级格式化上下文顺次排列元素：
![avatar](https://static001.geekbang.org/resource/image/a5/e7/a5e1b9a77d9745499f96d25cf0a0dbe7.png)
行内级格式化上下文顺次排列元素：
![avatar](https://static001.geekbang.org/resource/image/1c/cf/1ced4fa809b30343df45e559cf0c08cf.png)

当我们要把正常流中的一个盒或者文字排版，需要分成三种情况处理。

- **当遇到块级盒**：排入块级格式化上下文。
- **当遇到行内级盒或者文字**：首先尝试排入行内级格式化上下文，如果排不下，那么创建一个行盒，先将行盒排版（行盒是块级，所以到第一种情况），行盒会创建一个行内级格式化上下文。
- **遇到 float 盒**：把盒的顶部跟当前行内级上下文上边缘对齐，然后根据 float 的方向把盒的对应边缘对到块级格式化上下文的边缘，之后重排当前行盒。

以上讲的都是一个块级格式化上下文中的排版规则，实际上，页面中的布局没有那么简单，一些元素会在其内部创建新的块级格式化上下文，这些元素有：

1. 浮动元素
2. 绝对定位元素；
3. 非块级但仍能包含块级元素的容器（如 inline-blocks, table-cells, table-captions）；
4. 块级的能包含块级元素的容器，且属性 overflow 不为 visible。

#### 正常流的使用技巧

##### 等分布局问题

```
<div class="outer">
    <div class="inner"></div>
    <div class="inner"></div>
    <div class="inner"></div>
</div>
.inner {
    width:33.33%;
    height:300px;
    display:inline-block;
    outline:solid 1px blue;
}
```

这段代码执行之后，效果跟我们预期不同，我们可以发现，每个 div 并非紧挨，中间有空白，这是因为我们为了代码格式加入的换行和空格被 HTML 当作空格文本，跟 inline 盒混排了的缘故。
解决方案是修改 HTML 代码，去掉空格和换行：

```
<div class="outer"><div class="inner"></div><div class="inner"></div><div class="inner"></div></div>
```

但是这样做影响了源代码的可读性，一个变通的方案是，改变 outer 中的字号为 0。

```
.inner {
    width:33.33%;
    height:300px;
    display:inline-block;
    outline:solid 1px blue;
    font-size:30px;
}
.outer {
    font-size:0;
}
```

##### 自适应宽

```
<div class="outer">
  <div class="fixed"></div>
  <div class="auto"></div>
</div>

.fixed {
  height: 300px;
  width: 100px;
  float: left;
  background-color: skyblue
}
.auto {
  height: 300px;
  margin-left: 100px;
  background-color: lightblue
}
```
