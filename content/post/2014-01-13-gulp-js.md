---
title: Gulp.js
author: 陈 三
layout: post
date: 2014-01-12T16:08:44+00:00
url: /gulp-js.html
views:
  - 972
categories:
  - 前端开发
tags:
  - grunt.js
  - gulp.js

---
好像突然间，就看到 twitter 上到处在聊 gulp.js [^11402.1]了，还拿来跟 grunt.js [^11402.2]作对比，说它的语法更简洁，说它的速度更快&#8230;&#8230;

**Note**：_gulp 在2013.7.18推出0.1版本，grunt 在两年前推出_

grunt.js 下，加载插件是这样写的：

    grunt.loadNpmTasks('grunt-contrib-uglify');
    

gulp.js 下，则是这样：

    var uglify = require('gulp-uglify');
    

gulp 加载插件的语法有点 Node.js 的意思，就我个人喜好说，确实会喜欢 `require` 的方式多一点。

再来看定义任务。

gulp 下是这样：

    gulp.task('scripts', function() {// 定义一个脚本任务
      // 最小化、混淆 js 目录下不包括 vendor 子目录的所有 js 文件，并将结果保存到 build/js 目录下
      return gulp.src(['js/**/*.js', '!js/vendor/**'])
        .pipe(uglify()) // pipe 是一个管道，可以连接不同部分
        .pipe(rename({ // 重命名文件
            ext: ".min.js"
        }))
        .pipe(gulp.dest('build/js'));
    });
    

这个任务在 grunt 下写的话：

    uglify: { 
          build: {
          files: [
            {
              expand: true,     
              cwd: 'js/',      
              src: ['**/*.js', !js/vendor/**], 
              dest: 'build/js',   
              ext: '.min.js',   
            }
          }
        }
    

我觉得 gulp 的 pipe 用法确实要比 grunt 更漂亮。因为很多任务间常常要有联系，比如检查语法后（jshint）后要最小化混淆（uglify）处理，gulp 可以用 pipe 实现，直观明了，grunt 要定义两个任务，一个 jshint，一个 uglify，然后在 uglify 任务中把 `src` 设置为 jshint 任务的结果，比如 `<%= jshint.all.dest %>` 这样，任务一多，可能就有点乱。

最后再来看注册任务。

gulp 下：

    gulp.task('default', function() {
      gulp.run('scripts', 'images');
    }
    

grunt 下：

    grunt.registerTask('default', ['scripts', 'images']);
    

一番比较下来，gulp 的语法确实要更讨人喜欢。不过**我猜** grunt 的插件支持目前应该要更多些。至于 gulp.js <q>速度更快</q>一说，除非项目很大，否则比较的意义并不大。

[^11402.1]:    
    [gulp.js &#8211; the streaming build system][1]

[^11402.2]:    
    [Gruntjs – 陈三][2]

 [1]: http://gulpjs.com/
 [2]: http://www.zfanw.com/blog/gruntjs.html