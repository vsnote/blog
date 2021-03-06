---
title: Ubuntu 软件安装
author: 陈 三
layout: post
date: 2012-11-13T09:50:02+00:00
url: /install-software-on-ubuntu.html
views:
  - 2293
dsq_thread_id:
  - 925859972
categories:
  - Ubuntu
tags:
  - Ubuntu

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#Ubuntu"><span class="toc_number toc_depth_1">1</span> Ubuntu 软件源</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_Deb"><span class="toc_number toc_depth_1">2</span> 下载的 Deb 安装包</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#PPA_8211_Personal_Package_Archives"><span class="toc_number toc_depth_1">3</span> PPA &#8211; Personal Package Archives</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">4</span> 编译源代码</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">5</span> 参考</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    刚开始接触 Ubuntu 时，对它的软件安装方面，我只觉一片混乱，也是在那时，我觉得 Windows 平台下软件安装的易用性其实非常不错 &#8211; 多时就是一个可执行的 EXE 或 MSI 文件，双击然后一路点击下一步即可；又或者解压，就可以直接运行 &#8211; 基本上，会用电脑的人都知道怎样在 Windows 上安装软件。但 Ubuntu 上有所不同，或者说，Linux 系统下的情况与 Windows 平台不太一样。
  </p>
  
  <p>
    首先了解一个软件包（Package）的概念。软件包包含程序运行的所需文件。但同样是“包”，又可以分两种，一种是源文件包，一种是已经编译过的二进制包 &#8211; 二进制文件计算机可以直接执行，比如 Windows 下的 exe 文件，或者 Ubuntu 下的 deb 包；而源文件不行，需要编译才行。那为什么 Linux 下软件包不全部以二进制可直接执行的形式提供？这是因为 Linux 系统种类繁多，所使用的二进制有所不同，需要分别打包才行，比如，x86 架构跟 AMD64 的需要分别提供，32 位系统与 64 位的也需要分别提供。
  </p>
  
  <p>
    也就是说，Windows 下提供的软件安装文件基本都是已编译过的，而 Ubuntu 下就不一定。我暂时还没听说过有人在 Windows 平台下载源文件然后编译个一天一夜的，Linux 下却是听了好几次。
  </p>
  
  <p>
    所以，Ubuntu 系统里安装软件的问题在于，<strong>编译</strong>过的安装软件包怎么取得 &#8211; 或者已有提供，或者自己编译。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="Ubuntu">Ubuntu 软件源</span><a title="标题链接地址" class="u-floatRight hidden" id="heyUbuntu" href="#Ubuntu"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Ubuntu 的软件源（software channels/repositories）上包含了许多可以直接下载、安装的软件包，它有四个频道：Main、Restricted、Universe 和 Multiverse，它们的目的有所不同，默认仅 Main 与 Restricted 频道上的软件可以下载安装，但可以设置启用其他两个频道。对普通用户的使用来说，区别并没那么大。
  </p>
  
  <p>
    从这些软件源上下载软件安装的方法有多种：
  </p>
  
  <h3>
    APT 命令行
  </h3>
  
  <p>
    APT 是 Advanced Packaging Tool 的缩写，用于管理软件包。
  </p>
  
  <p>
    通过它的命令行工具来安装软件非常简单。首先打开 shell，
  </p>
  
  <pre><code>sudo apt-get install &lt;package_name&gt; 
</code></pre>
  
  <p>
    <package_name> 是软件在源里的名称，如果无法确定，可以通过下列命令来查询：
  </p>
  
  <pre><code>apt-cache search &lt;keyword&gt;
</code></pre>
  
  <p>
    譬如说要在 Ubuntu 下安装 dropbox，可以通过上述命令确定 dropbox 的名称，如下图：
  </p>
  
  <p>
    <a href="http://www.zfanw.com/blog/wp-content/uploads/2012/11/apt-cache-search-dropbox.png"><img src="http://www.zfanw.com/blog/wp-content/uploads/2012/11/apt-cache-search-dropbox.png" alt="搜索软件源中的 dropbox 关键词" title="apt-cache-search-dropbox" width="471" height="108" class="alignnone size-full wp-image-6740" srcset="https://www.zfanw.com/blog/wp-content/uploads/2012/11/apt-cache-search-dropbox.png 471w, https://www.zfanw.com/blog/wp-content/uploads/2012/11/apt-cache-search-dropbox-300x68.png 300w" sizes="(max-width: 471px) 100vw, 471px" /></a>
  </p>
  
  <p>
    如果不喜欢命令行，Ubuntu 也还有其他可视化的图形操作界面用于安装软件。
  </p>
  
  <h3>
    Aptitude
  </h3>
  
  <p>
    Aptitude 是 APT 的前端界面，通过它可以操控真正的 APT 命令。它支持键盘操作 &#8211; 如果熟悉 Vim，就会发现大部分快捷键均可用，它也部分支持鼠标操作。
  </p>
  
  <p>
    个人平时极少使用这个工具，更倾向于用命令行 apt-get 或者下面要介绍的几个方法。
  </p>
  
  <p>
    不过这个软件有个彩蛋，如下图，蛮好玩的：
  </p>
  
  <p>
    <img src="https://upload.wikimedia.org/wikipedia/commons/c/c6/Aptitude_moo.png" alt="aptitude" />
  </p>
  
  <p>
    注：图片来自 <a href="https://en.wikipedia.org/wiki/File:Aptitude_moo.png">Wikipedia</a>。
  </p>
  
  <h3>
    软件中心
  </h3>
  
  <p>
    Ubuntu 软件中心对新手来说，是非常简单明了的软件管理工具。
  </p>
  
  <p>
    打开软件中心，搜索软件，安装软件，就这么简单。
  </p>
  
  <h3>
    新立得
  </h3>
  
  <p>
    英文名叫 ”Synaptic“，就我所了解，Ubuntu 12.04 之后的版本中默认并不安装新立得软件包管理器，需要用户自己安装：
  </p>
  
  <pre><code>sudo apt-get install synaptic
