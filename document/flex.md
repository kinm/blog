<!-- docs/_sidebar.md -->
# Flex布局指南

### **Flex基础概念**
```
display:flex;

//Webkit 内核的浏览器，必须加上-webkit前缀。
```
当某个元素的display指定为flex后，该元素将沿着主轴（main axis）和交叉轴（cross axis）来布局：
![](images/screenshot_1570782738087.png)
* 主轴（main axis）是沿着 flex 元素放置的方向延伸的轴（比如页面上的横向的行、纵向的列）。该轴的开始和结束被称为main start和main end。
* 交叉轴（cross axis）是垂直于 flex 元素放置方向的轴。该轴的开始和结束被称为cross start和cross end。
* 设置了 `display: flex` 的父元素被称之为 flex 容器（flex container）。
* 在 flex 容器中表现为柔性的盒子的元素被称之为flex 项（flex item）。
*****

### **Flex容器的属性**

* ### flex-direction属性

```

flex-direction: row | row-reverse | column | column-reverse;

// flex-direction 属性根据主轴来设置Flex Item的排列方向
// row：以主轴水平方向左侧为起点排列Item（默认值）
// row-reverse：以主轴水平方向右侧为起点排列Item （row反向排列）
// column：以主轴垂直方向顶部为起点排列Item
// column-reverse：以主轴垂直方向底部为起点排列Item （column反向排列）

```

* ### flex-wrap属性

```
flex-wrap: nowrap | wrap | wrap-reverse;

// flex-wrap 属性定义Item换行。（用于轴线上无法排列所有Item时的换行）
// nowrap：不换行（默认值）
// wrap：向下换行（flex容器排列不下的Item在下方换行）
// wrap-reverse：向上换行（flex容器排列不下的Item在上方换行）
```
* ### flex-flow属性
```
flex-flow: <flex-direction> || <flex-wrap>;

// flex-flow 属性是flex-direction和flex-wrap的缩写，你可以将：

flex-direction: row;
flex-wrap: wrap;

// 缩写为：

flex-flow: row wrap;
```

* ### justify-content属性

```
justify-content: flex-start | flex-end | center | space-between | space-around;

// justify-content 属性定义Item在主轴上的对齐方式
// flex-start：左对齐（默认值）
// flex-end：右对齐
// center： 居中
// space-between：两端对齐，Item之间的间隔都相等
// space-around：每个Item两侧的间隔相等（Item之间的间隔比Item与边框的间隔大一倍）
```

* ### align-items属性

```
align-items: flex-start | flex-end | center | baseline | stretch;

// align-items 属性定义Item在交叉轴上的对齐方式。
// flex-start：交叉轴起点对齐
// flex-end：交叉轴终点对齐
// center：交叉轴中间对齐
// baseline：Item第一行文字的基线对齐
// stretch：如果Item未设置高度或设为auto，将占满整个容器的高度（默认值）
```

* ### align-content属性
```
align-content: flex-start | flex-end | center | space-between | space-around | stretch;

// align-content 属性定义了多根轴线的对齐方式，如果Item只有一根轴线，该属性不起作用
// flex-start：与交叉轴起点对齐
// flex-end：与交叉轴终点对齐
// center：与交叉轴中间对齐
// space-between：与交叉轴两端对齐，轴线之间的间隔平均分布
// space-around：每根轴线两侧的间隔都相等（轴线之间的间隔比轴线与边框的间隔大一倍）
// stretch：轴线占满整个交叉轴（默认值）
```

 ![](images/screenshot_1570784978820.png)
*****
### **Flex Item的属性**
* ### order属性
```
.item {
  order: <integer>;
}

// order 属性定义Item的排列顺序，数值越小，排列越靠前，默认为0
```
* ### flex-grow属性
```
.item {
  flex-grow: <number>; /* default 0 */
}
// flex-grow属性定义Item的放大比例，默认为`0`，即如果存在剩余空间，也不放大，如果所有项目的`flex-grow`属性都为1，则它们将等分剩余空间
```
* ### flex-shrink属性
```
.item {
    flex-shrink: <number>; /* default 1 */
}
// flex-shrink属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小
```
*  ### flex-basis属性
```
.item {
  flex-basis: <length> | auto; /* default auto */
}
// flex-basis属性定义了在分配多余空间之前Item占据的主轴空间（main size）,它可以设为跟`width`或`height`属性一样的值（比如350px），则Item将占据固定空间
```
* ### flex属性
```
.item {
  flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}
// flex属性是`flex-grow`,`flex-shrink`和`flex-basis`的简写，默认值为`0 1 auto`。后两个属性可选
// 该属性有两个快捷值：`auto`(`1 1 auto`) 和 none (`0 0 auto`)
```
* ### align-self属性
```
.item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}

// align-self属性允许单个Item有与其他Item不一样的对齐方式，可覆盖`align-items`属性。默认值为`auto`，表示继承父元素的`align-items`属性，如果没有父元素，则等同于`stretch`。
// flex-start：交叉轴起点对齐
// flex-end：交叉轴终点对齐
// center：交叉轴中间对齐
// baseline：Item第一行文字的基线对齐
// stretch：如果Item未设置高度或设为auto，将占满整个容器的高度（默认值）
```