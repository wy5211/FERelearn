### CSS动画与交互

##### 基本语法
SGML还规定了一些特殊的节点类型，在我们之前的DOM课程中已经讲过几种节点类型，它们都有与之对应的HTML语法
![avatar](https://static001.geekbang.org/resource/image/b6/bc/b6fdf08dbe47c837e274ff1bb6f630bc.jpg)
**标签语法**
* 开始标签：<tagname>
* 结束标签：</tagname>
* 自闭合标签：<tagname />

**文本语法**
在HTML中，规定了两种文本语法，一种是普通的文本节点，另一种是CDATA文本节点。

**注释语法**
HTML注释语法以\<!--开头，以-->结尾，注释的内容非常自由，除了-->都没有问题。

**DTD语法（文档类型定义）**
SGML的DTD语法十分复杂，但是对HTML来说，其实DTD的选项是有限的，浏览器在解析DTD时，把它当做几种字符串之一
HTML4.01有三种DTD。分别是严格模式、过渡模式和frameset模式。
```
严格模式
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">

过度模式
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">

frameset模式
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" "http://www.w3.org/TR/html4/frameset.dtd">
```

HTML4.01又规定了XHTML语法，同样有三个版本
```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" 
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "
http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN" 
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">
```
HTML5
```
<!DOCTYPE html>
```

文本实体：每一个文本实体由&开头，由;结束，这属于基本语法的规定，文本实体可以用#后跟一个十进制数字，表示字符Unicode值。除此之外这两个符号之间的内容，则由DTD决定。
```
&lt;
&nbsp;
&gt;
&amp;
```