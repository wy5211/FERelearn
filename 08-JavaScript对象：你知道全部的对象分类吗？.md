### JavaScript对象
#### JavaScript中的对象分类
我们可以把对象分为以下几类：
* 宿主对象（hosts Objects）：由JavaScript宿主环境提供的对象，它们的行为完全由宿主环境决定。
* 内置对象（built-in Objects）：由
JavaScript语言提供的对象
  * 固有对象（Intrinsic Objects）：由标准规定，随着JavaScript运行时创建而自动创建的对象实例
  * 原生对象（Native Objects）：可以由用户通过Array、RegExp等内置构造器或者特殊语法创建的对象
  * 普通对象（Ordinary Objects）：由{}语法、Object构造器或者class关键字定义类创建的对象，它能被原型继承。

##### 宿主对象
JavaScript宿主对象千奇百怪，最熟悉的无疑是浏览器环境中的宿主。
在浏览器环境中，全局对象是window，window上有很多属性，如document。
实际上，window上的属性一部分来自JavaScript，一部分来自浏览器环境
JavaScript标准中规定了全局对象属性，w3c的各种标准中规定了Window对象的其它属性。

##### 内置对象·固有对象
固有对象在任何JS代码执行前就已经被创建好了，它们通常扮演者雷瑟基础库的角色。如Math、JSON等

##### 内置对象·原生对象
能够通过语言本身构造器创建的对象称作原生对象。在JavaScript标准中，提供了30多个构造器。按照不同应用场景，原生对象可以分成以下几类：
![avatar](https://static001.geekbang.org/resource/image/6c/d0/6cb1df319bbc7c7f948acfdb9ffd99d0.png)
通过这些构造器，我们可以用new来创建新的对象，所以我们把这些对象称作原生对象
这些构造器创建的对象多数使用了私有字段,例如：
* Error: \[[ErrorData]]
* Boolean: \[[BooleanData]]
* Number: \[[NumberData]]
* Date: \[[DateValue]]
* RegExp: \[[RegExpMatcher]]
* Symbol: \[[SymbolData]]
* Map: \[[MapData]]

这些字段使得原型继承方法无法正常工作，所以，我们可以认为，所有这些原生对象都是为了特定能力或者性能，而设计出来的“特权对象”。

##### 用对象来模拟函数与构造器：函数对象与构造器对象
函数对象的定义是：具有[[call]]私有字段的对象，构造器对象的定义是：具有私有字段[[construct]]的对象。
[[construct]]的执行过程如下：
* 以 Object.protoype 为原型创建一个新对象；
* 以新对象为 this，执行函数的[[call]]；
* 如果[[call]]的返回值是对象，那么，返回这个对象，否则返回第一步创建的新对象。

这样的规则造成了个有趣的现象，如果我们的构造器返回了一个新的对象，那么new创建的新对象就变成了一个构造函数之外完全无法访问的对象，这一定程度上可以实现“私有”。
```
function cls(){
    this.a = 100;
    return {
        getValue:() => this.a
    }
}
var o = new cls;
o.getValue(); //100
//a在外面永远无法访问到
```

##### 特殊行为的对象
* Array：Array的length属性根据最大的下标自动发生变化。
* Object.prototype：作为所有正常对象的默认原型，不能再给它设置原型了。
* String：为了支持下标运算，String的正整数属性访问会去字符串里查找。
* Arguments：arguments的非负整数型下标属性跟对应的变量联动。
* 模块的namespace对象：特殊的地方非常多，跟一般对象完全不一样，尽量只用于import吧
* 类型数组和数组缓冲区：跟内存块相关联，下标运算比较特殊。
* bind后的function：跟原来的函数相关联。