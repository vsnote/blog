---
title: Github Pages 自定义域名
author: 陈 三
layout: post
date: 2014-11-16T05:27:43+00:00
url: /github-pages-custom-domain.html
views:
  - 1972
categories:
  - 前端开发
tags:
  - Github

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_CNAME"><span class="toc_number toc_depth_1">1</span> 创建 CNAME 文件</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_CNAME-2"><span class="toc_number toc_depth_1">2</span> 添加 CNAME 记录</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_A"><span class="toc_number toc_depth_1">3</span> 添加 A 记录</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    我最近挖的一个坑，托管在 Github 库上，库地址是 https://github.com/chenxsan/linuxcoo。未设定自定义域名的话，可以通过 <a href="http://chenxsan.github.io/linuxcoo/">http://chenxsan.github.io/linuxcoo/</a> 访问。
  </p>
  
  <p>
    现在，我要给它添加一个自定义域名 <a href="http://www.linuxcoo.com" title="Linux Coo - Linux 命令集合">www.linuxcoo.com</a>。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_CNAME">创建 CNAME 文件</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_CNAME" href="#_CNAME"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    首先，在库的 <em>gh-pages</em> 分支根目录下创建 <a href="https://help.github.com/articles/adding-a-cname-file-to-your-repository/"><em>CNAME</em></a> 文件，写入：
  </p>
  
  <pre><code>www.linuxcoo.com
</code></pre>
  
  <p>
    注意以下几点：
  </p>
  
  <ul>
    <li>
      CNAME 文件名大写
    </li>
    <li>
      域名前不需要添加 http 这样的协议
    </li>
    <li>
      这里使用 www 子域名而不是顶级的 linuxcoo.com，Github 推荐使用子域名
    </li>
    <li>
      如果域名 &#8216;linuxcoo.com&#8217; 同样指向这个库的话，Github Pages 会自动将其重定向到 &#8216;www.linuxcoo.com&#8217; 上
    </li>
  </ul>
  
  <h2 class="storycontent-h2">
    <span id="_CNAME-2">添加 CNAME 记录</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_CNAME-2" href="#_CNAME-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    DNS 中添加一条 CNAME 记录，将 <em>www</em> 指向 <em>chenxsan.github.io</em>。
  </p>
  
  <p>
    之后检查 DNS 设置的情况：
  </p>
  
  <pre><code>$ dig www.linuxcoo.com +nostats +nocomments +nocmd

; &lt;&lt;&gt;&gt; DiG 9.9.5-rpz2+rl.14038.05-P1 &lt;&lt;&gt;&gt; www.linuxcoo.com +nostats +nocomments +nocmd
;; global options: +cmd
;www.linuxcoo.com.              IN      A
www.linuxcoo.com.       3599    IN      CNAME   chenxsan.github.io.
chenxsan.github.io.     3599    IN      CNAME   github.map.fastly.net.
github.map.fastly.net.  14      IN      A       103.245.222.133
</code></pre>
  
  <p>
    一切正常。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_A">添加 A 记录</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_A" href="#_A"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    上面的 CNAME 记录只是将 www.linuxcoo.com 指向 Github 服务器，此时访问 linuxcoo.com 域名，会返回 404 错误，所以还需要在 DNS 中添加两条 A 记录指向 Github Pages 的两个 IP（更好的办法是添加 <a href="http://support.dnsimple.com/articles/alias-record/">ALIAS</a>，但 Google Domains 并不支持）：
  </p>
  
  <ol>
    <li>
      192.30.252.153
    </li>
    <li>
      192.30.252.154
    </li>
  </ol>
  
  <p>
    再使用 <code>dig</code> 命令检查 DNS 状况：
  </p>
  
  <pre><code>$ dig linuxcoo.com

; &lt;&lt;&gt;&gt; DiG 9.9.5-rpz2+rl.14038.05-P1 &lt;&lt;&gt;&gt; linuxcoo.com
;; global options: +cmd
;; Got answer:
;; -&gt;&gt;HEADER&lt;&lt;- opcode: QUERY, status: NOERROR, id: 56008
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;linuxcoo.com.                  IN      A

;; ANSWER SECTION:
linuxcoo.com.           3599    IN      A       192.30.252.153
linuxcoo.com.           3599    IN      A       192.30.252.154

;; Query time: 588 msec
;; SERVER: 8.8.8.8#53(8.8.8.8)
;; WHEN: Fri Nov 14 22:27:00 CST 2014
;; MSG SIZE  rcvd: 73
</code></pre>
  
  <p>
    这时再访问 linuxcoo.com 域名，已经能正常打开，并且因为第一步中的设置，Github 会帮我们重定向到 www 上。
  </p>
</div>