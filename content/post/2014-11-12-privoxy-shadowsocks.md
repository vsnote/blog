---
title: Privoxy shadowsocks
author: 陈 三
layout: post
date: 2014-11-12T05:37:33+00:00
excerpt: Privoxy 转发到 shadowsocks
url: /privoxy-shadowsocks.html
views:
  - 4070
categories:
  - openSUSE
tags:
  - Privoxy
  - shadowsocks

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_shadowsocks"><span class="toc_number toc_depth_1">1</span> 服务器端安装 shadowsocks</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_shadowsocks-2"><span class="toc_number toc_depth_1">2</span> 本地安装 shadowsocks</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#Privoxy"><span class="toc_number toc_depth_1">3</span> Privoxy 转发</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    <a href="https://github.com/clowwindy/shadowsocks">shadowsocks</a> 是一个 SOCKS5 代理，所以，它的用法跟 SSH 搭建 SOCKS 代理服务器差不多。至于谁好谁坏，谁快谁慢，环境不一样，我觉得很难有固定标准，所以还是靠自己的感受判断。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_shadowsocks">服务器端安装 shadowsocks</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_shadowsocks" href="#_shadowsocks"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    首先根据 <a href="https://github.com/clowwindy/shadowsocks/wiki/Shadowsocks-使用说明">shadownsocks 安装说明</a> 在服务器（比如 VPS）上安装 shadowsocks 并配置、启用。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_shadowsocks-2">本地安装 shadowsocks</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_shadowsocks-2" href="#_shadowsocks-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    在本机上，我们还需要一个 shadowsocks 客户端。通常照服务器端一样安装，安装后 shadowsocks 提供有 <code>sslocal</code> 命令。
  </p>
  
  <p>
    以我的 openSUSE 13.2 为例，安装完 <a href="https://github.com/madeye/shadowsocks-libev">shadowsocks-libev</a>，根据服务器端的配置修改 <em>/etc/shadowsocks/shadowsocks-libev-config.json</em> 文件，然后执行 <code>ss-local</code> 命令（注意，libev 版本的命令比其他版本的 shadowsocks 命令多出中间一个连字符）：
  </p>
  
  <pre><code>ss-local -c /etc/shadowsocks/shadowsocks-libev-config.json
</code></pre>
  
  <p>
    运行的结果如下：
  </p>
  
  <blockquote>
    <p>
      2014-11-12 09:49:44 INFO: initialize ciphers&#8230; aes-256-cfb
    </p>
    
    <p>
      2014-11-12 09:49:44 INFO: server listening at port 1080.
    </p>
  </blockquote>
  
  <p>
    说明本地 shadowsocks 服务器已经在 127.0.0.1:1080 上监听。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="Privoxy">Privoxy 转发</span><a title="标题链接地址" class="u-floatRight hidden" id="heyPrivoxy" href="#Privoxy"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    接下来就是把 Privoxy 的流量转发到本机的 1080 端口。
  </p>
  
  <p>
    打开 Privoxy 的 <em>config</em> 文件，添加如下规则：
  </p>
  
  <pre><code>forward-socks5 / 127.0.0.1:1080 .
</code></pre>
  
  <p>
    规则的具体意义见 <a href="http://www.zfanw.com/blog/privoxy-forward-ssh.html">SSH 搭建 SOCKS 代理服务器</a>一篇。
  </p>
</div>