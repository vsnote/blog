---
title: XAMPP 虚拟主机设置
author: 陈 三
layout: post
date: 2012-08-22T13:52:56+00:00
url: /xampp-virtual-hosts.html
views:
  - 1246
dsq_thread_id:
  - 814505445
categories:
  - 前端开发
tags:
  - xampp
  - 虚拟主机设置

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 更新</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 参考</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    我系统上 XAMPP 安装在 /opt/lampp 目录下，于是本地服务器根目录处在 /opt/lampp/htdocs，如果不做更改的话，需要把文件放到 htdocs 里才能通过 http://localhost/ 访问到，这会有一个问题，/opt 目录特殊，在其下新建的文件均有权限上的限制，需要 sudo 才能编辑，非常不便。
  </p>
  
  <p>
    另外，Eclipse 默认的 Workspace 目录是建在用户主目录下的，即 /home/username/workspace，所以，如果 workspace 目录能享受本地服务器根目录待遇就没什么问题了。
  </p>
  
  <p>
    解决办法有几种，但最为方便，也有助于分离不同项目，便于管理、调试的方法是设置虚拟主机 &#8211; 我想卖虚拟主机的人们肯定很熟悉这个。
  </p>
  
  <p>
    打开 httpd.conf 文件，在末尾加入以下：
  </p>
  
  <pre><code>&lt;VirtualHost *:80&gt;
    ServerName localhost
    DocumentRoot /opt/lampp/htdocs
&lt;/VirtualHost&gt;

&lt;VirtualHost *:80&gt;
    ServerName ec.localhost
    DocumentRoot /home/sam/workspace
    &lt;Directory /home/sam/workspace&gt;
                Require all granted
        AllowOverride all
        Order Allow,Deny
        Allow from all
    &lt;/Directory&gt;
&lt;/VirtualHost&gt;
</code></pre>
  
  <p>
    之后打开 /etc/hosts 文件，加入：
  </p>
  
  <pre><code>127.0.0.1 ec.localhost
</code></pre>
  
  <p>
    将 ec.localhost 域名解析到 127.0.0.1 上。
  </p>
  
  <p>
    这时访问 ec.localhost 就没问题了。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">更新</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    2012.12.28 Fri
  </p>
  
  <p>
    另一个办法，可以达到相似的目的，并且要比上述办法简单，就是利用 Apache 配置中的 Alias 功能。
  </p>
  
  <p>
    打开 httpd.conf 文件，查找 <code>&lt;/Directory&gt;</code>，添加以下内容：
  </p>
  
  <pre><code>Alias /ec /home/sam/ec
</code></pre>
  
  <p>
    重启 Apache，然后我们就可以通过 localhost/ec 来访问 /home/sam/ec 目录了。当然，如果仅这样设置就开始访问 localhost/ec 会显示 403 错误，表示没有权限访问，所以我们还要为其设置权限：
  </p>
  
  <pre><code>&lt;Directory /home/sam/ec&gt;
  Require all granted
  Order allow,deny
  Allow from all
&lt;/Directory&gt;    
</code></pre>
  
  <p>
    将上述语句加到 Alias 语句后，保存 httpd.conf 并重启 Apache 服务器。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">参考</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <a href="http://httpd.apache.org/docs/2.4/vhosts/name-based.html">Virtual hosts</a>
    </li>
    <li>
      <a href="http://httpd.apache.org/docs/2.4/mod/mod_access_compat.html">http://httpd.apache.org/docs/2.4/mod/mod_access_compat.html</a>
    </li>
    <li>
      <a href="https://httpd.apache.org/docs/2.2/mod/mod_alias.html">Apache Module mod_alias</a>
    </li>
  </ol>
</div>