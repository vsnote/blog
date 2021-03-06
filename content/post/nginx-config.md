---
title: openSUSE 安装配置 NGINX
author: 陈 三
layout: post
date: 2013-10-22T14:13:28+00:00
excerpt: 如何用 nginx 搭建一个简易的 Web 服务器。
url: /nginx-config.html
views:
  - 732
categories:
  - openSUSE
  - 前端开发
tags:
  - nginx
  - openSUSE

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 环境</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_nginx"><span class="toc_number toc_depth_1">2</span> 安装 nginx</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_nginx-2"><span class="toc_number toc_depth_1">3</span> 启动 nginx</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_nginx-3"><span class="toc_number toc_depth_1">4</span> 配置 nginx</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    本来这篇是在 Ubuntu 下完成的，因为升级过程中出了点小差错，于是变成在 openSUSE 上完成。
  </p>
  
  <p>
    我的配置 Web 服务器，只要最简单的，不需要数据库，不需要 PHP 等。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">环境</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <p>
        openSUSE 12.3
      </p>
    </li>
    
    <li>
      <p>
        KDE
      </p>
    </li>
    
    <li>
      <p>
        Konsole + ZSH
      </p>
    </li>
  </ol>
  
  <h2 class="storycontent-h2">
    <span id="_nginx">安装 nginx</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_nginx" href="#_nginx"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <pre><code>cnf nginx
</code></pre>
  
  <p>
    <code>cnf</code> 命令会自动查找 nginx 命令，如果系统上还没安装，它会提示你安装哪个包：
  </p>
  
  <pre><code>sudo zypper install nginx
</code></pre>
  
  <h2 class="storycontent-h2">
    <span id="_nginx-2">启动 nginx</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_nginx-2" href="#_nginx-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    再使用 <code>cnf nginx</code> 检查的话，可以看到，nginx 可执行文件位于 <code>/usr/sbin/nginx</code> 位置，需要 root 权限才可以运行。
  </p>
  
  <pre><code>sudo /usr/sbin/nginx
</code></pre>
  
  <p>
    之后输入 root 密码。
  </p>
  
  <p>
    打开 <a href="http://localhost">localhost</a> 地址，页面显示：
  </p>
  
  <blockquote>
    <p>
      <strong>403 Forbidden</strong>
    </p>
    
    <p>
      nginx/1.2.9
    </p>
  </blockquote>
  
  <p>
    之所以返回 403 错误，是因为 localhost 默认的根目录(/srv/www/htdocs/)下不存在 index.html 文件。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_nginx-3">配置 nginx</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_nginx-3" href="#_nginx-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    如果尝试往 /srv/www/htdocs/ 目录下写入文件，就会发现，这个目录需要 root 权限才可以操作。我显然不想每次编辑 HTML/CSS/js 文件都需要加 sudo。
  </p>
  
  <p>
    打开 /etc/nginx/ 目录，编辑目录下的 nginx.conf 配置文件：
  </p>
  
  <pre><code>sudo vim nginx.conf
</code></pre>
  
  <p>
    查找 /srv/www/htdocs 字样，将其修改为其他目录，比如 /home/sam/front/htdocs。
  </p>
  
  <p>
    之后重启 nginx：
  </p>
  
  <pre><code>sudo /usr/sbin/nginx -s reload
</code></pre>
  
  <p>
    刷新 <a href="http://localhost">localhost</a>，如果还是显示 403，则说明配置成功。之后把我的前端文件夹放在其中即可。
  </p>
</div>