### JavaScript对象
#### 什么是原型？
“基于类”的编程提倡使用一个关注分类和类之间关系开发模型。在这类语言中，总是先有类，再从类去实例化一个对象。类与类之间又可能会形成继承、组合等关系。类又往往与语言的类型系统整合，形成一定编译时的能力。
与此相对，“基于原型”的编程看起来更为提倡程序员去关注一系列对象实例的行为，而后才去关心如何将这些对象，划分到最近的使用方式相似的原型对象，而不是将它们分成类。
在JavaScript之前，原型系统就更多与高动态性语言配合，并且多数基于原型的语言提倡运行时的原型修改
原型系统的“复制操作”有两种实现思路：
* 一个是并不真的去复制一个原型对象，而是使得新对象持有一个原型的引用；
* 另一个是切实地复制对象，从此两个对象再无关联。

显然JavaScript属于后者

#### JavaScript的原型
* 如果所有对象都有私有字段\[[prototype]]，就是对象的原型；
* 读一个属性，如果对象本身没有，则会继续访问对象的原型，直到原型为空或者找到为止。

从 ES6 以来，JavaScript提供了一系列内置函数，以便更为直接地访问操纵原型。三个方法分别为：
* Object.create 根据指定的原型创建新对象，原型可以是null；
* Object.getPrototypeOf 获得一个对象的原型；
* Object.setPrototypeOf 设置一个对象的原型。

利用这三个方法，我们可以完全抛开类的思维，利用原型来实现抽象和复用
```
const cat = {
    say(){
        console.log("meow~");
    },
    jump(){
        console.log("jump");
    }
}

const tiger = Object.create(cat,  {
    say:{
        writable:true,
        configurable:true,
        enumerable:true,
        value:function(){
            console.log("roar!");
        }
    }
})


const anotherCat = Object.create(cat);

anotherCat.say();

const anotherTiger = Object.create(tiger);

anotherTiger.say();
```

##### 早期版本中的类与原型
在早期版本的JavaScript中，“类”的定义是一个私有属性 \[[class]]，语言标准为内置类型诸如Number、String、Date等指定了\[[class]]属性，以表示它们的类。语言使用者唯一可以访问\[[class]]属性的方式是Object.prototype.toString。
```
var o = new Object;
var n = new Number;
var s = new String;
var b = new Boolean;
var d = new Date;
var arg = function(){ return arguments }();
var r = new RegExp;
var f = new Function;
var arr = new Array;
var e = new Error;
console.log([o, n, s, b, d, arg, r, f, arr, e].map(v => Object.prototype.toString.call(v))); 
// "[object Object]", "[object Number]", "[object String]", "[object Boolean]", "[object Date]", "[object Arguments]", "[object RegExp]", "[object Function]", "[object Array]", "[object Error]"
```

在ES5开始，\[[class]] 私有属性被 Symbol.toStringTag 代替，Object.prototype.toString 的意义从命名上不再跟 class 相关。我们甚至可以自定义 Object.prototype.toString 的行为，以下代码展示了使用Symbol.toStringTag来自定义 Object.prototype.toString 的行为：
```
const o = { [Symbol.toStringTag]: "MyObject" }
console.log(o + ""); // [object MyObject]
```

我们仍然要把new理解成JavaScript面向对象的一部分，下面我就来讲一下new操作具体做了哪些事情。
new 运算接受一个构造器和一组调用参数，实际上做了几件事：
* 以构造器的 prototype 属性（注意与私有字段\[[prototype]]的区分）为原型，创建新对象；
* 将 this 和调用参数传给构造器，执行；
* 如果构造器返回的是对象，则返回，否则返回第一步创建的对象。

下面时用构造器模拟类的两种方法：
```
function c1(){
    this.p1 = 1;
    this.p2 = function(){
        console.log(this.p1);
    }
} 
var o1 = new c1;
o1.p2();

function c2(){
}
c2.prototype.p1 = 1;
c2.prototype.p2 = function(){
    console.log(this.p1);
}

var o2 = new c2;
o2.p2();
```
第一种方法是直接在构造器中修改this，给this添加属性。
第二种方法是修改构造器的prototype属性指向的对象，它是从这个构造器构造出来的所有对象的原型。

#### ES6中的类
ES6中引入了class关键字，并且在标准中删除了所有\[[class]]相关的私有属性描述，类的概念正式从属性升级成语言的基础设施，从此，基于类的编程方式成为了JavaScript的官方编程范式。

```
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
  // Getter
  get area() {
    return this.calcArea();
  }
  // Method
  calcArea() {
    return this.height * this.width;
  }
}
```
最重要的是，类提供了继承能力。我们来看一下下面的代码。
```
class Animal { 
  constructor(name) {
    this.name = name;
  }
  
  speak() {
    console.log(this.name + ' makes a noise.');
  }
}

class Dog extends Animal {
  constructor(name) {
    super(name); // call the super class constructor and pass in the name parameter
  }

  speak() {
    console.log(this.name + ' barks.');
  }
}

let d = new Dog('Mitzie');
d.speak(); // Mitzie barks.
```

比起早期的原型模拟方式，使用extends关键字自动设置了constructor，并且会自动调用父类的构造函数，这是一种更少坑的设计。

所以当我们使用类的思想来设计代码时，应该尽量使用class来声明类，而不是用旧语法，拿函数来模拟对象。