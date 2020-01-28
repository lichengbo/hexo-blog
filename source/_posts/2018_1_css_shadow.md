---
title: css shadow 参数转换工具
date: 2018-03-07 14:17:14
tags: '转载'
---

阴影常用的有 <code>box-shadow</code> 和 <code>text-shadow</code> 

box-shadow: h-shadow v-shadow blur spread color inset;

可以直接使用转换工具将参数转换为CSS语法：[转换工具](https://lichengbo.cn/tool/shadow.html)

<!-- more -->

相关概念：

"混合模式"：Photoshop提供了各式各样的混合模式，但是CSS3阴影只支持正常模式（normal）。

"颜色（color）"：阴影颜色。对应于CSS3阴影中的 color 值。

"不透明度（opacity）"：阴影的不透明度。对应于CSS3阴影的颜色 rgba() 中的 a 值。

"角度（Angle）"：投影的角度。

"距离（Distance）"：阴影的距离。根据角度和距离可以换算出CSS3阴影中的x-offset和y-offet。 x-offset = Distance x cos(180 - Angle) ， y-offset = Distance x sin(180 - Angle)

"扩展（Spread）"：阴影的扩展大小。控制阴影实体颜色和虚化颜色的多少。 Spread x Size = 阴影中实体颜色的大小 。剩下的就是虚化的颜色。CSS3阴影 spread-radius = Spread x Size

"大小（Size）"：阴影的大小。在CSS3中 blur-radius + spread-radius = Size 即 blur-radius = Size - spread-radius 。

若样式如图
![样式设置图](http://files.jb51.net/file_images/article/201511/2015112717073526.png)

计算如下：

```
color: rgba(118,113,113,.75)
x-offset: 5 x cos(180°- 145°) = 4.09px
y-offset: 5 x sin(180°- 145°) = 2.87px
spread-radius: 10 x 6% = 0.6px
blur-radius: 10 - 0.6 = 9.4px;
box-shadow: 4.09px 2.87px 9.4px 0.6px rgba(118,113,113,.75);
text-shadow: 4.09px 2.87px 9.4px rgba(118,113,113,.75);
```

文章转自[http://www.jb51.net/css/404167.html](http://www.jb51.net/css/404167.html)