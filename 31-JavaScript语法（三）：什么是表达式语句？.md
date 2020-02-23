### JavaScript语法（三）

#### 什么是表达式语句
表达式语句实际上就是一个表达式，它是由运算符连接变量或者直接量构成的，直接量就是直接用某种语法写出来的具有特定类型的值。比如数字123，字符串Hello world。

##### PrimaryExpression 主要表达式
表达式的最小单位，它所涉及的语法结构也是优先级最高的。
* 定义基本类型
```
"abc";
123;
null;
true;
false;
```

* 定义对象类型
```
({});
(function(){});
(class{ });
[];
/abc/g;
```

##### MemberExpression 成员表达式
Member Expression通常是用于访问对象成员的
```
a.b
a['b']
new.target
super.b
```
Member Expression最初设计是为了属性访问的，不过从语法结构需要，以下两种在JavaScript标准中当做Member Expression：
* 带函数的模板：这个带函数名的模板表示把模板的各个部分算好后传递给一个函数。
```
f`a${b}c`;
```
* 带参数列表的new运算，注意，不带参数列表的new运算优先级更低，不属于Member Expression。
```
new Cls();
```

##### NewExpression NEW表达式
Member Expression加上new就是New Expression（当然，不加new也可以构成New Expression，JavaScript中默认独立的高优先级表达式都可以构成低优先级表达式）
```
new new Cls(1)
实际意思：new (new CLs(1))
```

##### CallExpression 函数调用表达式
Member Expression还能构成Call Expression。它的基本形式是Member Expression后加一个括号里的参数列表，或者我们可以用上super关键字代替Member Expression。
```
a.b(c);
super();
一些变体
a.b(c)(d)(e);
a.b(c)[3];
a.b(c).d;
a.b(c)`xyz`;
```

##### LeftHandSideExpression 左值表达式
New Expression 和 Call Expression 统称LeftHandSideExpression，左值表达式。左值表达式就是可以放到等号左边的表达式。

##### AssignmentExpression 赋值表达式
AssignmentExpression 赋值表达式也有多种形态，最基本的当然是使用等号赋值：
```
a = b
等号嵌套
a = b = c = d
等价于
a = (b = (c = d))
```
赋值表达式的使用，还可以结合一些运算符
```
a += b
```
包括*=、/=、%=、+=、-=、<<=、>>=、>>>=、&=、^=、|=、**=

##### Expression 表达式
赋值表达式可以构成Expression表达式的一部分。在JavaScript中，表达式就是用逗号运算符连接的赋值表达式。在JavaScript中，比赋值运算优先级更低的就是逗号运算符了。我们可以把逗号可以理解为一种小型的分号。