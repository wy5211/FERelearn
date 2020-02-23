### JavaScript类型
JavaScript模块会从运行时、文法和执行过程三个角度去剖析JS的知识体系，本篇我们就从运行时的角度去看JavaScript的类型系统。
> 运行时类型是代码实际执行过程中我们用到的类型。所有的类型数据都会属于7个类型之一。从变量、参数、返回值到表达式中间结果，任何JavaScript代码运行过程中产生的数据，都具有运行时类型

#### 类型
7中语言类型：
* Number
* String
* Boolean
* Undefined
* Null
* Object
* Symbol

##### Undefined，Null
Undefined表示未定义，它的类型只有一个值undefined，任何变量在赋值前是Undefined类型，undefined值。一般我们可以用全局变量undefined来表达这个值，或者void运算来把任何一个表达式变成undefined值。
但是undefined是一个变量（不可修改），并非关键字，所以为了避免修改，建议使用void 0来获取undefined值。
null表示定义了但是为空，Null类型只有一个值就是null，null是关键字。

##### Boolean
Boolean有两个值：分别为true和false，表示逻辑真和逻辑假，同时又true和false两个关键字来表示两个值

##### String
String表示文本数据，有最大长度2^53 - 1，这个最大长度，并非是理解中的字符数。
String的意思并非字符串，而是字符串的UTF16编码，字符串的操作charAt,charCodeAt,length等都是针对UTF16标码。所以最大长度实际上是受字符串的编码长度影响。
> Note：现行的字符集国际标准，字符是以 Unicode 的方式表示的，每一个 Unicode 的码点表示一个字符，理论上，Unicode 的范围是无限的。UTF是Unicode的编码方式，规定了码点在计算机中的表示方法，常见的有 UTF16 和 UTF8。 Unicode 的码点通常用 U+??? 来表示，其中 ??? 是十六进制的码点值。 0-65536（U+0000 - U+FFFF）的码点被称为基本字符区域（BMP）。

JavaScript 中的字符串是永远无法变更的，一旦字符串构造出来，无法用任何方式改变字符串的内容，所以字符串具有值类型的特征。
```
let a = 'java';
a = a + 'script';
实际上字符串'java'开辟了内存空间存储，'javascript'又开辟了新的空间存储，再把a指向'javascript'，所以'java'并没有改变
```

##### Number
Number类型有 18437736874454810627(即2^64-2^53+3) 个值。
JavaScript 中的 Number 类型基本符合 IEEE 754-2008 规定的双精度浮点数规则，但是JavaScript为了表达几个额外的语言场景（比如不让除以0出错，而引入了无穷大的概念），规定了几个例外情况：
* NaN，占用了 9007199254740990，这原本是符合IEEE规则的数字；
* infinity，无穷大
* -infinity，负无穷大

JavaScript中有 +0 和 -0，在加法类运算中它们没有区别，但是除法的场合则需要特别留意区分，“忘记检测除以-0，而得到负无穷大”的情况经常会导致错误，而区分 +0 和 -0 的方式，正是检测 1/x 是 Infinity 还是 -Infinity。

同样根据浮点数的定义，非整数的Number类型无法用 ==（===也不行） 来比较，一段著名的代码，为什么在JavaScript中，0.1+0.2不能=0.3：
```
0.1 + 0.2 == 0.3 // false
```
浮点数运算的精度问题导致等式左右的结果并不是严格相等，而是相差了个微小的值。所以实际上，这里错误的不是结论，而是比较的方法，正确的比较方法是使用JavaScript提供的最小精度值：
```
Math.abs(0.1 + 0.2 - 0.3) <= Number.EPSILON // true
```

##### Symbol
在ES6中，整个对象系统被用Symbol重塑
我们创建 Symbol 的方式是使用全局的 Symbol 函数
```
 var mySymbol = Symbol("my symbol");
 注意，并不需要new
```
我们可以使用 Symbol.iterator 来自定义 for…of 在对象上的行为：
```
const o = {}
o[Symbol.iterator] = function () {
  let index = 0
  return {
    next: function () {
      return {
        value: index ++,
        done: index > 10
      }
    }
  }
}
for (let v of o) {
  console.log(v)
}
// 0 1 2 3 4 5 6 7 8 9
```

##### Object
Object是最复杂的类型，也是JS核心机制之一
Number、String和Boolean，三个构造器是两用的，当跟 new 搭配时，它们产生对象，当直接调用时，它们表示强制类型转换。

