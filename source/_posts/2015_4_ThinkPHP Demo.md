title: "随便说说和一个ThinkPHP Demo"
date: 2015-10-07 16:07:25
tags: php
---
十一假期很快就过去了，转眼已经开学第四周了。这几周真正是回到了大学生活的节奏，每周前三天总共4节课。没课的时候呆在宿舍，玩玩电脑写写代码。下午没事的时候就去打球，感觉这几周打球的次数都顶的上过去一学期的次数了。晚上不查寝了，也不用跑到机房去自习了。总在宿舍呆着，玩游戏的时间倒也增加了不少。
<!-- more -->
不废话了，上学期总想着学PHP，然后各种事情瞎忙，也没去看。小学期的时候交作业倒是用了一点，用php写了一个Web 版的图书管理系统，但是写的非常乱。而且主要的数据库结构是小组其他成员弄的，基本上就是对数据库查询，和数据的显示。这段时间正好没事又看了下，然后试着用了下比较流行的后台框架ThinkPHP，对MVC 模型又有了一些认识。以前虽然知道模块化的优点，但有时候总是想不通有些地方分层的用处。暑假实习时用Angular 也是MVC 模式，用的时候有的地方总是不明白值是怎么传过去的，看了TP 之后感觉有些地方都是想通的。ThinkPHP 模块化非常好，也封装了很多基本的SQL方法，我现在写的Demo 因为还没有很多的功能，所以基本没有自己写SQL 语句，都是用的封装的函数。我总感觉使用框架一定程度上降低了学习的成本，也简化了开发的过程，但是这样不能了解内部的工作机制，比如我在写的时候基本上没有对model 层进行操作，基本上都是control 和view 部分。


现在主要完成后台部分的功能，因为原本作业已经有了大概的模型，所以只是增加模块和功能。好多js 代码都没有分开，也懒得去重构了。主要目的是了解一下thinkphp 的使用。写的过程中也发现了一些问题，暂时不在这里重述了，都记录在了开发日志中，等到Demo 基本完成时再来修改吧。但是由于前台想实现一个类似购物的平台，正好和后台图书销售整合起来。估计写完也要一段时间。由于样式用的bootstrap，也就先不贴效果图了。先放上[代码地址](https://github.com/lichengbo/booksale)