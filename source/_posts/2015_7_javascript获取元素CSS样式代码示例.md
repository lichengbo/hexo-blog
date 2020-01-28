title: javascript获取元素CSS样式代码示例
date: 2015-11-18 21:57:46
tags: [JavaScript, 转载]
---

## 使用css控制页面有4种方式，分别为行内样式(内联样式)、内嵌式、链接式、导入式。
- 行内样式(内联样式)即写在html标签中的style属性中，如
<!-- more -->

```
<div style="width:100px;height:100px;"></div>
```
- 内嵌样式即写在style标签中，例如

```
<style type="text/css">
    div {width:100px; height:100px;}
</style>
```
- 链接式即为用link标签引入css文件，例如

```
<link href="test.css" type="text/css" rel="stylesheet" />
```

- 导入式即为用import引入css文件，例如

```
@import url("test.css")
```

## 获取样式

> 如果想用javascript 获取一个元素的样式信息，首先想到的应该是元素的style属性。但是元素的style属性仅仅代表了元素的内联样式，如果一个元素的部分样式信息写在内联样式中，一部分写在外部的css文件中，通过style属性是不能获取到元素的完整样式信息的。因此，需要使用元素的计算样式才能获取元素的样式信息。

在上一篇文章中用到的函数如下
```
function getCss(obj, key){
    return obj.currentStyle ? obj.currentStyle[key] : document.defaultView.getComputedStyle(obj, false)[key]   
};
```


## 示例

```
<style type="text/css">
    #testDiv{
    　　border:1px solid red;
    　　width: 100px;
    　　height: 100px;
    　　color: red;
    }
</style>

<div id="testDiv"></div>

<script type="text/javascript">
    var testDiv = document.getElementById("testDiv");
    var styleInfo = window.getComputedStyle ? window.getComputedStyle(testDiv, "") : testDiv.currentStyle;
    var width = styleInfo.width;　　//100px;
    var height = styleInfo.height;　　//100px;
    var color = styleInfo.color;　　// rgb(255, 0, 0)
</script>
```

最后要注意一点，元素的计算样式是只读的，如果想设置元素样式，还得用元素的style属性（这个才是元素style属性的真正用途所在）。

原文地址： javascript获取元素CSS样式代码示例 [http://www.jb51.net/article/43868.htm](http://www.jb51.net/article/43868.htm)


