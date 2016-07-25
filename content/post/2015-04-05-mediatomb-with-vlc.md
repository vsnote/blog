---
title: MediaTomb + VLC
author: 陈 三
layout: post
date: 2015-04-05T02:27:00+00:00
excerpt: 使用 MediaTomb 搭建自己的媒体服务器
url: /mediatomb-with-vlc.html
views:
  - 790
categories:
  - 未分类
tags:
  - Mac OSX
  - openSUSE
  - VLC

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_MediaTomb"><span class="toc_number toc_depth_1">1</span> 安装 MediaTomb</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_MediaTomb-2"><span class="toc_number toc_depth_1">2</span> 运行 MediaTomb</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_VLC"><span class="toc_number toc_depth_1">3</span> 安装 VLC</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#TODO"><span class="toc_number toc_depth_1">4</span> TODO</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">5</span> 备注</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    前阵子让 ThinkPad 退休，换了 MacBook Pro，于是 ThinkPad 就闲置一边，无所事事。今天突然想到，我手上设备也有多台了，不如把 ThinkPad 搞成媒体服务器，专门用于存储 AV(audio/video)，然后其它设备通过客户端读取。
  </p>
  
  <p>
    试验是在 MacBook + ThinkPad 上进行的，涉及的软件有：
  </p>
  
  <ol>
    <li>
      <a href="http://mediatomb.cc/">MediaTomb</a> &#8211; <a href="http://en.wikipedia.org/wiki/List_of_UPnP_AV_media_servers_and_clients#UPnP_AV_media_servers" title="维基百科 UPnP 服务器列表">UPnP 媒体服务器</a>
    </li>
    <li>
      <a href="http://www.videolan.org/vlc/download-macosx.html">VLC for Mac OSX</a>
    </li>
  </ol>
  
  <p>
    环境：
  </p>
  
  <ol>
    <li>
      ThinkPad &#8211; openSUSE 13.2 64 bits
    </li>
    <li>
      MacBook &#8211; OSX Yosimite 10.10.2
    </li>
  </ol>
  
  <p>
    <strong>注意</strong>：如果有使用 vpn、代理等等，请暂时关闭；有防火墙的也暂时关闭。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_MediaTomb">安装 MediaTomb</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_MediaTomb" href="#_MediaTomb"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <p>
        在 openSUSE 终端窗口执行以下命令：
      </p>
      
      <pre><code>sudo zypper ar -f http://packman.inode.at/suse/openSUSE_13.2/ packman
</code></pre>
      
      <p>
        这一步添加 packman 库。
      </p>
    </li>
    
    <li>
      <p>
        刷新软件库的源
      </p>
      
      <pre><code>sudo zypper ref
</code></pre>
    </li>
    
    <li>
      <p>
        安装 MediaTomb
      </p>
      
      <pre><code>sudo zypper in mediatomb
</code></pre>
      
      <p>
        这样，我们就在 openSUSE 上装好 MediaTomb 了。
      </p>
    </li>
  </ol>
  
  <h2 class="storycontent-h2">
    <span id="_MediaTomb-2">运行 MediaTomb</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_MediaTomb-2" href="#_MediaTomb-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    第二步，我们要在 openSUSE 上启动 MediaTomb。
  </p>
  
  <p>
    打开终端窗口，执行命令：
  </p>
  
  <pre><code>mediatomb
</code></pre>
  
  <p>
    MediaTomb 会绑定一个 ip:port，比如 10.10.10.35:49152 这样。但这个网址我们的其它设备是无法访问的，所以我们需要修改它。
  </p>
  
  <p>
    假设路由分配给 openSUSE 系统的 ip 地址是 192.168.0.104。我们在启动 mediatomb 时传递一个 <a href="http://mediatomb.cc/pages/documentation#id2855871">ip 参数</a>给它：
  </p>
  
  <pre><code>mediatomb --ip 192.168.0.104
</code></pre>
  
  <p>
    等它启动后，我们就可以通过这个 ip:port 访问它的 web UI 界面 &#8211; 这是一个可视化管理界面，可以添加视频文件、文件夹等，省得我们再去跟命令行打交道，截图如下：
  </p>
  
  <p>
    [resp_image id=&#8217;15265&#8242; caption=&#8221; ]
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_VLC">安装 VLC</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_VLC" href="#_VLC"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    从 <a href="http://www.videolan.org/vlc/download-macosx.html">VLC 官网</a> 下载安装 VLC，然后打开 VLC，如下图：
  </p>
  
  <p>
    [resp_image id=&#8217;15266&#8242; caption=&#8221; ]
  </p>
  
  <p>
    双击视频就可以打开，拖动也非常流畅：
  </p>
  
  <p>
    [resp_image id=&#8217;15267&#8242; caption=&#8221; ]
  </p>
  
  <h2 class="storycontent-h2">
    <span id="TODO">TODO</span><a title="标题链接地址" class="u-floatRight hidden" id="heyTODO" href="#TODO"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <input type="checkbox" disabled /> openSUSE 系统绑定静态 ip，不要每次 ip 都在变
    </li>
    <li>
      <input type="checkbox" disabled /> MediaTomb 随 openSUSE 系统启动，后台运行，不要每次都手动开启
    </li>
    <li>
      <p>
        <input type="checkbox" checked disabled /> 看看 iOS 又如何连接
      </p>
      
      <p>
        在 iOS 上安装 VLC 即可，VLC 会自动发现局域网内的 UPnP 服务器。
      </p>
    </li>
  </ol>
  
  <h2 class="storycontent-h2">
    <span id="i">备注</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      MediaTomb 很久不更新了，<a href="http://mediatomb.cc/changelog.txt">最新一个版本 v0.12.1 是在 2010.08.04 发布</a>，所以请自行斟酌是否继续使用。以我目前的使用情况看，暂时没发现什么问题。
    </li>
  </ol>
</div>