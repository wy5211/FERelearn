### CSS渲染

#### 颜色的原理
##### RGB颜色
我们在计算机中，最常见的颜色表示法是RGB颜色，它符合光谱三原色理论：红、绿、蓝三种颜色的光可以构成所有的颜色。
![avatar](https://static001.geekbang.org/resource/image/7f/a1/7f5bf39cbe44e36758683a674f9fcfa1.png)
三色数值最大表示白色，三色数值为0表示黑色。

##### CMYK颜色
实际上是这样的，颜料显示颜色的原理是它吸收了所有别的颜色的光，只反射一种颜色，所以颜料三原色其实是红、绿、蓝的补色，也就是：品红、黄、青。
对CMYK颜色表示法来说，同一种颜色会有多种表示方案，但是我们参考印刷行业的习惯，会尽量优先使用黑色。

##### HSL颜色
色相（H）纯度（S）和明度（L）
![avatar](https://static001.geekbang.org/resource/image/a3/ce/a3016a6ff178870d6dba23f807b0dfce.png)

##### 其它颜色
RGBA是代表Red（红色）、Green（绿色）、Blue（蓝色）和Alpha的色彩空间

##### 渐变
在CSS中，background-image这样的属性，可以设为渐变。CSS中支持两种渐变，一种是线性渐变，一种是放射性渐变

##### 形状
* border
* box-shadow
* border-radius
