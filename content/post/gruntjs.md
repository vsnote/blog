---
title: Gruntjs
author: 陈 三
layout: post
date: 2013-07-12T15:15:00+00:00
url: /gruntjs.html
dsq_thread_id:
  - 1494463492
views:
  - 1596
categories:
  - 前端开发
tags:
  - grunt.js
  - JavaScript
  - 自动化

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_Gruntjs"><span class="toc_number toc_depth_1">1</span> 安装 Gruntjs</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_packagejson"><span class="toc_number toc_depth_1">2</span> 配置 package.json</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_Gruntfilejs"><span class="toc_number toc_depth_1">3</span> 配置 Gruntfile.js</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    在前端开发中，有很多琐碎要做，比如检查代码语法、压缩 CSS、最小化混淆 JavaScript 代码、优化图片大小等等，如果要一个个处理，会非常耗时，重要的是，会比较无聊。于是就出现 Grunt.js<fnref target="9479.1" /> 这样的工具，流程化、自动化处理这一系列前端需求。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Gruntjs">安装 Gruntjs</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Gruntjs" href="#_Gruntjs"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    首先需要安装 Node.js，因为 Grunt 及其插件通过 NPM 管理。
  </p>
  
  <p>
    安装完 Node.js 后，打开命令行窗口安装 grunt-cli 工具：
  </p>
  
  <pre><code>npm install -g grunt-cli
</code></pre>
  
  <p>
    如果在 Linux 系统下，一般还需要 <code>sudo</code> 权限。
  </p>
  
  <p>
    之后我们就可以在命令行下执行 <code>grunt</code> 命令了。
  </p>
  
  <p>
    但是如果要 Grunt 运转，还需配置两个文件，package.json 与 Gruntfile.js。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_packagejson">配置 package.json</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_packagejson" href="#_packagejson"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    package.json 文件结构如下：
  </p>
  
  <pre><code>{
  "name": "Hello",
  "version": "0.1.0",
  "devDependencies": {
    "grunt": "~0.4.1",
    "grunt-contrib-csslint": "~0.1.2",
    "grunt-contrib-jshint": "~0.6.0",
    "grunt-contrib-imagemin": "~0.1.4",
    "grunt-contrib-concat": "~0.1.3",
    "grunt-contrib-cssmin": "~0.6.1"
    "grunt-contrib-uglify": "~0.2.2",
    "grunt-contrib-watch": "~0.2.2",
  }
}
</code></pre>
  
  <p>
    它定义当前项目的许多信息，比如名称、版本、版权声明，当然还有当前项目依赖的 npm 模块。
  </p>
  
  <p>
    该文件有几种生成方法：
  </p>
  
  <ol>
    <li>
      <code>npm init</code> 命令，命令会问几个问题，我们只要回答或选择默认答案，就可以创建基本的 json 文件
    </li>
    <li>
      使用某些模板带的
    </li>
    <li>
      手写
    </li>
  </ol>
  
  <p>
    我通常更喜欢前端两种。
  </p>
  
  <p>
    不过第一种方法生成的 package.json 文件很简单，只能作为一个起步，在它的基础上依自己的需求再定义。比如，执行下面的命令就会在 package.json 文件的 devDependencies 部分增加 grunt-contrib-jshint 一项：
  </p>
  
  <pre><code>npm install grunt-contrib-jshint --save-dev
</code></pre>
  
  <p>
    第二种办法，比如使用 <code>grunt-init</code><fnref target="9479.2" /> 来搭脚手架，这样很多东西马上就可用，比较省事。
  </p>
  
  <p>
    在创建完 package.json 文件后，命令行中输入：
  </p>
  
  <pre><code>npm install
</code></pre>
  
  <p>
    会在当前目录下安装所有未安装的依赖模块。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Gruntfilejs">配置 Gruntfile.js</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Gruntfilejs" href="#_Gruntfilejs"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    在准备好需要的模块后，我们可以开始根据项目的需要来配置任务，这是 Gruntfile.js 起的作用：
  </p>
  
  <pre><code>module.exports = function(grunt) {

  // 针对当前项目的配置
  grunt.initConfig({
    pkg: grunt.file.readJSON('package.json'),// 从 package.json 文件读入数据
    uglify: { //定义任务做什么
      options: { // 这里，我们可以修改任务的许多行为
        banner: '/*! &lt;%= pkg.name %&gt; &lt;%= grunt.template.today("yyyy-mm-dd") %&gt; */\n'
      },
      build: {
        src: 'src/&lt;%= pkg.name %&gt;.js', // 定义要处理的文件位置
        dest: 'build/&lt;%= pkg.name %&gt;.min.js' //定义处理后的文件存放位置
      }
    }
  });

  // 加载插件 任务谁来做
  grunt.loadNpmTasks('grunt-contrib-uglify');

  // 注册一个默认任务
  grunt.registerTask('default', ['uglify']);

};
</code></pre>
  
  <p>
    Gruntfile.js 的结构还是蛮简单的。我们在其中定义任务（registerTask），这个任务由各个小任务（比如上面代码中的 uglify）组成，小任务里还可以细分出任务目标（比如 uglify 中的 build）。至于各个任务的执行，由相应插件完成，这就需要载入插件 （loadNpmTasks）。
  </p>
  
  <p>
    根据需求完成配置后，命令行下运行：
  </p>
  
  <pre><code>grunt
</code></pre>
  
  <p>
    就会执行默认任务。
  </p>
  
  <p>
    当然，我们也可以指定执行某个任务甚至目标：
  </p>
  
  <pre><code>grunt uglify:build
</code></pre>
  
  <footnotes>
    <fn name="9479.1">
      <p>
        <a href="http://gruntjs.com/">Grunt: The JavaScript Task Runner</a>
      </p>
    </fn>
    
    <fn name="9479.2">
      <p>
        <a href="http://gruntjs.com/project-scaffolding">Project Scaffolding &#8211; Grunt: The JavaScript Task Runner</a>
      </p>
    </fn>
  </footnotes>
</div>