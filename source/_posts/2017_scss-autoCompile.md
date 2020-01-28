---
title: scss 自动编译配置
date: 2017-12-31 16:14:36
tags: css
---

## 引语
目前项目使用的CSS预处理器是SCSS，工作流是Ruby+SASS+IDEA file watcher。Windows 需要安装Ruby，配置繁琐。而且随着项目向Vue 迁移，前端开发不需要本地起Tomcat 服务。另外VSCode 编辑器的发展，越来越多的前端开发使用这个轻量的编辑器，因此想更换下SCSS 的编译流程。本文记录下配置过程踩下的坑。

<!-- more -->

## 基本配置
使用自动化Gulp，相关配置如下：

```
var gulp = require('gulp');
var sass = require('gulp-sass');
var watch = require('gulp-watch');

gulp.task('default', function() {
  return gulp.src('sass/*.scss')
    .pipe(watch('sass/*.scss'))
    .pipe(sass())
    .pipe(gulp.dest('dist'));
});
```

上面的几行命令即可完成SCSS 文件监听，改动编译。但是一个文件改动就会编译目录下的全部SCSS 文件，因此需要修改配置实现增量编译更新。使用gulp-changed 完成该功能。参考该[博客](http://www.cnblogs.com/zichi/p/6265208.html)。

修改如下
```
var changed = require('gulp-changed');

gulp.task('compileSass', () => {
    return gulp.src(ENTRY)
    .pipe(changed(DIST, { // dest 参数需要和 gulp.dest 中的参数保持一致
        extension: '.css' // 如果源文件和生成文件的后缀不同，这一行不能忘
    }))
    .pipe( sass() )
    .pipe( gulp.dest( DIST ) );
});

gulp.task('watch', () => {
    gulp.watch(ENTRY, ['compileSass']);
});
```

其中几个注意点：
>1. 如果源文件和生成文件的后缀不一样，需要加上 extension 参数。
>2. gulp-changed 是基于文件的判断，不启动watch，直接编译也是有效的。
>3. 因为 gulp-changed 只会将修改过的文件往下 pipe，所以如果后续有需要合并的操作（concat 操作），那么就会导致文件缺失，合并后的文件其实就是修改过的文件了。

## 配置优化
- 增加autoprefixer

```
.pipe(autoprefixer({
    browsers: ['last 2 versions'],
    cascade: false
}))
```


