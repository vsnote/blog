---
title: Privoxy 简明教程
author: 陈 三
layout: post
date: 2014-09-24T14:29:34+00:00
excerpt: 教你如何安装、配置、使用 Privoxy。
url: /privoxy-tutorial.html
views:
  - 9555
categories:
  - openSUSE
  - 未分类
tags:
  - Privoxy

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#Privoxy"><span class="toc_number toc_depth_1">1</span> Privoxy 用途</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#Privoxy-2"><span class="toc_number toc_depth_1">2</span> Privoxy 安装</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_Privoxy"><span class="toc_number toc_depth_1">3</span> 启动 Privoxy</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">4</span> 配置浏览器</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_Privoxy-2"><span class="toc_number toc_depth_1">5</span> 设置 Privoxy</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    我估计八成人第一遍看 <a href="http://www.privoxy.org/3.0.21/user-manual/index.html">Privoxy 手册</a>，只一头雾水。
  </p>
  
  <p>
    我此前写过<a href="http://www.zfanw.com/blog/tag/privoxy">两篇</a>相关教程，介绍 Privoxy 中屏蔽网页广告、视频广告的用法，较为具体。这里概括性地写一篇简明教程。所谓「站得高，看得远」，一旦对 Privoxy 整体结构有把握，自然胸有成竹，做得到有的放矢地查阅手册，而不是一头栽进茫茫的配置项中。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="Privoxy">Privoxy 用途</span><a title="标题链接地址" class="u-floatRight hidden" id="heyPrivoxy" href="#Privoxy"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Privoxy 是一个代理软件，代理 &#8211; 简单说，就是进出你电脑的流量的中介。借由它，我们可以控制出去的请求、返回的响应。不必要的请求 &#8211; 比如视频广告的地址、图片广告的地址，我们可以直接 <code>block</code> 掉；不必要的响应内容 &#8211; 比如页面中的文字广告，我们可以借由 <code>filter</code> 过滤掉，不让其显示。
  </p>
  
  <p>
    当然，上面只是 Privoxy 最常见、最普通的用法，Privoxy 还有其它用法，这里且按下。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="Privoxy-2">Privoxy 安装</span><a title="标题链接地址" class="u-floatRight hidden" id="heyPrivoxy-2" href="#Privoxy-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Privoxy 支持的平台非常多：
  </p>
  
  <blockquote>
    <p>
      Windows 95 and later versions (98, ME, 2000, XP, Vista, Windows 7 etc.), GNU/Linux (RedHat, SuSE, Debian, Fedora, Gentoo, Slackware and others), Mac OS X (10.4 and upwards on PPC and Intel processors), OS/2, Haiku, DragonFly, FreeBSD, NetBSD, OpenBSD, Solaris, and various other flavors of Unix.
    </p>
  </blockquote>
  
  <p>
    Windows 平台的安装自不用说，下载一个 exe 文件一路点击下一步；Linux 平台多数可以通过仓库安装。
  </p>
  
  <p>
    比如 Ubuntu：
  </p>
  
  <pre><code>sudo apt-get install privoxy
</code></pre>
  
  <p>
    又比如 openSUSE：
  </p>
  
  <pre><code>sudo zypper install privoxy
</code></pre>
  
  <p>
    一般也建议使用仓库安装。
  </p>
  
  <p>
    或者你实在愿意折腾，那就下载<a href="http://sourceforge.net/projects/ijbswa/files/Sources/">源代码</a>自己编译安装。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Privoxy">启动 Privoxy</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Privoxy" href="#_Privoxy"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    安装完 Privoxy 后，需要启动它，因为各平台下的各个系统情况不一，这里就不一一介绍，请看<a href="http://www.privoxy.org/user-manual/startup.html">手册说明</a>。
  </p>
  
  <p>
    openSUSE 下按 <kbd>Alt + F1</kbd> 搜索并打开 <em>Service Manager</em>，查找 privoxy 项，启用并启动它，Privoxy 就会以系统服务的形态运行。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">配置浏览器</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    大部分时候，我们可能只需要浏览器走 Privoxy 代理，则打开浏览器的代理设置，将 HTTP 与 SSL 代理设置为 <code>127.0.0.1</code>，端口为 8118。
  </p>
  
  <p>
    如果想省事，也可以配置系统代理。
  </p>
  
  <p>
    配置完浏览器后，在浏览器中打开 <a href="http://p.p">http://p.p</a> 网址，看是否显示如下内容：
  </p>
  
  <blockquote>
    <p>
      This is Privoxy 3.0.21 on unknown (127.0.0.1), port 8118, enabled
    </p>
  </blockquote>
  
  <p>
    如果有，说明 Privoxy 正常运行且浏览器配置正确。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Privoxy-2">设置 Privoxy</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Privoxy-2" href="#_Privoxy-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    以上准备就绪后，可以开始定制我们的 Privoxy 了。
  </p>
  
  <p>
    一切从 config 文件说起。
  </p>
  
  <p>
    config 文件在各种系统下位置、名称可能并不一样，比如 Windows 系统下，它其实叫 config.txt，在 openSUSE 系统下，它所在的目录为 <em>/etc/privoxy</em>，这个目录是个软链接，指向 <em>/var/lib/privoxy/etc</em>。
  </p>
  
  <p>
    但通常，我们并不需要修改 config 文件，这里且让它默认着。
  </p>
  
  <p>
    再来介绍两类文件：
  </p>
  
  <ol>
    <li>
      action 文件 <ol>
        <li>
          match-all.action
        </li>
        <li>
          default.action
        </li>
        <li>
          user.action
        </li>
      </ol>
    </li>
    
    <li>
      filter 文件 <ol>
        <li>
          default.filter
        </li>
        <li>
          user.filter
        </li>
      </ol>
    </li>
  </ol>
  
  <p>
    match-all.action、default.action、default.filter 这几个文件，建议不要做修改，因为 Privoxy 升级时会覆盖掉。所以把我们的配置内容写到 user.action 及 user.filter 中 &#8211; 这也是为什么两个文件叫 user.* 的缘故。
  </p>
  
  <h3>
    action 文件
  </h3>
  
  <p>
    action 文件定义 Privoxy 的动作，比如 <code>{+block}</code>：
  </p>
  
  <pre><code>{+block{干掉陈三的 blog}}
