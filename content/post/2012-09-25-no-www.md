---
title: NO WWW
author: 陈 三
layout: post
date: 2012-09-25T05:39:04+00:00
url: /no-www.html
views:
  - 755
dsq_thread_id:
  - 860746032
categories:
  - WordPress
tags:
  - 301
  - htaccess

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_no-www"><span class="toc_number toc_depth_1">1</span> 为什么要 no-www</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">2</span> 具体实践情况</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#no-www_301_www"><span class="toc_number toc_depth_1">3</span> no-www 301 重定向到 www</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#www_301_no-www"><span class="toc_number toc_depth_1">4</span> www 301 重定向到 no-www</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">5</span> 鸣谢</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    首先，这标题绝非我拒绝使用 WWW （互联网）的意思。只是在讲域名中不要加 www。另外，这也不是我的主张，只是看到互联网上有<a href="http://no-www.org/">这么个主张</a>，就介绍一下。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_no-www">为什么要 no-www</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_no-www" href="#_no-www"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    对普通互联网使用者来说，域名中 www 或 no-www 其实并无关系，只要能正常访问网站即可。但按 <a href="http://no-www.org/">No-WWW</a> 网站的说法，则 www 其实是多余的：
  </p>
  
  <blockquote>
    <p>
      默认情况下，所有流行的浏览器都默认 HTTP 协议。如此，浏览器就会在请求的 URL 地址前自动补上 ‘http://’，然后自动连接 HTTP 服务器上的 80 端口&#8230;&#8230;Web 服务器允许通过主域名访问页面，除非指定特殊子域名。
    </p>
    
    <p>
      简单说，使用 www 子域名根本是多余的，空耗费连接时间。
    </p>
  </blockquote>
  
  <p>
    当然，有说 no-www 的，肯定就有 <a href="http://www.yes-www.org/">yes-www</a> 的，理由也不少。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">具体实践情况</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    那么来看下具体实践的情况。
  </p>
  
  <p>
    这是 Quantcast 美国的 <a href="http://www.quantcast.com/top-sites">top sites</a> 数据。我抽取前 20 名来做个统计：
  </p>
  
  <table class="table table-striped table-hover table-bordered table-condensed">
    <tr>
      <th>
        no-www&nbsp;&rarr;&nbsp;www
      </th>
      
      <th>
        www&nbsp;&rarr;&nbsp;no-www
      </th>
      
      <th>
        未曾做重定向
      </th>
    </tr>
    
    <tr>
      <td>
        google.com
      </td>
      
      <td>
        twitter.com
      </td>
      
      <td>
        ask.com
      </td>
    </tr>
    
    <tr>
      <td>
        youtube.com
      </td>
      
      <td>
        vimeo.com
      </td>
      
      <td>
      </td>
    </tr>
    
    <tr>
      <td>
        facebook.com
      </td>
      
      <td>
        pinterest.com
      </td>
      
      <td>
      </td>
    </tr>
    
    <tr>
      <td>
        msn.com
      </td>
      
      <td>
        wordpress.org
      </td>
      
      <td>
      </td>
    </tr>
    
    <tr>
      <td>
        yahoo.com
      </td>
      
      <td>
      </td>
      
      <td>
      </td>
    </tr>
    
    <tr>
      <td>
        amazon.com
      </td>
      
      <td>
      </td>
      
      <td>
      </td>
    </tr>
    
    <tr>
      <td>
        wikipedia.org
      </td>
      
      <td>
      </td>
      
      <td>
      </td>
    </tr>
    
    <tr>
      <td>
        ebay.com
      </td>
      
      <td>
      </td>
      
      <td>
      </td>
    </tr>
    
    <tr>
      <td>
        microsoft.com
      </td>
      
      <td>
      </td>
      
      <td>
      </td>
    </tr>
    
    <tr>
      <td>
        huffingtonpost.com
      </td>
      
      <td>
      </td>
      
      <td>
      </td>
    </tr>
    
    <tr>
      <td>
        bing.com
      </td>
      
      <td>
      </td>
      
      <td>
      </td>
    </tr>
    
    <tr>
      <td>
        ehow.com
      </td>
      
      <td>
      </td>
      
      <td>
      </td>
    </tr>
    
    <tr>
      <td>
        blogspot.com
      </td>
      
      <td>
      </td>
      
      <td>
      </td>
    </tr>
    
    <tr>
      <td>
        answers.com
      </td>
      
      <td>
      </td>
      
      <td>
      </td>
    </tr>
    
    <tr>
      <td>
        blogger.com
      </td>
      
      <td>
      </td>
      
      <td>
      </td>
    </tr>
  </table>
  
  <p>
    可以看到，除了 ask 不曾统一网址外，所有其他网站均做了网址的重定向，或 no-www 重定向到 www，或 www 重定向到 no-www。
  </p>
  
  <p>
    其实按我理解，则重定向网址的需求更多不是因为 no-www 或 yes-www 提出的理由，而是出于<a href="http://www.mattcutts.com/blog/seo-advice-url-canonicalization/">讨好搜索引擎的需要</a>。
  </p>
  
  <p>
    举我的博客为例，如果不做重定向，则以下网址访问的内容其实是一致的：
  </p>
  
  <ol>
    <li>
      http://www.zfanw.com/blog
    </li>
    <li>
      http://zfanw.com/blog
    </li>
  </ol>
  
  <p>
    用户可能不关心它是有 www 还是没有，但搜索引擎会注意到这点。具体可以看 Google 网站工具上“<a href="http://support.google.com/webmasters/bin/answer.py?hl=zh-Hans&hlrm=en&answer=139066">规范化</a>&#8220;的说明。
  </p>
  
  <p>
    那么如何实现 no-www 到 www 或是 www 到 no-www 的 301 重定向？简单的办法是通过 .htaccess 文件设置。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="no-www_301_www">no-www 301 重定向到 www</span><a title="标题链接地址" class="u-floatRight hidden" id="heyno-www_301_www" href="#no-www_301_www"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    在 .htaccess 文件中加入以下代码：
  </p>
  
  <pre><code>#####301 跳转所有 no-www 到 www
RewriteEngine On
RewriteCond %{HTTP_HOST} ^[^.]+\.[^.]+$ [NC]
RewriteRule ^(.*)$ http://www.%{http_host}/$1 [R=301,NC]
</code></pre>
  
  <p>
    这样，输入网址 http://zfanw.com/blog 就会跳转到网址 http://www.zfanw.com/blog
  </p>
  
  <h2 class="storycontent-h2">
    <span id="www_301_no-www">www 301 重定向到 no-www</span><a title="标题链接地址" class="u-floatRight hidden" id="heywww_301_no-www" href="#www_301_no-www"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    类似的，在 .htaccess 文件加入如下代码：
  </p>
  
  <pre><code>#####301 跳转所有 www 到 no-www
RewriteEngine On
RewriteCond %{HTTP_HOST} ^www\.(.+)$ [NC]
RewriteRule ^(.*)$ http://%1/$1 [R=301,L] 
</code></pre>
  
  <p>
    这样，输入网址 http://www.zfanw.com/blog 就会跳转到网址 http://zfanw.com/blog
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">鸣谢</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <a href="http://wiki.apache.org/httpd/CanonicalHostNames">apache wiki</a>
    </li>
  </ol>
</div>