---
title: vimprobable2
author: 陈 三
layout: post
date: 2015-01-30T17:00:13+00:00
excerpt: 一个操作方式类似 vimperator 的浏览器，比 Firefox 更为轻便简洁
url: /vimprobable2.html
views:
  - 1052
categories:
  - openSUSE
tags:
  - vimperator

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 简介</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 安装</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-3"><span class="toc_number toc_depth_1">3</span> 配置</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-4"><span class="toc_number toc_depth_1">4</span> 问题</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    Vimprobable 的 <a href="http://sourceforge.net/p/vimprobable/wiki/FAQ/">FAQ</a> 里有一个问答是这样的：
  </p>
  
  <blockquote>
    <p>
      Why not just use Vimperator?
    </p>
    
    <p>
      Mozilla Firefox (and also its variants like Iceweasel) gets worse with every version. It behaves like a molasse by now.
    </p>
    
    <p>
      为什么不就用 Vimperator？
    </p>
    
    <p>
      Mozilla Firefox（包括它的变体，比如 Iceweasel），越做越糟。
    </p>
  </blockquote>
  
  <p>
    如果你是 vimperator 用户，估计也能体会到 vimprobable 开发者的这句话。每一次 Firefox 升级，vimperator 基本都会出些小问题，然后要等开发者修复，再自己编译、重新安装。但很多人是在 Windows 环境下使用，要跑个简单的 <code>make xpi</code> 命令估计都要先花时间折腾环境。
  </p>
  
  <p>
    所以，试试 vimprobable？
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">简介</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    vimprobable 基于 webkit，它是已经停止开发的 vimpression 的分支。它的键操作与 vimperator 很像，如果你用过 vimperator，则非常容易上手。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">安装</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    vimprobable 目前有两个版本，vimprobable1 与 vimprobable2，目前版本 1 只会打些小补丁，主要开发集中在版本 2。
  </p>
  
  <p>
    所以以下说明均指 vimprobable2。
  </p>
  
  <p>
    vimprobable 支持三种操作系统：
  </p>
  
  <ul>
    <li>
      BSD
    </li>
    <li>
      Mac
    </li>
    <li>
      Linux
    </li>
  </ul>
  
  <p>
    我是在 openSUSE 13.2 上安装使用。
  </p>
  
  <ol>
    <li>
      <p>
        下载源代码
      </p>
      
      <p>
        下载源代码有两种方式：
      </p>
      
      <ul>
        <li>
          下载<a href="http://sourceforge.net/projects/vimprobable/files/latest/download">压缩包</a>
        </li>
        <li>
          <code>git clone git://git.code.sf.net/p/vimprobable/code</code>
        </li>
      </ul>
    </li>
    
    <li>
      <p>
        安装 vimprobable
      </p>
      
      <ol>
        <li>
          <code>cd</code> 到代码目录中
        </li>
        <li>
          <code>sudo make install</code>
        </li>
      </ol>
      
      <p>
        注意 vimprobable 需要三个依赖：
      </p>
      
      <ul>
        <li>
          libwebkit-1.0 >= 1.1.11
        </li>
        <li>
          libgtk+-2.0
        </li>
        <li>
          libsoup-2.4
        </li>
      </ul>
    </li>
  </ol>
  
  <p>
    安装完成后，即可以通过命令行执行 vimprobable2 了。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-3">配置</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-3" href="#i-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    vimprobable2 的<a href="http://www.vimprobable.org/man/vimprobablerc.5.htm">配置</a>有以下几种方式，
  </p>
  
  <ol>
    <li>
      <code>make install</code> 前修改 <em>config.h</em> 及 <em>keymap.h</em> 文件
    </li>
    <li>
      通过 <code>:set</code> 命令临时修改
    </li>
    <li>
      通过指定 rc 配置文件，默认为 <em>~/.config/vimprobable/vimprobablerc</em>，这是永久的
    </li>
  </ol>
  
  <p>
    比如我们想改它的默认主页：
  </p>
  
  <pre><code>:set homepage=https://www.google.com
</code></pre>
  
  <p>
    有兴趣可以看看<a href="https://github.com/chenxsan/rc-files/blob/master/.config/vimprobable/vimprobablerc">我的配置文件</a>。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-4">问题</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-4" href="#i-4"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    我在使用过程中有碰到几个问题，
  </p>
  
  <ul>
    <li>
      <p>
        ssl 错误。
      </p>
      
      <p>
        这是在访问一些 https 网址时出现的：
      </p>
      
      <blockquote>
        <p>
          Unable to load page
        </p>
        
        <p>
          Problem occurred while loading the URL https://www.google.co.jp/?gfe_rd=cr&ei=AzXLVIvcFOv98wf4wYCQCw
        </p>
        
        <p>
          Unacceptable TLS certificate
        </p>
      </blockquote>
      
      <p>
        vimprobable 默认使用 <em>/etc/ssl/certs/ca-certificates.crt</em> 检查网站证书，而我的系统下该路径并没有文件，当然你可以自己指定路径，
      </p>
      
      <pre><code>:set cabundle=/path/to/file
</code></pre>
      
      <p>
        但我因为不确定要指向哪里，所以更宁愿简单粗野处理：
      </p>
      
      <pre><code>:set strictssl=false
</code></pre>
      
      <p>
        不过请注意这样可能带来中间人攻击的风险。
      </p>
    </li>
    
    <li>
      <p>
        <kbd>gi</kbd> 无法进入 Insert 模式
      </p>
      
      <p>
        这是 vimprobable 使用 GTK 绑定或某些网站使用不规范的 HTML 元素的缘故，暂时无法避免。
      </p>
    </li>
    
    <li>
      <p>
        使用代理
      </p>
      
      <p>
        我的电脑上安装有 <a href="http://www.zfanw.com/blog/tag/privoxy">Privoxy</a>，vimprobable 也支持开启 proxy，但它是根据 <code>http_proxy</code> 这个环境变量来走的，所以我在 .zshrc 文件中添加如下一行：
      </p>
      
      <pre><code>alias vimpr='export HTTP_PROXY="127.0.0.1:8118"; vimprobable2'
</code></pre>
      
      <p>
        这样我不必修改整个系统的代理设置，只需要在运行 vimprobable2 前对当前会话配置即可。
      </p>
    </li>
  </ul>
</div>