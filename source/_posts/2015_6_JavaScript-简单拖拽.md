title: JavaScript 简单拖拽
date: 2015-11-18 19:11:38
tags: JavaScript
---

最近在学习HTML5 的一些东西，做的时候用的是原生JS，正好算是复习JS了。在查资料的时候看到了一大神的博客中有个JS 拖拽效果，并且封装成了一个插件。但是作者的例子是四五年前的，而且有一些地方也没有限制。于是也想仿他的轮子做一下，案例倒不复杂，只是中间遇到了一些坑。

<!-- more -->

## 实现原理

拖拽效果非常常见，比如一些网站的快速登录，会弹出一个小的可以拖动登录界面。原理也很简单，就是鼠标移动时获取鼠标移动的距离，然后改变div 的top 和 left 的值。当然div 必须采用相对定位或是绝对定位，然后再进行一些边缘判断。

## 代码使用及效果

你可以点击这里查看源码 [lcb.drag.js](http://lichengbo.github.io/plugin/lcb.drag.js) 压缩文件 [lcb.drag.min.js](http://lichengbo.github.io/plugin/lcb.drag.min.js) 或在线Demo  [JS 拖拽效果](http://lichengbo.github.io/demo/JavaScript/jsdrag.html)

使用方法：
- 首先调用js文件，如下：

```
<script src="http://lichengbo.github.io/plugin/lcb.drag.js" type="text/javascript"></script>
```

- 然后调用startDrag 函数，将需要拖拽的对象ID传入即可

### 示例

- CSS

```
<style type="text/css">
    * {
        margin: 0;
        padding: 0;
    }

    body {
        background: #D9D9D9;
        font-family: 微软雅黑;
        overflow: hidden;
    }

    #container {
        width: 350px;
        height: 400px;
        background: #FFFFFF;
        position: absolute;
        top: 50px;
        left: 35%;
    }

    #header {
        height: 50px;
        background: #F7F7F7;
        cursor: move;
        line-height: 50px;
        padding-left: 10px;
        -webkit-user-select:none; /* 这句用于兼容兼容Chrome，加在拖拽对象上 */
    }

    .content {
        padding:10px 5px;
    }
</style>
```

- HTML

```
<div id="container">
    <div id="header">header</div>
    <div class="content">content</div>
</div>
```

- JS

```
<script src="http://lichengbo.github.io/plugin/lcb.drag.js" type="text/javascript"></script>
<script type="text/javascript">
    startDrag(header, container);
</script>
```

## 遇到的坑

其实这个拖拽效果倒不是重点，关键是拖拽时被拖拽的div 会产生选中事件。原本想阻止掉不就行了，然而遇到了万恶的兼容性问题。。查了好久才知道怎么解决。原文地址 [CSS禁用鼠标拖拽选中内容](http://my.oschina.net/web5/blog/146190?fromerr=5BTpfapD)

尤其是Chrome 用js 去阻止的话，效果反而更差。所以最好采用了Chrome 用CSS 去阻止选中事件，FF 和 IE 用js 阻止。但IE 好像有时会出现跳帧的情况~

代码如下：

```
CSS 阻止方法
chrome: -webkit-user-select:none;
firxfox: -moz-user-select:none;

IE需要使用JS的onSelected 事件

function disableSelection(target) {
    if (typeof target.onselectstart != "undefined") //IE route
        target.onselectstart=function(){return false}
    else if (typeof target.style.MozUserSelect != "undefined") //Firefox route
        target.style.MozUserSelect="none";
    else if(typeof target.style.webkitUserSelect != "undefined")
        target.style.webkitUserSelect = "none"; // 测试发现 Chrome 支持不好，最好用CSS 
    else //All other route (ie: Opera)
        target.onmousedown = function(){return false}
};
```

## 额外的知识点

在用JS 改变left 和 top 值时需要获取对象的CSS 属性值，但是JS obj.style.width 等只能获取行间样式
详细我放在另一篇转载的文章里 [javascript获取元素CSS样式代码示例](http://lichengbo.github.io/2015/11/18/6_2_javascript获取元素CSS样式代码示例/)


参考博客 [JavaScript实现最简单的拖拽效果](http://www.zhangxinxu.com/wordpress/2010/03/javascript实现最简单的拖拽效果/)