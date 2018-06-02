---
layout: post
title: Turnjs 参数选项
tags: [js,turnjs]
category: js
---
turnjs经常用来做html5页面的翻页效果，详细的罗列了turnjs4.*的参数作用。


## 选项 options
<table>
    <tr>
        <td>选项</td>
        <td>类型</td>
        <td>默认值</td>
        <td>描述</td>
    </tr>
    <tr>
        <td>acceleration</td>
        <td>Boolean</td>
        <td>TRUE</td>
        <td>设置硬件加速模式，对于触摸设备，此值必须为真。</td>
    </tr>
    <tr>
        <td>autoCenter</td>
        <td>Boolean</td>
        <td>FALSE</td>
        <td>取决于有多少页面可见，将翻页中心居中。 autoCenter选项更改了翻书的CSS margin-left属性。</td>
    </tr>
    <tr>
        <td>direction</td>
        <td>String</td>
        <td>ltr</td>
        <td>指定从左到右（DIR = ltr，默认值）或从右到左（DIR = rtl）的翻页书的方向性。</td>
    </tr>
    <tr>
        <td>display</td>
        <td>String</td>
        <td>double</td>
        <td>设置显示模式。使用单个显示每个视图只有一个页面或双重显示两个页面。single or double</td>
    </tr>
    <tr>
        <td>duration</td>
        <td>Number</td>
        <td>600</td>
        <td>以毫秒为单位设置转换的持续时间。如果设置0（零），翻页时不会发生转换。</td>
    </tr>
    <tr>
        <td>gradients</td>
        <td>Boolean</td>
        <td>TRUE</td>
        <td>在过渡期间显示渐变和阴影。</td>
    </tr>
    <tr>
        <td>height</td>
        <td>Number</td>
        <td>$("flipbook").height()</td>
        <td>设置翻书的高度。</td>
    </tr>
    <tr>
        <td>elevation</td>
        <td>Number</td>
        <td>0</td>
        <td>设置转换期间页面的高度。</td>
    </tr>
    <tr>
        <td>page</td>
        <td>Number</td>
        <td>1</td>
        <td>初始化动画书时设置页面。</td>
    </tr>
    <tr>
        <td>pages</td>
        <td>Number</td>
        <td>$("#flipbook").children().length</td>
        <td>设置任意数量的页面。如果页面数量大于#flipbook中的元素数量，则需要使用addPage方法动态添加这些页面。</td>
    </tr>
    <tr>
        <td>turnCorners</td>
        <td>String</td>
        <td>bl,br</td>
        <td>bl,br or tl,tr or bl,tr 设置从页面，下一页或上一页等方法翻页时使用的角点。</td>
    </tr>
    <tr>
        <td>when</td>
        <td>Object</td>
        <td>Empty object</td>
        <td>设置事件监听器。键必须列在事件列表中。 $("#flipbook").turn({when: { turning: function(event, page, pageObject){} } });</td>
    </tr>
    <tr>
        <td>width</td>
        <td>Number</td>
        <td>$("#flipbook").width()</td>
        <td>设置页面的宽度。</td>
    </tr>
</table>