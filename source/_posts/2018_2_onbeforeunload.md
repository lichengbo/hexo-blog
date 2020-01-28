---
title: Vue中实现浏览器onbeforeunload 效果
date: 2018-03-22 20:06:49
tags: JavaScript
---

最近开发遇到了检测用户修改未保存时，关闭浏览器提示保存的需求，类似下图。本文记录下用到的知识点。
![](https://user-gold-cdn.xitu.io/2018/4/20/162e0f5c5288924e?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

<!-- more -->

## window.onbeforeunload

详细描述见 <a href="https://developer.mozilla.org/zh-CN/docs/Web/API/Window/onbeforeunload" target="_blank">onbeforeunload MDN 文档</a> 作用是：当窗口即将被卸载（关闭）时，会触发该事件。此时页面文档依然可见，且该事件的默认动作可以被取消。另外页面刷新和切换也会触发该函数。

使用方法：
```
window.onbeforeunload = () => {
  if(hasChanged)
    return "放弃当前未保存内容而关闭页面？";
}
```

## window.onunload

onunload 方法用法与onbeforeunload 相同，功能相同

对比如下：
> onbeforeunload 浏览器兼容性较好，主流浏览器均支持。onunload 兼容性较差
onbeforeunload在onunload之前执行，它还可 以阻止onunload的执行。

## 导航守卫
但是onbeforeunload 在Vue 单页网站中有时候不起作用，因为单页切换不会触发窗口卸载事件。因此要用到 Vue-router <a href="https://router.vuejs.org/zh-cn/advanced/navigation-guards.html" target="_blank">导航守卫</a>来实现，用到了组件内的守卫。用法如下：

```
beforeRouteLeave: function(to, from , next){
  if (hasChanged) {
    this.$confirm('放弃当前未保存内容而关闭页面？', '提示', {
      confirmButtonText: '确定',
      cancelButtonText: '取消',
      type: 'warning'
    }).then(() => {
      next()
    }).catch(() => {
      next(false)
    });
  } else {
    next()
  }
}
```