.zfanw.com
</code></pre>
  
  <p>
    这一句，把我的网址挡掉，凡是 zfanw.com 的请求，均会返回 403 &#8211; Privoxy 直接返回一个被 blocked 的提示页面，内容大概如下：
  </p>
  
  <blockquote>
    <p>
      Your request for http://www.zfanw.com/blog/ was blocked. Block reason: .zfanw.com
    </p>
  </blockquote>
  
  <p>
    分析下代码的意义：
  </p>
  
  <ol>
    <li>
      第一行，<code>{+block}</code> 是一个指令，<code>block</code>后的 <code>{}</code> 写的是要 block 的原因，不写也可以，作用类似于注释。
    </li>
    <li>
      第二行， <code>.zfanw.com</code>，这是一个上述指令要应用的网址，分两个部分，一个 domain，一个 path，domain 部分支持部分通配符，比如 <code>*</code>、<code>?</code>、<code>[0-9]</code>、<code>[a-z]</code>；path 部分是指第一个 <code>/</code> 后的部分网址，支持 POSIX 1003.2 正则表达式，比 domain 部分灵活。具体见<a href="http://www.privoxy.org/user-manual/actions-file.html">手册</a>。
    </li>
  </ol>
  
  <h3>
    filter 文件
  </h3>
  
  <p>
    filter 文件定义过滤<strong>响应</strong>的规则，比如：
  </p>
  
  <pre><code>FILTER: blockBaiduAd 去除百度推广广告
s|&lt;/head&gt;|&lt;style type=text/css&gt;\#content_left&gt;table,[id*='00'],\#ec_im_container,\#ec_im_container+div,.ad-block,.EC_zwd_table{display: none !important;}&lt;/style&gt;&lt;/head&gt;|g
s|&lt;/body&gt;&lt;script.*&lt;/script&gt;&lt;/html&gt;|&lt;/body&gt;&lt;/html&gt;|g
</code></pre>
  
  <p>
    第一行中，大写的 <code>FILTER</code> 表示定义一个过滤规则，<code>blockBaiduAd</code> 表示规则名称，再后面是说明。
  </p>
  
  <p>
    第二行及第三行，是对返回的页面进行修改。比如你用过 Vi/Vim 或 sed 等工具，应该对 <code>s</code> 这个替换命令很熟悉。简单说，上面的语句就是把页面内的代码作过更换，这样一些文字广告就不在浏览器中显示了。
  </p>
  
  <p>
    但是，user.filter 中只是定义过滤的规则，规则的应用，还是要在 action 文件中，所以以上规则写到 user.action 中，如下：
  </p>
  
  <pre><code># 清理百度推广广告
{+filter{blockBaiduAd}}
.baidu.com
</code></pre>
  
  <p>
    我想看过 action 文件配置结构的话，就已经知道这一句是什么意思：<code>#</code> 后是一个注释，<code>filter</code> 是指令，要求执行 <code>blockBaiduAd</code> 这条规则，<code>.baidu.com</code> 是应用到的网址。
  </p>
  
  <p>
    在整个使用过程中，要多多借助 Privoxy 提供的工具，比如 <a href="http://config.privoxy.org/show-url-info">http://config.privoxy.org/show-url-info</a>，可以查看你定义的规则是否对某一条 URL 生效。
  </p>
  
  <p>
    最后，如果已经看明白 Privoxy 的用法，并且打算自定义一些规则，欢迎关注我 <a href="https://github.com/chenxsan/Privoxy">Github 上的配置文件库</a>。
  </p>
</div>