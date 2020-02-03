### JavaScript执行（二）

#### 闭包
实际上js中跟闭包对应的概念就是“函数”。

#### 执行上下文：执行的基础设施
**在ES3中**
* scope：作用域，也常常被叫做作用域链。
* variable object：变量对象，用于存储变量的对象
* this value：this值

**在ES5中**
* Lexical enviroment：词法环境，获取变量时使用
* variable enviroment：变量环境，声明变量时使用
* this value：this值

**在ES2018中**
* Lexical enviroment：词法环境，获取变量或this值时使用
* variable enviroment：变量环境，声明变量时使用
* code evaluation state：用于恢复代码执行位置
* Function：执行的任务是函数时使用，表示正在被执行的函数
* ScriptOrModule：执行的任务是脚本时使用，表示正在被执行的代码
* Realm：使用的基础库和内置对象实例
* Generator：仅生成器上下文有这个属性，表示当前生成器

### var声明与赋值
立即执行的函数表达式（IIFE）
```
  ;(function() {
    //
  })()

  ;(function() {
    //
  })()
```
推荐使用void关键字
```
void function(){
    var a;
    //code
}();
```
这有效避免了语法，同时语义上void表示忽略后面表达式的值，变成undefined。

### let
let在运行时引入了块级作用于，在let之前，Js的if、for等语句不产生作用于
以下语句会产生作用于：
* for
* if
* switch
* try/catch/finally

### Realm
在实际的前端开发中，通过iframe等方式创建多window环境并非罕见的操作，所以，这才促成了新概念Realm的引入