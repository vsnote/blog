---
title: Gulp.js watch错误处理
author: 陈 三
layout: post
date: 2014-05-01T19:47:17+00:00
url: /gulp-js-watch-error-handle.html
views:
  - 1048
categories:
  - 前端开发
tags:
  - gulp.js

---
这是最近使用[Zed][1]编辑CoffeeScript文件经常碰上的一个问题。

如下gulpfile.js文件：

    var gulp = require('gulp'),
      coffee = require('gulp-coffee'),
      path = {
        scripts: ['coffee/**/*.coffee']
      };
    gulp.task('coffee', function() {
      return gulp.src(path.scripts)
        .pipe(coffee())
        .pipe(gulp.dest('js'));
    });
    gulp.task('watch', function() {
      gulp.watch(path.scripts, ['coffee']);
    });
    

命令行下执行：

    gulp watch
    

gulp watch命令监控.coffee文件变化，并自动编译成js文件。

问题是，Zed有自动保存文件的功能，CoffeeScript语句输入一半，切换到其他窗口做点其他事情，Zed就把文件保存好了。gulp watch监测到文件变化，试图编译.coffee文件，但因为语句仅有一半，于是gulp报错并强制退出。

这么一来，我不时就要重启gulp watch命令。

## 解决办法

一个最简单的解决办法，是利用gutil.log捕捉错误，而不是任由错误被抛出：

    var gulp = require('gulp'),
      coffee = require('gulp-coffee'),
      gutil = require('gulp-util'),
      path = {
        scripts: ['coffee/**/*.coffee']
      };
    gulp.task('coffee', function() {
      return gulp.src(path.scripts)
        .pipe(coffee())
        .on('error', gutil.log) // 在这里捕捉编译错误
        .pipe(gulp.dest('js'));
    });
    gulp.task('watch', function() {
      gulp.watch(path.scripts, ['coffee']);
    });
    

但是，这种处理方式，gulp watch在碰上错误时虽然不再强制退出，但也不再继续。gulp watch命令名存实亡，这时对.coffee文件做的修改，并不能被编译。

更美好的处理方式是使用gulp-plumber[^12539.1]：

    npm install gulp-plumber --save
    

新的gulpfile.js文件：

    var gulp = require('gulp'),
      coffee = require('gulp-coffee'),
      plumber = require('gulp-plumber'),
      path = {
        scripts: ['coffee/**/*.coffee']
      };
    gulp.task('coffee', function() {
      return gulp.src(path.scripts)
        .pipe(plumber()) //plumber给pipe打补丁
        .pipe(coffee())
        .pipe(gulp.dest('js'));
    });
    gulp.task('watch', function() {
      gulp.watch(path.scripts, ['coffee']);
    });
    

这样哪怕编译错误，gulp watch命令也能正常工作。

[^12539.1]:    
    [Error management in gulp][2]

 [1]: http://zedapp.org/
 [2]: https://gist.github.com/floatdrop/8269868