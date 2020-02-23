### JavaScript语法（一）

##### 脚本和模块
JavaScript有两种源文件，一种叫做脚本，一种叫做模块。这个区分是在ES6引入了模块机制开始的，在ES5和之前的版本中，就只有一种源文件类型（就只有脚本）。
脚本是可以由浏览器或者node环境引入执行的，而模块只能由JavaScript代码用import引入执行。
我们对标准中的语法产生式做一些对比，不难发现，实际上模块和脚本之间的区别仅仅在于是否包含import 和 export。
现代浏览器可以支持用script标签引入模块或者脚本，如果要引入模块，必须给script标签添加type=“module”。如果引入脚本，则不需要type。
![avatar](https://static001.geekbang.org/resource/image/43/44/43fdb35c0300e73bb19c143431f50a44.jpg)

##### import声明
import声明有两种用法，一个是直接import一个模块，另一个是带from的import，它能引入模块里的一些信息
```
import "mod"; //引入一个模块
import v from "mod";  //把模块默认的导出值放入变量v
```
带from的import细分又有三种用法
* import x from "./a.js" 引入模块中导出的默认值。
* import {a as x, modify} from "./a.js"; 引入模块中的变量。
* import * as x from "./a.js" 把模块中所有的变量以类似对象属性的方式引入。

第一种方式还可以跟后两种组合使用。
* import d, {a as x, modify} from "./a.js"
* import d, * as x from "./a.js"

语法要求不带as的默认值永远在最前。注意，这里的变量实际上仍然可以受到原来模块的控制。

##### export声明
模块中导出变量的方式有两种，一种是独立使用export声明，另一种是直接在声明型语句前添加export关键字。
独立使用export声明就是一个export关键字加上变量名列表
```
export { a, b, c }
```
直接在声明型语句前添加export关键字，这里的export可以加在任何声明性质的语句之前，整理如下：
* var
* function(含async和generator)
* class
* let
* const

export还有一种特殊的用法，就是跟default联合使用。export default 表示导出一个默认变量值，它可以用于function和class。这里导出的变量是没有名称的，可以使用import x from "./a.js"这样的语法，在模块中引入。
export default 还支持一种语法，后面跟一个表达式
```
var a = {}
export default a
```
这里跟导出变量是不一致的，这里导出的是值，以后a的变化与导出的值就无关了。
在import语句前无法加入export，但是我们可以直接使用export from语法
```
export a from 'a.js'
```

JavaScript引擎除了执行脚本和模块之外，还可以执行函数。而函数体跟脚本和模块有一定的相似之处。

##### 函数体
执行函数的行为通常是在JavaScript代码执行时，注册宿主环境的某些事件触发的，而执行的过程，就是执行函数体（函数的花括号中间的部分）。
宏任务中可能会执行的代码包括“脚本(script)”“模块（module）”和“**函数体（function body）**”。
函数体其实也是一个语句的列表。跟脚本和模块比起来，函数体中的语句列表中多了return语句可以用。

函数体实际上有四种。
* 普通函数体
```
function foo() {
  // todo
}
```
* 异步函数体
```
async function foo() {
  // todo
}
```
* 生成器函数体
```
function *foo() {
  // todo
}
```
* 异步生成器函数体
```
async function *foo() {
  // todo
}
```
上面四种函数体的区别在于：能否使用await或者yield语句。
关于函数体、模块和脚本能使用的语句，参考下方表格
![avatar](https://static001.geekbang.org/resource/image/0b/50/0b24e78625beb70e3346aad1e8cfff50.jpg)

#### JavaScript语法的全局机制：预处理和指令序言。
##### 预处理
JavaScript执行前，会对脚本、模块和函数体中的语句进行预处理。预处理过程将会提前处理var、函数声明、class、const和let这些语句，以确定其中变量的意义。
var的作用能够穿透一切语句结构，它只认脚本、模块和函数体三种语法结构。
##### function声明
在全局（脚本、模块和函数体），function声明表现跟var相似，不同之处在于，function声明不但在作用域中加入变量，还会给它赋值。
```
console.log(foo);
function foo(){

}
```
##### class声明
class声明在全局的行为跟function和var都不一样。

在class声明之前使用class名，会抛错：
```
console.log(c);
class c{

}
```
这段代码我们试图在class前打印变量c，我们得到了个错误，这个行为很像是class没有预处理，但是实际上并非如此。
```
var c = 1;
function foo(){
    console.log(c);
    class c {}
}
foo();
```
执行后，我们看到，仍然抛出了错误，如果去掉class声明，则会正常打印出1，也就是说，出现在后面的class声明影响了前面语句的结果。
这说明，class声明也是会被预处理的，它会在作用域中创建变量，并且要求访问它时抛出错误。

class的声明作用不会穿透if等语句结构，所以只有写在全局环境才会有声明作用

#### 指令序言机制
脚本和模块都支持一种特别的语法，叫做指令序言（Directive Prologs）。
这里的指令序言最早是为了use strict设计的，它规定了一种给JavaScript代码添加元信息的方式。
```
"use strict";
function f(){
    console.log(this);
};
f.call(null);
```
"use strict"是JavaScript标准中规定的唯一一种指令序言，但是设计指令序言的目的是，留给JS的引擎和实现者一些统一的表达方式，在静态扫描时指定JS代码的一些特性。
"no lint"声明本文件不需要进行lint检查的指令
JavaScript的指令序言是只有一个字符串直接量的表达式语句，它只能出现在脚本、模块和函数体的最前面。