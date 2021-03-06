---
title: Web 前端优化 – 缓存页面组件
author: 陈 三
layout: post
date: 2012-10-31T06:28:08+00:00
url: /caching-in-http.html
views:
  - 952
dsq_thread_id:
  - 908014507
categories:
  - WordPress
  - 前端开发
tags:
  - 前端优化

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 设置方法</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 参考</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    在 Web 前端优化里，缓存页面组件是很重要的一项。不常改动的图片、CSS 、JavaScript 文件等，可以缓存在浏览器中，这样，用户再次访问时，浏览器直接从缓存中读取文件，一来减少浏览器请求数，加快用户访问速度，二来服务器需要返回的内容少了，减轻服务器负担。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">设置方法</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    缓存页面组件的方法有多种，这一种是修改 HTTP 头。
  </p>
  
  <p>
    假设服务器是 Apache，可以通过配置 .htaccess 文件来启用缓存：
  </p>
  
  <pre><code>&lt;IfModule mod_expires.c&gt;
    # 启用缓存
    ExpiresActive On

    #默认缓存时间为 1 天
    ExpiresDefault "access plus 1 day"

    #图片的缓存时间设置为一周
    ExpiresByType image/x-icon "access plus 7 days"
    ExpiresByType image/jpeg "access plus 7 days"
    ExpiresByType image/png "access plus 7 days"
    ExpiresByType image/gif "access plus 7 days"


    ExpiresByType application/x-shockwave-flash "access plus 7 days"

    #CSS 的缓存时间也设置成一周
    ExpiresByType text/css "access plus 7 day"

    #Javascript 的缓存时间同样设置为一周
    ExpiresByType text/javascript "access plus 7 day"
    ExpiresByType application/x-javascript "access plus 7 day"


    ExpiresByType text/html "access plus 10 minutes"
    ExpiresByType application/xhtml+xml "access plus 10 minutes"
&lt;/IfModule&gt;
&lt;IfModule mod_headers.c&gt;
    #设置代理缓存
  &lt;FilesMatch "\.(js|css|xml|gz|html)$"&gt;
    Header append Vary: Accept-Encoding
  &lt;/FilesMatch&gt;
&lt;/IfModule&gt;
</code></pre>
  
  <p>
    以上配置针对<a href="http://en.wikipedia.org/wiki/Internet_media_type">不同类型文件</a>设置不同有效期限，比如 jpeg/png/gif 图片，从用户第一次访问算起，7 天内有效，如果用户在 7 天内还访问这个网站，则直接从浏览器缓存中读取该图片，无需服务器上再返回。
  </p>
  
  <p>
    打开 firebug，启用 Net 面板，刷新页面，如果看到有返回状态码 304 Not Modified 的文件，说明设置成功。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">参考</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html">w3 &#8211; caching in http</a>
    </li>
    <li>
      <a href="http://www.mnot.net/cache_docs/">cache docs</a>
    </li>
    <li>
      <a href="http://httpd.apache.org/docs/2.2/mod/mod_expires.html">Apache mod_expires</a>
    </li>
    <li>
      <a href="http://httpd.apache.org/docs/current/mod/mod_headers.html#header">Apache mod_headers</a>
    </li>
  </ol>
</div>