Symbol 函数比较特殊，直接用 new 调用它会抛出错误，但它仍然是 Symbol 对象的构造器。

JavaScript 语言设计上试图模糊对象和基本类型之间的关系，我们日常代码可以把对象的方法在基本类型上使用，比如：
```
'abc'.charAt(0) // a
```
甚至我们在原型上添加方法，都可以应用于基本类型，比如以下代码，在 Symbol 原型上添加了hello方法，在任何 Symbol 类型变量都可以调用。
```
Symbol.prototype.hello = () => console.log("hello");

const a = Symbol("a");
console.log(typeof a); //symbol，a并非对象
a.hello(); //hello，有效
```
##### 注意
事实上，“类型”在 JavaScript 中是一个有争议的概念。一方面，标准中规定了运行时数据类型； 另一方面，JS语言中提供了 typeof 这样的运算，用来返回操作数的类型，但 typeof 的运算结果，与运行时类型的规定有很多不一致的地方。我们可以看下表来对照一下。
![avatar](https://static001.geekbang.org/resource/image/ec/6b/ec4299a73fb84c732efcd360fed6e16b.png)

##### 类型转换
因为JS是弱类型，所以类型转换非常频繁。
实际上大部分类型转换规则是非常简单的，如下表所示：
![avatar](https://static001.geekbang.org/resource/image/71/20/71bafbd2404dc3ffa5ccf5d0ba077720.jpg)

##### StringToNumber
字符串到数字的类型转换，存在一个语法结构，类型转换支持十进制、二进制、八进制和十六进制
* 30；十进制
* 0b111；二进制
* 0o13；八进制
* 0xFF。十六进制

此外JavaScript支持的字符串语法还包括正负号科学计数法，可以使用大写或者小写的e来表示：
* 1e3；
* -1e-2。

需要注意的是，parseInt 和 parseFloat 并不使用这个转换
在不传入第二个参数的情况下，parseInt只支持16进制前缀“0x”，而且会忽略非数字字符，也不支持科学计数法。
多数情况下，Number 是比 parseInt 和 parseFloat 更好的选择。

##### NumberToString
在较小的范围内，数字到字符串的转换是完全符合你直觉的十进制表示。当Number绝对值较大或者较小时，字符串表示则是使用科学计数法表示的。

##### 装箱转换
每一种基本类型Number、String、Boolean、Symbol在对象中都有对应的类，所谓装箱转换，正是把基本类型转换为对应的对象，它是类型转换中一种相当重要的种类。
```
const symbolObj = (function () {return this}).call(Symbol('a'))
typeof symbolObj //Object
symbolObj instaceof Symbol //true
symbolObj.constructor == Symbol //true
```
装箱机制会频繁产生临时对象，在一些对性能要求较高的场景下，我们应该尽量避免对基本类型做装箱转换。
使用内置的 Object 函数，我们可以在JavaScript代码中显式调用装箱能力。
```
const symbolObj = Object(Symbol('a'))
typeof symbolObj //Object
symbolObj instaceof Symbol //true
symbolObj.constructor == Symbol //true
```
每一类装箱对象皆有私有的 Class 属性，这些属性可以用 Object.prototype.toString 获取：
```
const symbolObject = Object(Symbol("a"));
console.log(Object.prototype.toString.call(symbolObject)); //[object Symbol]
```
在 JavaScript 中，没有任何方法可以更改私有的 Class 属性，因此Object.prototype.toString 是可以准确识别对象对应的基本类型的方法，它比 instanceof 更加准确。
但需要注意的是，call本身会产生装箱操作，所以需要配合 typeof 来区分基本类型还是对象类型。

##### 拆箱转换
在JavaScript标准中，规定了 ToPrimitive 函数，它是对象类型到基本类型的转换（即，拆箱转换）。
对象到 String 和 Number 的转换都遵循“先拆箱再转换”的规则。通过拆箱转换，把对象变成基本类型，再从基本类型转换为对应的 String 或者 Number。
拆箱转换会尝试调用 valueOf 和 toString 来获得拆箱后的基本类型。如果 valueOf 和 toString 都不存在，或者没有返回基本类型，则会产生类型错误 TypeError。
在 ES6 之后，还允许对象通过显式指定 @@toPrimitive Symbol 来覆盖原有的行为。
```
const o = {
    valueOf : () => {console.log("valueOf"); return {}},
    toString : () => {console.log("toString"); return {}}
}

o[Symbol.toPrimitive] = () => {console.log("toPrimitive"); return "hello"}

console.log(o + "")
// toPrimitive
// hello
```

