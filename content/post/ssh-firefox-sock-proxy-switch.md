---
title: Firefox SOCKS 代理切换
author: 陈 三
layout: post
date: 2012-10-25T15:14:20+00:00
url: /ssh-firefox-sock-proxy-switch.html
views:
  - 2129
dsq_thread_id:
  - 900030521
categories:
  - Firefox
  - vimperator
tags:
  - Firefox
  - proxy
  - ssh
  - vimperator

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 修订历史</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#autoproxychangerjs"><span class="toc_number toc_depth_1">2</span> autoproxychanger.js</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <h2 class="storycontent-h2">
    <span id="i">修订历史</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <span itemprop=dateModified>2012.12.14</span>：文中介绍的方法，在对待所有网站上，是没有区别的，要么全部走 SOCKS 代理，要么全部不走，而且要经常<strong>手动</strong>切换，办法太笨，推荐使用更智能的 <a href="http://getfoxyproxy.org/">FoxyProxy</a>。
    </li>
  </ol>
  
  <p>
    如果你有一个 SSH 账号，允许你登录到远程电脑，那么可以将 Firefox 请求的数据通过 SSH tunnel 发送给远程电脑，借助远程电脑访问你想要访问的信息，保证信息安全。
  </p>
  
  <p>
    首先，通过 SSH 连接上远程电脑：
  </p>
  
  <pre><code>$ ssh -D 9999 -C samchen@zfanw.com
</code></pre>
  
  <p>
    <code>D</code> 参数表示 SSH 隧道在本地电脑监听的端口，<code>C</code> 参数表示压缩传输的数据。这样我们就利用 SSH 转发端口功能在本地电脑与远程电脑之间建起一条安全通道。
  </p>
  
  <p>
    接着是启用 Firefox 的 SOCKS 代理，打开 firefox 首选项中的网络，选择「设置」，然后进入代理配置对话框，按下图所示填入信息：
  </p>
  
  <p>
    [resp_image id=&#8217;15216&#8242; caption=&#8221; ]
  </p>
  
  <p>
    这样，firefox 浏览器所请求的数据将通过 SSH tunnel 发送给远程电脑，再由远程电脑代理我们请求。
  </p>
  
  <p>
    可是，如果经常要切换 SOCKS 代理呢？总不能时不时要打开代理设置对话框。当然，可以考虑装一个 firefox 扩展，不过我 firefox 上扩展的数量已经不下 10 个了，没打算为着这么个小功能特意装个插件。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="autoproxychangerjs">autoproxychanger.js</span><a title="标题链接地址" class="u-floatRight hidden" id="heyautoproxychangerjs" href="#autoproxychangerjs"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    如果你使用 Vimperator 扩展，则可以安装 <a href="https://github.com/vimpr/vimperator-plugins/blob/master/autoproxychanger.js">autoproxychanger.js</a>，这是一个 vimperator 脚本扩展，用于通过命令行控制代理的切换、开关。
  </p>
  
  <p>
    首先将其安装到 .vimperator/plugin/ 目录下，然后打开 .vimperatorrc 配置文件，加入如下两行内容：
  </p>
  
  <pre><code>let autochanger_proxy_settings = "[{ name:'disable', usage: 'direct connection', proxy:{type:0} },{ name:'socks', usage: 'ssh tunnel', proxy:{type:1,socks:'localhost',socks_port:9999,no_proxies_on:'localhost,127.0.0.1',}}]"

let autochanger_proxy_enabled="true"
</code></pre>
  
  <p>
    保存，然后重启 firefox，按 <kbd>:</kbd> 进入命令行模式，输入命令 <code>proxy</code>，再按一个空格，可以看到有三个自动补齐项：
  </p>
  
  <ol>
    <li>
      default
    </li>
    <li>
      disable
    </li>
    <li>
      socks
    </li>
  </ol>
  
  <p>
    选择 socks 即可启用 firefox 的 SOCKS 代理，disable 则是不使用代理。
  </p>
  
  <p>
    接着再到 vimperator 配置文件中定向两个键映射：
  </p>
  
  <pre><code>nnoremap &lt;C-A-p&gt; :proxy socks&lt;CR&gt;
nnoremap &lt;C-A-d&gt; :proxy disable&lt;CR&gt;
</code></pre>
  
  <p>
    这样就可以按 <kbd>Ctrl-Alt-P</kbd> 启用 SOCKS 代理，按 <kbd>Ctrl-Alt-D</kbd> 关闭代理。
  </p>
</div>