### JavaScript语法（四）
在一些通用的计算机语言设计理论中，能够出现在赋值表达式右边的叫做：右值表达式（RightHandSideExpression），而在JavaScript标准中，规定了在等号右边表达式叫做条件表达式（ConditionalExpression）

##### 更新表达式 UpdateExpression
左值表达式搭配 ++ -- 运算符，可以形成更新表达式。
```
-- a;
++ a;
a --
a ++
```
在ES2018中，跟早期版本有所不同，前后自增自减运算被放到了同一优先级。

##### 一元运算表达式 UnaryExpression
更新表达式搭配一元运算符，可以形成一元运算表达式
```
delete a.b;
void a;
typeof a;
- a;
~ a;
! a;
await a;
```

##### 乘方表达式 ExponentiationExpression
乘方表达式也是由更新表达式构成的。它使用**号。）
```
++i ** 30
2 ** 30 //正确
-2 ** 30 //报错
**运算是右结合的
```

##### 乘法表达式 MultiplicativeExpression
```
*
/
%
```

##### 加法表达式 AdditiveExpression
```
+ 
-
```

##### 移位表达式 ShiftExpression
移位表达式由加法表达式构成，移位是一种位运算，分成三种：
```
<< 向左移位
>> 向右移位
>>> 无符号向右移位
-1 >>> 1 // 2 ** 31
```

##### 关系表达式 RelationalExpression
```
<=
>=
<
>
instanceof 
in
```

##### 相等表达式 EqualityExpression
```
==
!=
===
!==
```
==十分复杂，但是归根结底，类型不同的变量比较时只有三条规则：
* undefined与null相等；
* 字符串和bool都转为数字再比较；
* 对象转换成primitive类型再比较。

##### 位运算表达式
* &按位与表达式
* ^按位异或表达式
* |按位或表达式
* ~按位取反表达式
异或运算有个特征，那就是两次异或运算相当于取消。所以有一个异或运算的小技巧，就是用异或运算来交换两个整数的值。
```
let a = 102, b = 324;

a = a ^ b;
b = a ^ b;
a = a ^ b;

console.log(a, b);
```

##### 逻辑与表达式和逻辑或表达式
逻辑与表达式由按位或表达式经过逻辑与运算符连接构成，逻辑或表达式则由逻辑与表达式经逻辑或运算符连接构成。
```
false || 1; // 1
false && undefined; // false

逻辑表达式具有短路的特性
true || foo()
这里foo不会被执行
```

##### 条件表达式 ConditionalExpression
条件表达式由逻辑或表达式和条件运算符构成，条件运算符又称三目运算符，它有三个部分，由两个运算符?和:配合使用。
```
condition? branch1: branch2
```
