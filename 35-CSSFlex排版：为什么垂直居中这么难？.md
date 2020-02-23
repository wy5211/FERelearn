### CSSFlex排版

##### Flex的设计
Flex排版的核心是display:flex和flex属性，它们配合使用。具有display:flex的元素我们称为flex容器，它的子元素或者盒被称作flex项。
flex项如果有flex属性，会根据flex方向代替宽/高属性，形成“填补剩余尺寸”的特性，这是一种典型的“根据外部容器决定内部尺寸”的思路，也是我们最常用的Windows和Apple窗口系统的设计思路。

##### Flex的原理
FLex支持横向和纵向，这样我们就需要做一个抽象，我们把Flex延伸的方向称为“主轴”，把跟它垂直的方向称为“交叉轴”。这样，flex项中的width和height就会称为交叉轴尺寸或者主轴尺寸。
而Flex又支持反向排布，这样，我们又需要抽象出交叉轴起点、交叉轴终点、主轴起点、主轴终点，它们可能是top、left、bottom、right。
Flex布局中有一种特殊的情况，那就是flex容器没有被指定主轴尺寸，这个时候，实际上Flex属性完全没有用了，所有Flex尺寸都可以被当做0来处理，Flex容器的主轴尺寸等于其它所有flex项主轴尺寸之和。

##### Flex的应用
**垂直居中：**
```
#parent {
  display:flex;
  width:300px;
  height:300px;
  outline:solid 1px;
  justify-content:center;
  align-content:center;
  align-items:center;
}
#child {
  width:100px;
  height:100px;
  outline:solid 1px;
}

<div id="parent">
  <div id="child">
  </div>
</div>
```
思路是创建一个只有一行的flexbox，然后用align-items: center和align-content: center来保证行位于容器中，元素位于行中。

**两列等高：**
```
.parent {
  display:flex;
  width:300px;
  justify-content:center;
  align-content:center;
  align-items:stretch;
}
.child {
  width:100px;
  outline:solid 1px;
}

<div class="parent">
  <div class="child" style="height:300px;">
  </div>
  <div class="child">
  </div>
</div>
<br/>
<div class="parent">
  <div class="child" >
  </div>
  <div class="child" style="height:300px;">
  </div>
</div>
```
思路是创建一个只有一行的flexbox，然后用stretch属性让每个元素高度都等于行高。

**自适应宽：**
```
.parent {
  display:flex;
  width:300px;
  height:200px;
  background-color:pink;
}
.child1 {
  width:100px;
  background-color:lightblue;
}
.child2 {
  flex:1;
  outline:solid 1px;
}

<div class="parent">
  <div class="child1">
  </div>
  <div class="child2">
  </div>
</div>
```
思路是要自适应的元素添加flex属性。

