### JavaScript词法

文法是编译原理中对语言的写法的一种规定，一般来说，文法分成词法和语法两种。

词法规定了语言的最小语义单元：token，可以翻译成“标记”或者“词”

##### 概述
JavaScript源代码中的输入可以这样分类：
* WhiteSpace 空白字符
* LineTerminator 换行符
* Comment 注释
* Token 词
  * IdentifierName 标识符名称，典型案例是我们使用的变量名，注意这里关键字也包含在内了。
  * Punctuator 符号，我们使用的运算符和大括号等符号。
  * NumericLiteral 数字直接量，就是我们写的数字。
  * StringLiteral 字符串直接量，就是我们用单引号或者双引号引起来的直接量。
  * Template 字符串模板，用反引号` 括起来的直接量。

##### 空白符号 Whitespace
![avatar](https://static001.geekbang.org/resource/image/dd/60/dd26aa9599b61d26e7de807dee2c6360.png)
##### 换行符 LineTerminator
##### 注释 Comment
##### 标识符名称 IdentifierName
##### 符号 Punctuator
##### 数字直接量 NumericLiteral
十进制的Number可以带小数，小数点前后部分都可以省略，但是不能同时省略，我们看几个例子：
```
.01
12.
12.01

12.toString() // error
12 .toString() // 需要增加空格
```
##### 字符串直接量 StringLiteral
##### 正则表达式直接量 RegularExpressionLiteral
##### 字符串模板 Template