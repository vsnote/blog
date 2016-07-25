---
title: Privoxy 转发 SSH
author: 陈 三
layout: post
date: 2014-11-10T05:43:44+00:00
url: /privoxy-forward-ssh.html
views:
  - 1662
categories:
  - openSUSE
tags:
  - Privoxy
  - ssh

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_socks"><span class="toc_number toc_depth_1">1</span> 搭建 socks 代理服务器</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_Privoxy"><span class="toc_number toc_depth_1">2</span> 配置 Privoxy 转发</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    前一阵子，有人在我博客<a href="http://www.zfanw.com/blog/privoxy-tutorial.html/comment-page-1#comment-6238">留言</a>，对我没有 Privoxy 转发需求表示“大吃一惊”。我倒是淡然地说，因为一直都在用 VPN，至今还算稳定，所以就没去想备用方案。
  </p>
  
  <p>
    后来想到我以前曾写过 <a href="http://www.zfanw.com/blog/ssh-firefox-sock-proxy-switch.html">SSH Firefox SOCKS 代理切换</a>一文，其实雏形已经有了，所以本文再略为修饰增补。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_socks">搭建 socks 代理服务器</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_socks" href="#_socks"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <pre><code>ssh -D 9999 -C zfanw@zfanw.com
</code></pre>
  
  <p>
    <code>D</code> 参数表示在本机 9999 端口创建一个 <a href="http://en.wikipedia.org/wiki/SOCKS">SOCKS 代理服务器</a>，并且通过 SSH 通道建立与远程服务器（zfanw.com 的主机）的安全连接。<code>C</code> 用于压缩传送数据，为可选参数。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Privoxy">配置 Privoxy 转发</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Privoxy" href="#_Privoxy"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    于是我们现在在本机上有两个代理服务器：
  </p>
  
  <ol>
    <li>
      SOCKS 代理服务器，端口为 9999
    </li>
    <li>
      Privoxy 的 HTTP 代理服务器，<a href="http://www.zfanw.com/blog/privoxy-tutorial.html#i">端口为 8118</a>
    </li>
  </ol>
  
  <p>
    接下来要做的，就是把 Privoxy 代理服务器的流量转发到 SOCKS 代理上。打开 Privoxy 的 <em>config</em> 文件，添加如下代码：
  </p>
  
  <pre><code>forward-socks5 / 127.0.0.1:9999 .
</code></pre>
  
  <p>
    <a href="http://www.privoxy.org/user-manual/config.html#SOCKS">其中</a> <em>forward-socks5</em> 表示转发目标是 SOCKS 服务器，<em>5</em> 是协议版本，<em>/</em> 表示转发所有 HTTP 请求，<em>127.0.0.1:9999</em> 即第一步中搭建的 SOCKS 代理服务器，最末的 <em>.</em> 表示经过 SOCKS 代理的请求不再过 HTTP 代理服务器。
  </p>
  
  <p>
    Privoxy 支持多个版本 SOCKS 转发协议。其中 forward-socks4 与 forward-socks4a 的区别是，后者 DNS 解析发生在 SOCKS 服务器上，前者则是在本地，forward-socks5 同样是在 SOCKS 服务器上。
  </p>
</div>