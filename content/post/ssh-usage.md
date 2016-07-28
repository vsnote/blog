---
title: SSH 使用方法
author: 陈 三
layout: post
date: 2012-10-23T04:41:02+00:00
url: /ssh-usage.html
views:
  - 1263
dsq_thread_id:
  - 896078436
categories:
  - openSUSE
  - Ubuntu
tags:
  - ssh

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 服务器上生成公钥/私钥</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 本地电脑生成公/私钥</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-3"><span class="toc_number toc_depth_1">3</span> 参考</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    前些日子，花钱买了个 SSH，想着总有机会用到，但来来去去，却实在找不到用处，后来都差点忘了这回事。
  </p>
  
  <p>
    很多空间服务器商在卖空间的同时，其实都配有一个 ssh 账号，用于建立安全通道，保证访问空间数据的安全性。
  </p>
  
  <p>
    比如我的博客，可以通过以下命令连接到服务器：
  </p>
  
  <pre><code>$ ssh zfanwcom@zfanw.com
</code></pre>
  
  <p>
    zfanwcom 指用户名，zfanw.com 指 ssh 服务器地址。随后会要求输入登录密码。
  </p>
  
  <p>
    登录到服务器上后，可以使用 <code>ls</code> 命令查看默认目录下的内容，这些内容与用 ftp 连接看到的内容一样，只不过数据的传输说是要比 ftp 安连接全。而如果使用命令 <code>pwd</code> 查看当前目录，则显示的是 /home/zfanwcom，即用户主目录。
  </p>
  
  <p>
    输入密码的方式有几个不好之处，一是如果密码太复杂太长，命令行里不便输入，另外安全性也差，因为只是个密码。因此 ssh 还有其他方式登录，比如公钥/私钥。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">服务器上生成公钥/私钥</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    我们先在服务器上生成一对公钥/私钥，然后将私钥下载到本地电脑，假设名称为 id_rsa，保存到 ~/.ssh/ 目录下，
  </p>
  
  <p>
    注意，需要更改该私钥的读写权限为 <code>rw-------</code>，如果权限设置不正确，ssh 会拒绝使用。
  </p>
  
  <pre><code>$ chmod 600 id_rsa
</code></pre>
  
  <p>
    接下来可以通过如下命令来访问服务器：
  </p>
  
  <pre><code>$ ssh -i $HOME/.ssh/id_rsa server
</code></pre>
  
  <p>
    这样我们就不需要输入密码。但这样还是需要输入服务器地址，所以还有一个更简便的方法，就是配置 ssh config 文件。
  </p>
  
  <p>
    打开 ~/.ssh/config 文件(如果没有请创建一个)，写入以下内容
  </p>
  
  <pre><code>Host zfanw
    HostName zfanw.com
    Port    22
    User    zfanwcom
    IdentityFile    ~/.ssh/id_rsa
</code></pre>
  
  <p>
    保存后，在命令行输入 <code>ssh zfanw</code> 即可以不输入密码访问空间服务器，但可能还需要输入一个 passphrase，这是用于加密私钥用的，如果偷懒，可以设置得简单一点，又或者不设置。
  </p>
  
  <p>
    以上是在空间服务器上生成一对公钥/私钥的，显然，我们的私钥也在上面 &#8211; 出于安全考虑，我想应该把它删除。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">本地电脑生成公/私钥</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    如果在本机生成一对公钥/私钥，则可以使用 ssh-keygen 命令：
  </p>
  
  <pre><code>$ mkdir -p $HOME/.ssh
$ chmod 0700 $HOME/.ssh
$ ssh-keygen -t rsa
</code></pre>
  
  <p>
    根据提示操作，这样就在 ~/.ssh/ 目录下会生成一个私钥 id_rsa，一个公钥 id_rsa.pub，接着用 ssh-copy-id 命令将公钥拷贝到 ssh 服务器上，这个方法能省去很多拷贝、设置权限的操作：
  </p>
  
  <pre><code>$ ssh-copy-id -i ~/.ssh/id_rsa.pub zfanwcom@zfanw.com
</code></pre>
  
  <p>
    然后输入密码，就将公钥加入到 ssh 服务器上的 ~/.ssh/authorized_keys 文件里。
  </p>
  
  <p>
    接下来通过配置 .ssh/config 文件来更简便地连接 ssh 服务器。
  </p>
  
  <p>
    据我理解，一对公钥/私钥应该可以通用，也可以分别针对不同服务器生成各自的公钥/私钥，比如为 github 服务器生成 github_id_rsa/github_id_rsa.pub，zfanw 服务器则使用 zfanw_id_rsa/zfanw_id_rsa.pub，这是鸡蛋放不同的篮子。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-3">参考</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-3" href="#i-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <a href="https://en.wikipedia.org/wiki/Ssh-keygen">Wikipedia 上的 ssh-keygen 词条</a>
    </li>
    <li>
      <a href="http://nerderati.com/2011/03/simplify-your-life-with-an-ssh-config-file/">Simplify Your Life With an SSH Config File</a>
    </li>
    <li>
      <a href="https://help.github.com/articles/generating-ssh-keys">Generating SSH Keys &#8211; github</a>
    </li>
  </ol>
</div>