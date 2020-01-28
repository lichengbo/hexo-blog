title: CSS3 属性及动画
date: 2015-10-26 17:08:21
tags: CSS3
---

CSS3是CSS（层叠样式表 Cascading StyleSheet）的升级技术。使原本庞大且复杂的CSS 更加模块化。这些模块包括： 盒子模型、列表模块、超链接方式 、语言模块 、背景和边框 、文字特效 、多栏布局等。CSS3完全向后兼容，现在CSS3 已经基本普及，平常用也是遵循新的标准。这篇主要是说一些CSS3 的动画属性Transitions （过渡）, Animation （动画）和 Transforms （变形）

<!-- more -->

## transition 过渡属性

语法 
```
transition: property duration timing-function delay;
```
- transition-property:  none | all | [ &lt;indent&gt; ] [ ',' &lt;indent&gt; ]\*  规定设置过渡效果的 CSS 属性的名称。
    - none(没有属性改变)
    - all（所有属性改变）默认值
    - indent（元素属性名）；当其值为none时，transition马上停止执行，当指定为all 时，则元素产生任何属性值变化时都将执行transition效果，ident是可以指定元素的某一个属性值
    - ([ &lt;indent&gt; ] [ ',' &lt;indent&gt; ]\* 表示属性值的正闭包，即至少一个属性或有多个属性，多个属性时用逗号隔开)

- transition-duration  规定完成过渡效果需要多少秒或毫秒。
- transition-timing-function: ease | linear | ease-in | ease-out | ease-in-out | cubic-bezier(&lt;number&gt;, &lt;number&gt;, &lt;number&gt;, &lt;number&gt;) [, ease | linear | ease-in | ease-out | ease-in-out | cubic-bezier(&lt;number&gt;, &lt;number&gt;, &lt;number&gt;, &lt;number&gt;)]\*

　　规定速度效果的速度曲线
　　1. ease：（逐渐变慢）默认值，ease函数等同于贝塞尔曲线(0.25, 0.1, 0.25, 1.0)；

　　2. linear：（匀速），linear 函数等同于贝塞尔曲线(0.0, 0.0, 1.0, 1.0)；

　　3. ease-in：(加速)，ease-in 函数等同于贝塞尔曲线(0.42, 0, 1.0, 1.0)；

　　4. ease-out：（减速），ease-out 函数等同于贝塞尔曲线(0, 0, 0.58, 1.0)；

　　5. ease-in-out：（加速然后减速），ease-in-out 函数等同于贝塞尔曲线(0.42, 0, 0.58, 1.0)；

　　6. cubic-bezier：（该值允许你去自定义一个时间曲线）， 特定的cubic-bezier曲线。 (x1, y1, x2, y2)　　四个值特定于曲线上点P1和点P2。所有值需在[0, 1]区域内，否则无效。

　　当然前五个效果比较常用，至于[贝塞尔曲线](http://baike.baidu.com/link?url=FeXhy7EcivcLKbhHxTQw-syG85MuU31Vq-oy57YLpsNpTRm8T-h8WIYCCqUL0ROL3v2Yiq83VRqFGuH3-Cf_jq)不用去纠结，这是PHP100 画的运动效果图

　　![图片](http://www.php100.com/uploadfile/2012/1029/20121029075656108.jpg)

- transition-delay ：定义过渡效果何时开始

## animation 动画属性

- animation-name  规定需要绑定到选择器的 keyframe 名称。。
- animation-duration  规定完成动画所花费的时间，以秒或毫秒计。
- animation-timing-function   规定动画的速度曲线。属性和transition 相同
- animation-delay 规定在动画开始之前的延迟。
- animation-iteration-count: n | infinite   规定动画应该播放的次数。默认值为1 infinite 无限循环
- animation-direction: normal | alternate; 规定是否应该轮流反向播放动画。
    - normal 为默认值。动画应该正常播放。即每次动画从0% 处开始  
    - alternate   动画应该轮流反向播放。即从0% 到100%，然后从100% 变化到0%
- animation-fill-mode：none | forwards | backwards | both 检索或设置对象动画时间之外的状态
    - none：默认值。不设置对象动画之外的状态
    - forwards：设置对象状态为动画结束时的状态
    - backwards：设置对象状态为动画开始时的状态
    - both：设置对象状态为动画结束或开始的状态


定义动画
```
    @keyframes name {
        0% {
            opacity: 1;
        }

        50% {
            opacity: 0;
        }

        100% {
            opacity: 1;
        }
    }
```

## transform 属性
transform: none|transform-functions;

常用的函数有

translate(x,y) 定义 2D 转换
scale(x,y) 定义 2D 缩放转换
rotateX 定义沿着 X 轴的 3D 旋转
skew(x-angle,y-angle) 定义沿着 X 和 Y 轴的 2D 倾斜转换
perspective(n)  为 3D 转换元素定义透视视图

我现在主要用的都是2D 的，3D还不是很会用，先放两个Demo 在这。有时间再把transform 属性补充完整
[CSS3 图片墙](http://lichengbo.github.io/demo/Postcard/)， [图片切换效果](http://lichengbo.github.io/demo/Postcard/css3Demo.html)

本文参考:
[php100 CSS3中的Transition属性详解](http://www.php100.com/html/webkaifa/DIV_CSS/2012/1029/11403.html)
[w3school CSS3教程](http://www.w3school.com.cn/css3/)

