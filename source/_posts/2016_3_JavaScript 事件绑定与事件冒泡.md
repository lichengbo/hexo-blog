title: 'JavaScript 事件绑定与事件冒泡'
date: 2016-03-20 11:17:00
tags: JavaScript
---
Dom 事件是一个非常常用的知识点，网页中经常需要给元素添加点击、双击等事件函数，用于对用户的操作做出反馈。
原生JavaScript 常用的事件绑定函数为：

<!-- more -->

```
// 方法1 绑定匿名函数
obj.onclick = function() {}

// 方法2
fun() {
    ...
}

obj.onclick = fun;

// 错误的方法
obj.onclick = fun(); // 这样相当于绑定了一个立即执行函数，只会在页面加载的时候执行。

```

这种方法兼容主流浏览器，如果只是绑定一个事件，推荐这样绑定。但是当你想对一个元素绑定多个事件时，这种方法就不行了。它只会执行最后一个绑定的函数。

W3C 标准的绑定方法为 obj.addEventListener(event, function, useCapture);

```
obj.addEventListener('click', fun1, true);
obj.addEventListener('click', fun2, true);
obj.addEventListener('click', fun3, true);

```
执行顺序为method1->method2->method3，实现绑定多个函数。但该方法不支持IE9 以下浏览器。。。

老版本IE 需使用 obj.attachEvent(event, function);

```
obj.attachEvent("onclick", fun1);
obj.attachEvent("onclick", fun2);
obj.attachEvent("onclick", fun3);
```
这种方法的event 前需加on，执行顺序为：method3->method2->method1

> addEventListener 方法中的useCapture 是一个Boolean值，用来设置事件是在事件捕获时执行，还是事件冒泡时执行。attachEvent() 方法没有相关设置，不过IE的事件模型默认是在事件冒泡时执行的，也就是在useCapture 等于false 的时候执行，所以把在处理事件时把useCapture 设置为false 是比较安全，也实现兼容浏览器的效果。

## 事件冒泡

浏览器默认情况下，触发一个元素事件时，若该元素父级元素也有相同的事件，就会触发事件冒泡。而且事件会沿着Dom 树依次传递，直到到达的最顶端document。

浏览器对事件的捕获有两种类型
> 冒泡型事件：事件按照从最特定的事件目标到最不特定的事件目标(document对象)的顺序触发。
捕获型事件：事件从最不精确的对象(document 对象)开始触发，然后到最精确.

比如：

```
<div id="box">
    <p><span>1234</span></p>
</div>

<script type="text/javascript">
    var oSpan = document.getElementsByTagName('span')[0];
    var oP = document.getElementsByTagName('p')[0];
    var oDiv = document.getElementById('box');

    function fun1() {
        console.log("span click");
    }

    function fun2() {
        console.log("p click");
    }

    function fun3() {
        console.log("div click");
    }

    function fun4() {
        console.log("document click");
    }

    oSpan.addEventListener('click', fun1, false);
    oP.addEventListener('click', fun2, false);
    oDiv.addEventListener('click', fun3, false);
    document.addEventListener('click', fun4, true);


    // 点击 1234
    // useCapture 为false，事件冒泡时执行。输出顺序为
    // span click
    // p click
    // div click
    // document click

    // useCapture 为true，事件捕获时执行。输出顺序为
    // document click
    // div click
    // p click
    // span click
</script>
```

阻止事件冒泡
在上面那个例子中，当我点击数字1234时，会触发4个click 函数的执行。但是如果我只想触发span 的click 函数，就需要阻止事件冒泡。

阻止事件冒泡

```
function fun1(e) {
    console.log("span click");

     if (e && e.stopPropagation) {
        e.stopPropagation();
    }
    else {
        window.event.cancelBubble = true; // 使用IE的方式来取消事件冒泡
        return false;
    }
}
```

如果span 的父元素是a 标签的话，点击span 会触发a 标签的跳转。可以阻止浏览器的默认行为

```
function (e) {
    if (e && e.preventDefault) {
        e.preventDefault(); // 阻止默认浏览器动作(W3C) 
    }
    else {
        window.event.returnValue = false; //IE中阻止函数器默认动作的方式 
        return false;
    }
}
```

参考 [js 停止事件冒泡和阻止浏览器默认事件](http://www.cnblogs.com/guohu/archive/2013/01/15/2860888.html)