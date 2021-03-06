---
title: jspm-server 自动刷新页面
author: 陈 三
layout: post
date: 2015-06-05T10:41:09+00:00
excerpt: 安装、使用 jspm-server
url: /jspm-live-reload.html
views:
  - 1118
categories:
  - 前端开发
tags:
  - jspm

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#jspm-server"><span class="toc_number toc_depth_1">1</span> jspm-server 用法</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">2</span> 热重载</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    我在 <a href="http://www.zfanw.com/blog/jspm-systemjs.html" title="jspm 用法">JSPM 环境下开发</a>时，页面修改由 <a href="http://www.browsersync.io/" title="访问 Browsersync 官网">Browsersync</a> 监控并自动刷新：
  </p>
  
  <pre><code>browser-sync start --server --files '*.html, style/**, script/**'
</code></pre>
  
  <p>
    BrowserSync 的好处是，如果多个浏览器中测试同一个页面地址，则页面修改会同步到多个浏览器中。
  </p>
  
  <p>
    后来想，gulp.js、webpack、grunt.js 等都内置了自动刷新页面的功能，jspm 或许也会有。找了资料，没有，但有个 <a href="https://github.com/geelen/jspm-server" title="访问 Github 上 jspm-server 库">jspm-server</a>，这是 <a href="https://github.com/tapio/live-server" title="访问 Github 上 live-server 库">live-server</a> 的一个分支，针对 jspm 做了处理。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="jspm-server">jspm-server 用法</span><a title="标题链接地址" class="u-floatRight hidden" id="heyjspm-server" href="#jspm-server"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <p>
        全局安装 jspm-server
      </p>
      
      <pre><code>npm install -g jspm-server
</code></pre>
    </li>
    
    <li>
      <p>
        启动 jspm-server
      </p>
      
      <p>
        切换到项目目录，执行：
      </p>
      
      <pre><code>jspm-server
</code></pre>
      
      <p>
        默认开启的地址是 <code>http://127.0.0.1:8080/</code>，我们可以通过 <code>--port</code> 参数指定端口：
      </p>
      
      <pre><code>jspm-server --port=9999
</code></pre>
    </li>
  </ol>
  
  <p>
    与 Browsersync 类似，jspm-server 在 v0.1.6 版本后，同样可以同步刷新多个浏览器中打开的页面。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">热重载</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    如果你开发过 react，就会发现，它的大小模块非常多，如果每次修改一个小模块，就要整个页面重载 &#8211; 加载上百个小模块的话，则至少需要 1、2 秒的时间，这会降低我们的开发效率。所以 react 社区里出了一个 <a href="https://github.com/gaearon/react-hot-loader" title="react hot loader github 库">react-hot-loader</a>，可以只重载我们修改过的模块 &#8211; 即热重载，大幅提高我们的开发效率。
  </p>
  
  <p>
    jspm-server 同样具备热重载的功能，条件有二：
  </p>
  
  <ol>
    <li>
      在 index.html 中设置 <code>System.trace = true;</code>，当然，也可以在 config.js 文件中配置
    </li>
    <li>
      在能够热重载的 ES6 模块中添加 <code>export let __hotReload = true</code>
    </li>
  </ol>
  
  <p>
    关于第二步，可以借助浏览器的开发者工具，我的经验，有关联的模块都需要增加该语句。另外，CSS 文件默认能够自动热重载，不需要我们额外处理。
  </p>
  
  <p>
    效果见下图：
  </p>
  
  <p>
    [resp_image id=&#8217;16987&#8242; caption=&#8221; ]
  </p>
</div>