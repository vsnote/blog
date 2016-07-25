---
title: Gruntjs 批量无损压缩图片大小
author: 陈 三
layout: post
date: 2013-07-20T09:32:50+00:00
url: /gruntjs-optimize-image-size-loseless.html
dsq_thread_id:
  - 1514155702
views:
  - 1946
categories:
  - 前端开发
tags:
  - Gruntjs
  - 前端优化

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_imagemin"><span class="toc_number toc_depth_1">1</span> 安装 imagemin 插件</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">2</span> 配置压缩图片任务</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    Photoshop 切出的图片，含有多余信息，它们对网页前端并没有用处，反而增加图片大小，所以 Google Web Fundamentals 里建议我们<a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/image-optimization#tools-and-parameter-tuning">使用工具</a>压缩图片大小，减少用户下载的文件大小。
  </p>
  
  <p>
    如果你用 Grunt.js，我们就可以借助它的插件 <a href="https://github.com/gruntjs/grunt-contrib-imagemin">Grunt-contrib-imagemin</a> 来批量、无损压缩图片大小。
  </p>
  
  <p>
    如果你对 Grunt.js 不了解，可以看我上一篇<a href="http://www.zfanw.com/blog/gruntjs.html">简单介绍</a>。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_imagemin">安装 imagemin 插件</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_imagemin" href="#_imagemin"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    切换到项目文件夹，
  </p>
  
  <pre><code>cd projectName
npm install grunt-contrib-imagemin --save-dev
</code></pre>
  
  <h2 class="storycontent-h2">
    <span id="i">配置压缩图片任务</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    接下来配置 Gruntfile.js 文件，定义优化图片大小的任务：
  </p>
  
  <pre><code>/*global module:false*/
module.exports = function (grunt) {
  'use strict'
  grunt.initConfig({
    imagemin: {
      /* 压缩图片大小 */
      dist: {
        options: {
          optimizationLevel: 3 // 定义 PNG 图片优化水平
        },
        files: [{
          expand: true,
          cwd: 'img/',
          src: ['**/*.{png,jpg,jpeg}'], // 优化 img 目录下所有 png/jpg/jpeg 图片
          dest: 'img/' // 优化后的图片保存位置，覆盖旧图片，并且不作提示
        }]
      }
    },
  })
  grunt.loadNpmTasks('grunt-contrib-imagemin')
  grunt.registerTask('img', ['imagemin'])
}

</code></pre>
  
  <p>
    运行 <code>grunt imagemin</code> 命令：
  </p>
  
  <p>
    <a href="http://www.zfanw.com/blog/wp-content/uploads/2013/07/Screenshot-from-2013-07-20-135942.png"><img src="http://www.zfanw.com/blog/wp-content/uploads/2013/07/Screenshot-from-2013-07-20-135942.png" alt="Gruntjs 批量压缩图片大小" width="548" height="187" class="alignnone size-full wp-image-9672" srcset="https://www.zfanw.com/blog/wp-content/uploads/2013/07/Screenshot-from-2013-07-20-135942.png 548w, https://www.zfanw.com/blog/wp-content/uploads/2013/07/Screenshot-from-2013-07-20-135942-300x102.png 300w" sizes="(max-width: 548px) 100vw, 548px" /></a>
  </p>
  
  <p>
    上图可以看到，图片压缩的比率非常可观。之后再使用 <a href="https://developers.google.com/speed/pagespeed/insights">Google PageSpeed 工具</a>检测，就不再提醒我们压缩图片。
  </p>
</div>