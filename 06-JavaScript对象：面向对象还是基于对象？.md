### JavaScript面向对象
* 为什么JavaScript（直到ES6）有对象的概念，但是却没有类的概念
* 为什么JavaScript对象里可以自由添加属性

JavaScript标准对基于对象的定义，这个定义的具体内容是：语言和宿主的基础设施是由对象来提供的，并且JavaScript程序即是一系列互相通讯的对象集合。

这里的意思不是表达弱化面向对象的意思，反而是表达对象对于语言的重要性。

#### 什么是面向对象
在《面向对象分析与设计》这本书中，Grady Booch替我们做了总结，他认为，从人类的认知角度来说，对象应该是下列事物之一：
1. 一个可以触摸或者看见的东西
2. 人的智力可以理解的东西
3. 可以指导思考或行动的东西

#### JavaScript 对象的特征
不论任何语言，对象有如下几个特点：
* 对象具有唯一标识性：即使完全相同的对象，也并非同一个对象
* 对象具有状态：同一个对象可能处于不同状态之下
* 对象具有行为：对象的状态可能因为行为而改变

标识性的意思是，对象是用内存地址来体现的。
状态和行为，C++中称为”成员变量“和”成员函数“，Java中称为”属性“和”方法“，JavaScript中统一称为”属性“。

**在实现对象基本特征的基础上，JavaScript具有高度动态性，这是因为JavaScript赋予了使用者可以在运行时为对象添改状态和行为的能力**

##### JavaScript对象的两类属性
对JavaScript而言，属性并非简单的key-value，JavaScript用一组特征来描述属性。

第一类数据属性：
* value: 值
* writable: 可写
* enumerable: for in是否可以枚举
* configurable：属性能否被删除或修改特征值

大多数情况下，只需关心值便可

第二类访问器属性（getter/setter）：
* getter: 函数或undefined，在取值时被调用
* setter：函数或undefined，在赋值时被调用
* enumerable：for in是否可以枚举
* configurable：属性是否被修改或改变特征值

访问器属性使得属性在读写时得到完全不同的值，它可以视为一种函数的语法糖。

我们可以使用Object.getOwnPropertyDescripter查看

在创建对象时，可以使用get和set关键字来创建访问器属性：
```
const o = {
  get a() {
    return 1
  }
}
o.a // 1
```

实际上，JavaScript的对象运行时时一个”属性的集合“，属性以字符串或Symbol为key，以数据属性特征值或者访问器特征值为value。
对象时一个属性的索引结构。
另外以Symbol为属性名，是JavaScript对象的一个特色。
JavaScript的对象设计与主流对象设计语言差异非常大，但是提供了完全运行时的对象系统，这使得它可以模仿多数面向对象编程范式，所以它也是面向对象的编程语言。
JavaScript语言标准也已经明确说明，JavaScript是一门面向对象的语言，我想标准中能这样说，正是因为JavaScript的高度动态性的对象系统。