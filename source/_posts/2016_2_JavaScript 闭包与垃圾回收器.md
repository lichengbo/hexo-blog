title: JavaScript 闭包与垃圾回收器
date: 2016-03-19 17:09:57
tags: JavaScript
---

闭包是指有权访问另一个函数作用域中的变量的函数，或者说能够读取其他函数内部变量的函数。
创建闭包的最常见的方式就是在一个函数内创建另一个函数，通过另一个函数访问这个函数的局部变量。

<!-- more -->

闭包的特性

> 1. 函数嵌套函数
2. 函数内部可以引用外部的参数和变量
3. 参数和变量不会被垃圾回收机制回收

使用闭包的优点

> 1. 能使一个变量长期驻留在内存中
2. 避免全局变量的污染
3. 可以构造私有成员

使用闭包的注意事项
> 1. 注意内存泄漏，特别是在IE 浏览器中。在函数末尾应将没用的变量清除
2. 闭包会在父函数外部，改变父函数内部变量的值。

简单的闭包例子

```
function closure() {
     var num = 1;
     return function() {
         console.log(num);
     }
 }

closure()(); // 1
```

一个常见的例子：给几个button 分别绑定click事件，让其输出对应的顺序
```
<div>
    <input type="button" value="button1">
    <input type="button" value="button2">
    <input type="button" value="button3">
    <input type="button" value="button4">
</div>

```

```
<script type="text/javascript">
    for(var i = 0; i < oBtn.length; i++) {
        oBtn[i].onclick = function() {
            console.log(i);  // 错误的方法。输出4
        }
    }

    // 可以通过给每个button 添加一个属性，记录他的位置
    for(var i = 0; i < oBtn.length; i++) {
        oBtn[i].i = i;
        oBtn[i].onclick = function() {
            console.log(this.i);
        }
    }

    // 通过闭包的方法
    for(var i = 0; i < oBtn.length; i++) {
        (function(num) {
            oBtn[i].onclick = function() {
                console.log(num);
            }
        })(i);
    }
</script>
```

有兴趣的话可以看一看阮一峰博客中的两个思考题 [学习Javascript闭包](http://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html)


## 垃圾回收 (GC:Garbage Collecation)

JavaScript和Java 一样也有垃圾回收器机制，加上现在计算机性能的飞速发展，我们在编码的过程中大可不必考虑内存分配及无用内存的回收问题了，当然这肯定不是良好的编程习惯。及时的清除不用的变量，能够有效的避免内存泄漏。

JavaScript 垃圾回收机制有两种方式
- 标记清除 (mark and sweep)
这是JavaScript最常见的垃圾回收方式，当变量进入执行环境的时候，比如函数中声明一个变量，垃圾回收器将其标记为“进入环境”，当变量离开环境的时候（函数执行结束）将其标记为“离开环境”。
垃圾回收器会在运行的时候给存储在内存中的所有变量加上标记，然后去掉环境中的变量以及被环境中变量所引用的变量（闭包），在这些完成之后仍存在标记的就是要删除的变量了，因为环境中的变量已经无法访问到这些变量了，然后垃圾回收器相会这些带有标记的变量机器所占空间。

- 引用计数 (reference counting)
在低版本IE中经常会出现内存泄露，很多时候就是因为其采用引用计数方式进行垃圾回收。引用计数的策略是跟踪记录每个值被使用的次数，当声明了一个变量并将一个引用类型赋值给该变量的时候这个值的引用次数就加1，如果该变量的值变成了另外一个，则这个值得引用次数减1，当这个值的引用次数变为0的时候，说明没有变量在使用，这个值没法被访问了，因此可以将其占用的空间回收，这样垃圾回收器会在运行的时候清理掉引用次数为0的值占用的空间。

上面引用 [JavaScript 垃圾回收](http://www.cnblogs.com/dolphinX/p/3348468.html)