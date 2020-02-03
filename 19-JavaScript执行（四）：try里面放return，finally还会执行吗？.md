### JavaScript执行（四）
JavaScript语句执行机制涉及的一种基础类型：Completion类型

#### Completion类型
```
function foo(){
  try{
    return 0;
  } catch(err) {

  } finally {
    console.log("a")
  }
}

console.log(foo());
```
可以看到finally和return语句都执行了，foo()结果返回0。虽然return执行了，但是没有立刻返回，又执行了finally里面的内容
如果在finally也return一个结果，在一个函数中执行了两次return，而且是返回finally里的结果
这一的基础正是Js语句执行的完成状态，我们用一个标准类型来表示：Completion Record。
Completion Record 表示一个语句执行完之后的结果，它有三个字段：
* [[type]] 表示完成的类型，有break continue return throw和normal几种类型；
* [[value]] 表示语句的返回值，如果语句没有，则是empty；
* [[target]] 表示语句的目标，通常是一个JavaScript标签（标签在后文会有介绍）。

Javascript语句分类：
![avatar](https://static001.geekbang.org/resource/image/98/d5/98ce53be306344c018cddd6c083392d5.jpg)

#### 普通语句
* 声明类语句
  * var声明
  * const声明
  * let声明
  * 函数声明
  * 类声明
* 表达式语句
* 空语句
* debugger语句

普通语句执行后，会得到[[type]]为normal的Completion Record，Js引擎遇到这个Completion Record会继续执行下一条语句。

只有表达式会产生[[value]]，从引擎控制的角度，这个value并没有用处。如：
![avatar](https://static001.geekbang.org/resource/image/a3/67/a35801b1b82654d17e413e51b340d767.png)

#### 语句块
语句块是用大括号括起来的一组语句，是一种语句的复合结构，可以嵌套
语句块本身并不复杂，我们需要注意的是语句块内部的语句的Completion Record的[[type]] 如果不为 normal，会打断语句块后续的语句执行。

#### 控制型语句
控制类语句分成两部分，一类是对其内部造成影响，如if、switch、while/for、try，另一类是对外部造成影响如break、continue、return、throw。
一般来说， for/while - break/continue 和 try - throw 这样比较符合逻辑的组合，是大家比较熟悉的，但是，实际上，我们需要控制语句跟break 、continue 、return 、throw四种类型与控制语句两两组合产生的效果。
![avatar](https://static001.geekbang.org/resource/image/77/d3/7760027d7ee09bdc8ec140efa9caf1d3.png)

#### 带标签的语句
大部分时候，这个语句类似于注释，唯一有作用是与完成记录类型中的target相匹配，用于跳出多层循环。
```
outer: while(true) {
  inner: while(true) {
    break outer;
  }
}
console.log('finished')
```








