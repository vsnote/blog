---
title: Linode vps 安装配置 Ghost
author: 陈 三
layout: post
date: 2015-01-03T06:20:45+00:00
excerpt: VPS 里配置 apache 与 Ghost 博客程序
url: /linode-vps-install-ghost.html
views:
  - 903
categories:
  - 前端开发
tags:
  - Ghost
  - Linode
  - node.js
  - vps

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_Ghost"><span class="toc_number toc_depth_1">1</span> 安装 Ghost</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_Apache_Ghost"><span class="toc_number toc_depth_1">2</span> 配置 Apache 与 Ghost</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    我的 vps 情况：
  </p>
  
  <ul>
    <li>
      操作系统 &#8211; CentOS 7 64 位
    </li>
    <li>
      web 服务器软件 &#8211; Apache
    </li>
  </ul>
  
  <p>
    Ghost<fnref target="14873.1" /> 基于 Node.js，它本身自带 web 服务器，不需要 Apache。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Ghost">安装 Ghost</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Ghost" href="#_Ghost"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    主要参照 Ghost 官方帮助<fnref target="14873.2" />。
  </p>
  
  <ol>
    <li>
      <p>
        下载 Ghost
      </p>
      
      <pre><code>$ curl -L https://ghost.org/zip/ghost-latest.zip -o ghost.zip
</code></pre>
    </li>
    
    <li>
      <p>
        解压 Ghost
      </p>
      
      <pre><code>$ unzip -uo ghost.zip -d ghost
</code></pre>
    </li>
    
    <li>
      <p>
        安装 Ghost
      </p>
      
      <pre><code>$ cd ghost
$ npm install --production
</code></pre>
    </li>
    
    <li>
      <p>
        启动 Ghost
      </p>
      
      <pre><code>$ npm start --production
</code></pre>
    </li>
  </ol>
  
  <p>
    现在，你可以在 vps 上通过 <code>127.0.0.1:2368</code> 路径访问到 Ghost 博客了。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Apache_Ghost">配置 Apache 与 Ghost</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Apache_Ghost" href="#_Apache_Ghost"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    当然，你的目的可不是在 vps 上访问 Ghost，而是通过域名访问 Ghost。
  </p>
  
  <p>
    ghost 目录下有一个 <code>config.example.js</code> 文件，用于配置相关信息<fnref target="14873.3" />，比如域名，端口等。
  </p>
  
  <p>
    执行以下操作前，请先确保你在 DNS 服务器上把域名绑定到 vps 的 ip 地址。
  </p>
  
  <ol>
    <li>
      <p>
        复制一个 config.js
      </p>
      
      <pre><code>$ cd ghost
$ cp config.example.js config.js
</code></pre>
    </li>
    
    <li>
      <p>
        修改 config.js
      </p>
      
      <p>
        将 config.js 里 production 部分里的 <code>url: 'http://my-ghost-blog.com'</code> 改为 <code>url: 'http://example.com'</code>。
      </p>
    </li>
    
    <li>
      <p>
        重启 Ghost
      </p>
      
      <p>
        按 <kbd>Ctrl - C</kbd> 关闭 Ghost，再执行 <code>npm start --production</code> 启动它。
      </p>
      
      <p>
        这时你能看到如下信息：
      </p>
      
      <pre><code>Migrations: Up to date at version 003
Ghost is running... 
Your blog is now available on http://example.com 
Ctrl+C to shut down
</code></pre>
      
      <p>
        但这信息并不意味着我们能访问到 Ghost 了。因为 example.com 域名访问的是 80 端口，在这个端口上监听的是 Apache 而不是 Node.js &#8211; 它是在 2368 端口监听着。
      </p>
    </li>
  </ol>
  
  <p>
    所以我们还需要配置 Apache。
  </p>
  
  <p>
    打开 <code>/etc/httpd/conf.d/vhost.conf</code> 文件（CentOS 系统的情况），添加如下内容：
  </p>
  
  <pre><code> &lt;VirtualHost *:80&gt;
     ServerName www.frontbin.com
     ServerAlias frontbin.com
     ProxyPreserveHost on
     ProxyPass / http://localhost:2368/
     ProxyPassReverse / http://localhost:2368/
 &lt;/VirtualHost&gt;
</code></pre>
  
  <p>
    重启 apache：
  </p>
  
  <pre><code>$ sudo service httpd restart 
</code></pre>
  
  <p>
    这样，Apache 充当代理，会把它监听到的流量转发给 Node.js 监听的端口，这时访问 http://example.com，我们就能打开 Ghost 博客了。
  </p>
  
  <footnotes>
    <fn name="14873.1">
      <p>
        <a href="https://ghost.org/">Ghost &#8211; Just a blogging platform</a>
      </p>
    </fn>
    
    <fn name="14873.2">
      <p>
        <a href="http://support.ghost.org/installing-ghost-linux/">Installing Ghost on Linux &#8211; Ghost SupportGhost Support</a>
      </p>
    </fn>
    
    <fn name="14873.3">
      <p>
        <a href="http://support.ghost.org/config/">Configuring Ghost &#8211; Ghost SupportGhost Support</a>
      </p>
    </fn>
  </footnotes>
</div>