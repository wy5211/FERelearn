### 浏览器 DOM

#### DOM API 介绍

DOM API 大致会包含 4 个部分。

- 节点：DOM 树形结构中的节点相关 API。
- 事件：触发和监听事件相关 API。
- Range：操作文字范围相关 API。
- 遍历：遍历 DOM 需要的 API。

#### 节点

DOM 的树形结构所有的节点有统一的接口 Node，我们按照继承关系，给你介绍一下节点的类型。
![avatar](https://static001.geekbang.org/resource/image/6e/f6/6e278e450d8cc7122da3616fd18b9cf6.png)

#### Node

Node 是 DOM 树继承关系的根节点，它定义了 DOM 节点在 DOM 树上的操作

#### Element 与 Attribute

##### 查找元素

- querySelector
- querySelectorAll
- getElementById
- getElementsByName
- getElementsByTagName
- getElementsByClassName

我们需要注意，getElementById、getElementsByName、getElementsByTagName、getElementsByClassName，这几个 API 的性能高于 querySelector。

而 getElementsByName、getElementsByTagName、getElementsByClassName 获取的集合并非数组，而是一个能够动态更新的集合。

##### Range

Range API 是一个比较专业的领域，如果不做富文本编辑类的业务，不需要太深入

##### 遍历

DOM API 中还提供了 NodeIterator 和 TreeWalker 来遍历树。

自用遍历
```
function walk(el) {
  console.log(el.nodeName);
  if(el.childNodes) {
    for (let childEl of el.childNodes) {
      // 判断为元素标签
      childEl.nodeType === 1 && walk(childEl)
    }
  }
}
walk(document.documentElement)
```
