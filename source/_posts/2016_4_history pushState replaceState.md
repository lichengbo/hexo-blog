title: 'HTML5 history pushState&replaceState'
date: 2016-09-16 17:35:37
tags: JavaScript
---
浏览器的history 对象有很多实用的方法和属性，比如back(), forward(), go(), length等。HTML5 中增加的pushState 和replaceState 方法能够修改浏览器的历史记录，这使得我们能在不跳转页面的前提下修改浏览器的URL。这就解决了在Ajax 局部刷新页面时，浏览器后退键无效的缺点。

<!-- more -->

## pushState

使用方法
```
history.pushState(stateObject, title, url);
```

使用中我感觉前两个参数作用不是很大，[MDN](https://developer.mozilla.org/zh-CN/docs/DOM/Manipulating_the_browser_history) 对其解释如下

>- 状态对象（state object） 一个JavaScript对象，与用pushState()方法创建的新历史记录条目关联。无论何时用户导航到新创建的状态，popstate事件都会被触发，并且事件对象的state属性都包含历史记录条目的状态对象的拷贝。
- 标题（title） FireFox浏览器目前会忽略该参数，虽然以后可能会用上。考虑到未来可能会对该方法进行修改，传一个空字符串会比较安全。或者，你也可以传入一个简短的标题，标明将要进入的状态。
- 地址（URL） 新的历史记录条目的地址。浏览器不会在调用pushState()方法后加载该地址，但之后，可能会试图加载，例如用户重启浏览器。新的URL不一定是绝对路径；如果是相对路径，它将以当前URL为基准；传入的URL与当前URL应该是同源的，否则，pushState()会抛出异常。该参数是可选的；不指定的话则为文档当前URL。

所以我使用时直接这样调用
```
history.pushState(null, "", url);
```

且如果url 传入的是相对路径，只会修改当前url 的最后一个参数。在MDN 中我还看到了操作location 有种方法也能起到这种效果，就是使用location 修改url 的hash 值时。url 会变化，且页面不会跳转

```
window.location = "#abc";
```

通过上面这种方式和pushState() 都会增加history 记录，history.length 会加一

## replaceState
replaceState 方法和pushState 方法使用方式一致，区别是replaceState 只修改当前url 参数，不会创建新的history 条目。

另外有人把pushState 和ajax 结合起来，封装成了[pjax](https://github.com/defunkt/jquery-pjax) 插件，查看[Demo](http://pjax.herokuapp.com/)