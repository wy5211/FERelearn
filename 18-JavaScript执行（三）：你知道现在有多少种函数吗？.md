### JavaScript执行（三）

#### 函数
八种函数：

#### 1、普通函数
```
function foo() {
  // todo
}
```

#### 2、箭头函数
```
const foo = () => {
  // todo
}
```

#### 3、方法：在class中定义的函数
```
  class C {
    foo() {
      // todo
    }
  }
```

#### 4、生成器函数
```
  function foo*() {
    foo() {
      // todo
    }
  }
```

#### 5、类：用class定义的类，实际上也是函数
```
  class Foo {
    constructor() {
      // todo
    }
  }
```

#### 6/7/8、异步函数：普通函数、箭头函数和生成器函数加上async
```
  async function foo() {
    // todo
  }

  const foo = async () => {
    // todo
  }

  async function foo*() {
    // todo
  }
```

#### this关键字行为
**this是执行上下文很重要的一个组成部分。同一个函数调用方式不同，得到的this值也不同**，例子如下：
```
function showThis(){
    console.log(this);
}

var o = {
    showThis: showThis
}

showThis(); // window
o.showThis(); // o
```
**调用函数时使用的引用，决定了函数执行时的this值。**

```
const showThis = () => {
    console.log(this);
}

var o = {
    showThis: showThis
}

showThis(); // window
o.showThis(); // window
```
**箭头函数：不论用什么引用来调用，都不影响this值**

```
class C {
    showThis() {
        console.log(this);
    }
}
var o = new C();
var showThis = o.showThis;

showThis(); // undefined
o.showThis(); // o
```
**方法：我们看到this的行为也不太一样，它得到了undefined的结果**

**结论：生成器函数、异步生成器函数和异步普通函数跟普通函数行为是一致的，异步箭头函数与箭头函数行为是一致的。**

#### this关键字的机制
在JavaScript标准中，为函数规定了用来保存定义时上下文的私有属性[[Environment]]。

当一个函数执行时，会创建一条新的执行环境记录，记录的外层词法环境（outer lexical environment）会被设置成函数的[[Environment]]。
如下：
```
var a = 1;
foo();

在另一个文件定义了foo：

var b = 2;
function foo(){
    console.log(b); // 2
    console.log(a); // error： a is not defined
}
```
Js用一个栈来管理上下文，栈的每一项又包含一个链表：
![avatar](https://static001.geekbang.org/resource/image/e8/31/e8d8e96c983a832eb646d6c17ff3df31.jpg)
当函数调用时，会入栈一个新的执行上下文，函数调用结束时，执行上下文被出栈。
而this的机制更复杂，Js定义了[[thisMode]]私有属性
[[thisMode]]私有属性
* lexical：表示从上下文中找this，对应箭头函数
* golbal：表示当this为undefined时，取全局对象，对应普通函数
* strict：当严格模式时使用，this严格按照调用时传入的值，可能为null或者undefined

class设计成了默认按strict模式执行，所以可以看到方法的行为跟普通函数有差异，对普通函数用strict可以达成与方法例子一样的效果
```
"use strict"
function showThis(){
    console.log(this);
}

var o = {
    showThis: showThis
}

showThis(); // undefined
o.showThis(); // o
```

函数创建新的执行上下文中的词法环境记录时，会根据[[thisMode]]来标记新纪录的[[ThisBindingStatus]]私有属性。

代码执行遇到this时，会逐层检查当前词法环境记录中的[[ThisBindingStatus]]，当找到有this的环境记录时获取this的值。

这样的规则的实际效果是，嵌套的箭头函数中的代码都指向外层this，例如：

```
var o = {}
o.foo = function foo(){
    console.log(this);
    return () => {
        console.log(this);
        return () => console.log(this);
    }
}

o.foo()()(); // o, o, o
```

#### 操作this的内置函数
* call
* apply
* bind

call和apply区别在于传参方式，bind生成一个绑定过的函数，并且均可用于不接受this的函数类型如箭头、class，无法实现改变this的能力，但可以实现传参。

#### new与this
new的执行过程
* 以构造器的prototype为原型，创建新对象
* 将this和调用参数传给构造器，执行
* 如果构造器返回的是对象，则返回，否则返回第一步创建的对象

以下为八种函数与new搭配的效果
![avatar](https://static001.geekbang.org/resource/image/6a/da/6a9f0525b713a903c6c94f52afaea3da.png)