</code></pre>
  
  <p>
    之后打开新立得搜索软件安装即可。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Deb">下载的 Deb 安装包</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Deb" href="#_Deb"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    某些软件有提供编译过的安装包文件下载，Ubuntu 下这种安装包文件的格式是 .deb。
  </p>
  
  <p>
    安装 .deb 包的方法如下：
  </p>
  
  <ol>
    <li>
      <p>
        通过 GDebi 工具，可以直接在命令行中运行，也可以通过图形界面 GDebi-gtk，如下图。
      </p>
      
      <p>
        <a href="http://www.zfanw.com/blog/wp-content/uploads/2012/11/gdebi.png"><img src="http://www.zfanw.com/blog/wp-content/uploads/2012/11/gdebi.png" alt="gdebi 安装 .deb 文件" title="gdebi" width="540" class="alignnone size-full wp-image-6751" srcset="https://www.zfanw.com/blog/wp-content/uploads/2012/11/gdebi.png 540w, https://www.zfanw.com/blog/wp-content/uploads/2012/11/gdebi-300x175.png 300w" sizes="(max-width: 540px) 100vw, 540px" /></a>
      </p>
    </li>
    
    <li>
      dpkg 安装 &#8211; 首先定位到 deb 安装文件目录下，然后运行命令 <code>sudo dpkg -i package_name.deb</code>。
    </li>
  </ol>
  
  <h2 class="storycontent-h2">
    <span id="PPA_8211_Personal_Package_Archives">PPA &#8211; Personal Package Archives</span><a title="标题链接地址" class="u-floatRight hidden" id="heyPPA_8211_Personal_Package_Archives" href="#PPA_8211_Personal_Package_Archives"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    因为安全或不稳定或其他种种因素，Ubuntu 软件源中不可能收录所有软件，于是有了 PPA，它的作用类似于 Ubuntu 官方的源，只不过是由个人提供打包，当然也会有某些官方源中的软件通过 PPA 发布不稳定版本等。
  </p>
  
  <p>
    PPA 的使用也非常简单，首先添加 PPA 源到 Ubuntu：
  </p>
  
  <pre><code>sudo add-apt-repository ppa:user/ppa-name
</code></pre>
  
  <p>
    然后更新所有源：
  </p>
  
  <pre><code>sudo apt-get update
</code></pre>
  
  <p>
    接着是安装 &#8211; 因为将 PPA 源添加到 Ubuntu 后，安装软件的方法与从官方源中安装并没有两样，所以，第一步中介绍的方法均可以使用：
  </p>
  
  <pre><code>sudo apt-get install &lt;package_name&gt;
</code></pre>
  
  <h2 class="storycontent-h2">
    <span id="i">编译源代码</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    源代码包中一般均带有 INSTALL 或 README 之类的安装说明文件，根据说明安装即可。
  </p>
  
  <p>
    不过这种方法是我最不愿意碰的，因为往往会为编译一个软件事先折腾一大堆东西 &#8211; 而我可能根本不想了解这些，只是想装好这个软件使用它而已。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">参考</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <a href="https://help.ubuntu.com/community/Repositories">Ubuntu 的软件源</a>
    </li>
    <li>
      <a href="https://help.ubuntu.com/community/InstallingSoftware">Ubuntu 软件安装方法</a>
    </li>
    <li>
      <a href="https://help.ubuntu.com/community/AptGet/Howto?action=show&redirect=AptGetHowto">APT 管理软件包</a>
    </li>
    <li>
      <a href="https://en.wikipedia.org/wiki/Aptitude_(software)">Aptitude</a>
    </li>
    <li>
      <a href="https://help.ubuntu.com/community/UbuntuSoftwareCenter?action=show&redirect=SoftwareCenterFAQ">软件中心</a>
    </li>
    <li>
      <a href="https://help.launchpad.net/Packaging/PPA">PPA</a>
    </li>
    <li>
      <a href="https://help.launchpad.net/Packaging/PPA/InstallingSoftware">从 PPA 安装软件</a>
    </li>
  </ol>
</div>