---
layout: post
title: css flex弹性布局
category: css
tags: [css,html,display,flex,弹性布局]
---
css display flex弹性布局 对flex-direction flex-wrap flex-flow justify-content align-items align-content等属性用法介绍


在开发前端页面时查找关于flex相关信息时看到了阮一峰老师写的关于flex布局的讲解，让人豁然开朗。所以我想把理解的转成自己的话记录下来。感谢阮一峰老师的文章。
[阮老师的原文地址](https://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)
图片元素copy阮老师的哈！！！

flex属性在线实验网站
[英文的在线的](https://the-echoplex.net/flexyboxes/)
[阮老师的博客评论中看到的](https://xluos.github.io/demo/flexbox/)

## flex与传统的区别
传统的布局靠盒模型float、margin、padding、position来进行排版，现在虽然也是一直用，但有些时候这种方式没有直接用flex来的方便，最明显的一点就是可以用==flex实现垂直居中==。
### 注意
设置元素为flex后，子元素的`float` `clear`和`vertical-align`将会失效。
行级元素可以用
```
display: inline-flex;
```
### 基本概念
我看了阮老师的讲解的基本概念，太专业了。我感觉我是比较喜欢土一点接地气的方式来理解。
在对元素设置为`dispaly: flex;`后就可以通过flex附带的几个属性对子元素（直系后代）进行控制了。
## 6个属性
### 1、flex-direction 排列方式 上下左右
```
.wrapper {
  flex-direction: [row | row-reverse | column | column-reverse];
}
row 默认值 子元素从左到右排列
row-reverse 子元素从右到左排列
column 子元素从上到下排列
column 子元素从下到上排列
```
![阮老师的图片](https://www.ruanyifeng.com/blogimg/asset/2015/bg2015071005.png)
### 2、flex-wrap 是否换行 上下位置
```
.wrapper{
  flex-wrap: [nowrap | wrap | wrap-reverse];
}
nowrap 默认值 不换行
wrap 正常的换行 超过内容下一行开始
wrap-reverse 和wrap相反 超过内容在最上面
```
wrap-reverse方式
![阮老师的图片](https://www.ruanyifeng.com/blogimg/asset/2015/bg2015071009.jpg)
### 3、flex-flow 前面两个的简写
```
.wrapper {
  flex-flow: [flex-direction || flex-wrap];
}
```
### 4、justify-content 水平的对其方式
```
.wrapper {
  justify-content: [flex-start | flex-end | center | space-between | space-around];
}
flex-start 默认值 左对齐
flex-end 右对齐
center 居中
space-between 两端对齐
space-around 每个子元素两侧的间隔相等。所以，子元素之间的间隔比子元素与边框的间隔大一倍
```
![阮老师的图片](https://www.ruanyifeng.com/blogimg/asset/2015/bg2015071010.png)
### 5、align-items 垂直对其方式
```
.wrapper {
  align-items: [flex-start | flex-end | center | baseline | stretch];
}
flex-start：顶部对齐。
flex-end：底部对齐。
center：中点对齐 元素上下居中。
baseline: 子元素的第一行文字的基线对齐。
stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。
```
![阮老师的图片](https://www.ruanyifeng.com/blogimg/asset/2015/bg2015071011.png)
### 6、align-content 多个子元素的对齐方式
该属性是对有多行子元素的排列方式设置，如果只有一行则无效
```
.wrapper {
  align-content: [flex-start | flex-end | center | space-between | space-around | stretch];
}
flex-start：顶部对齐。
flex-end：底部对齐。
center：中心对齐。
space-between：上下对齐，子元素之间的间隔平均分布 justify-content属性的垂直版space-between
space-around：每个子元素两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。justify-content属性的垂直版space-around
stretch（默认值）：占满整个盒子（可能会使元素拉伸）。
```
![阮老师的图片](https://www.ruanyifeng.com/blogimg/asset/2015/bg2015071012.png)
## 6个子元素属性
对父级元素设置成`display: flex;`后子元素也会有几个可选属性对子元素进行单独的控制
### 1、order 子元素的排列顺序
定义子元素的排列顺序越小越靠前
```
.children {
  order: <int>;
}
```
![阮老师的图片](https://www.ruanyifeng.com/blogimg/asset/2015/bg2015071013.png)
### 2、flex-grow 子元素放大比例
定义子元素的放大比例，默认是`0`即如果存在剩余空间，也不放大。
如果所有子元素的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。如果一个子元素的flex-grow属性为2，其他子元素都为1，则前者占据的剩余空间将比其他项多一倍。
允许浮点数
.children {
  flex-grow: <number>; /* default 0 */
}
![阮老师的图片](https://www.ruanyifeng.com/blogimg/asset/2015/bg2015071014.png)
### 3、flex-shrink 子元素缩小比例
定义了子元素的缩小比例，默认为1，即如果空间不足，该子元素将缩小。
如果所有子元素的flex-shrink属性都为1，当空间不足时，都将等比例缩小。如果一个子元素的flex-shrink属性为0，其他子元素都为1，则空间不足时，前者不缩小。

负值对该属性无效。
![阮老师的图片](https://www.ruanyifeng.com/blogimg/asset/2015/bg2015071015.jpg)
### 4、flex-basis 子元素父级的空间的宽度
定义了在分配多余空间之前，子元素占据的父级空间（main size）。浏览器根据这个属性，计算盒子是否有多余空间。它的默认值为auto，即子元素的本来大小。 子元素的basis最大 等于父级宽度
```
.children {
  flex-basis: <length px|em|rem|...> | auto; /* default auto */
}
它可以设为跟width或height属性一样的值（比如350px），则子元素将占据固定空间。
```
### 5、flex 对前面3个的简写
`flex`属性是`flex-grow`, `flex-shrink` 和 `flex-basis`的简写，默认值为0 1 auto。后两个属性可选。
```
.item {
  flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}
```
建议优先使用这个属性
该属性有两个快捷值：`auto` (`1 1 auto`) 和 `none` (`0 0 auto`)。
### 6、align-self 自定义对齐方式
align-self属性对单个子元素设置不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。
```
.item {
  align-self: [auto | flex-start | flex-end | center | baseline | stretch];
}
```
该属性可能取6个值，除了auto，其他都与align-items属性完全一致。
![阮老师的图片](https://www.ruanyifeng.com/blogimg/asset/2015/bg2015071016.png)
