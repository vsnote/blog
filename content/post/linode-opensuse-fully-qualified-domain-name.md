---
title: Linode 下 openSUSE 系统 FQDN 设置
author: 陈 三
layout: post
date: 2014-10-24T12:54:59+00:00
url: /linode-opensuse-fully-qualified-domain-name.html
views:
  - 677
categories:
  - openSUSE
tags:
  - fqdn
  - Linode
  - openSUSE
  - vps

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_hostname"><span class="toc_number toc_depth_1">1</span> 设置 hostname</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_FQDN"><span class="toc_number toc_depth_1">2</span> 设置 FQDN</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    Ubuntu 的势力已经大到超出我想象，所以 <a href="https://www.linode.com/docs/getting-started#update-etchosts">Linode 教程</a>中没有提及 openSUSE 下的情况也就没觉得奇怪。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_hostname">设置 hostname</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_hostname" href="#_hostname"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    其实我也好奇，为什么 VPS 需要设置 hostname。估计是为了好看，或者可移植性。譬如未设置前，<code>hostname -v</code> 显示的是 li-memeberxxx 之类的，设置后，主机名显得个性化了，另外换服务器的话，主机名不会变化 &#8211; 这只是我的揣测。
  </p>
  
  <p>
    openSUSE 下设置 hostname，跟 linode 教程中的 Ubuntu 部分略近：
  </p>
  
  <ol>
    <li>
      <code>sudo vi /etc/hostname</code> &#8211; 创建一个 hostname 文件，在其中输入 <code>orchid</code>，这个名称随你写，你爱什么写什么
    </li>
    <li>
      <code>hostname -F /etc/hostname</code> &#8211; 设定 hostname，名称为 /etc/hostname 文件内容
    </li>
  </ol>
  
  <p>
    再查看 <code>hostname -v</code> 结果，已经变成 <code>orchid</code>。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_FQDN">设置 FQDN</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_FQDN" href="#_FQDN"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    <a href="http://en.wikipedia.org/wiki/Fully_qualified_domain_name">FQDN</a> 的全称是 &#8220;fully qualified domain name&#8221;，为什么要设置它？又是一个诡异的问题。且不管它。
  </p>
  
  <p>
    <code>sudo vi /etc/hosts</code> 打开 hosts 文件，添加一行：
  </p>
  
  <pre><code>12.34.56.78 orchid.zfanw.com orchid
</code></pre>
  
  <p>
    第一部分即你的服务器 IP 地址，第二部分即是 FQDN 了，第三部分是前面设置的 hostname。
  </p>
  
  <p>
    注意，<code>orchid.zfanw.com</code> 需要做域名解析，A 记录绑定到服务器 IP &#8211; 这样主机外部访问时就可以解析到。
  </p>
  
  <p>
    之后再执行 <code>hostname -f</code> 查看 FQDN 值，输出的是：
  </p>
  
  <pre><code>orchid.zfanw.com
</code></pre>
  
  <p>
    有时会需要重启 Apache 服务，则执行如下命令：
  </p>
  
  <pre><code>sudo rcapache2 restart
</code></pre>
  
  <p>
    最后，当然是贴一下我的<a href="https://www.linode.com/?r=c1160d4e51485f11b9ae6b4cf286ebf455f87613">推广链接</a>。我不太记得好处是什么，大致是你从这链接点击注册使用 3 个月以上，我得到一定的返现，这返现足够我吃十顿快餐吧。
  </p>
  
  <p>
    附：<a href="http://www.zfanw.com/blog/linode-fqdn-hostname.html">Linode FQDN 设置 – 陈三</a>
  </p>
</div>