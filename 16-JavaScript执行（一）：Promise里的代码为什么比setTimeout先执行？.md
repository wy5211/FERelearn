### JavaScript执行（一）
一段JavaScript代码，在浏览器或者Node环境中先传递给JavaScript引擎，并且要求它去执行。

在ES3和更早的版本中，Js并没有异步执行的能力，这就意味着宿主环境传递给js引擎一段代码，引擎把代码顺序执行，这个就是宿主发起的任务。
但是，在ES5之后，Js加入了Promise，这个Js引擎本身也可以发起任务。

这里的Js语言，采纳JSC引擎的术语，宿主发起的任务称为宏观任务-macroTask，Js引擎发起的任务称为微观任务-microTask。

#### 宏观和微观任务
宏观任务的队列就相当于事件循环
微观任务总是在下一个宏观任务前执行
![avatar](https://static001.geekbang.org/resource/image/16/65/16f70a9a51a65d5302166b0d78414d65.jpg)

#### Promise
Promise是Js提供的一种标准化的异步管理方式，思想是，需要进行io、等待或者其他异步操作的函数，不返回真实结果，而返回一个“承诺”，函数在合适时机调用，选择等待承诺兑现（通过then方法回调）

* 确认宏观任务，遇到宏观任务就在宏观队列中加入任务
* 执行当前宏观任务中的微观任务
* 执行下一个宏观任务
* 执行当前宏观任务中的微观任务
* 执行结束

### async/await
async/await是ES2016新加入的特性，提供了用for、if等代码结构来编写异步方式，runtime基础是Promise。基本用法如下：
```
<!-- 定义 -->
async function foo() {
  console.log('a')
}

<!-- 使用 -->
await foo()

<!-- 循环使用 -->
for(let i = 3; i > 0; i --) {
  await foo()
  console.log(i)
}
console.log('c')
```

#### 练习
实现一个红绿灯，把一个圆形div按照绿色3秒，黄色1秒，红色2秒循环改变背景色
```
<!-- 练习 -->
function sleep(duration){
  return new Promise(resolve => {
    setTimeout(resolve, duration)
  })
}
async function color(duration, name)
{
  console.log(name)
  console.log(new Date())
  await sleep(duration)
}

async function traffic(){
  while(true) {
    await color(3000, 'green')
    await color(1000, 'yellow')
    await color(2000, 'red')
  }
}
await traffic()
```