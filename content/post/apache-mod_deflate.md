---
title: 如何安装使用 Apache mod_deflate 模块
author: 陈 三
layout: post
date: 2014-10-31T14:20:58+00:00
url: /apache-mod_deflate.html
views:
  - 883
categories:
  - openSUSE
  - WordPress
tags:
  - apache
  - openSUSE

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 安装</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 启用</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-3"><span class="toc_number toc_depth_1">3</span> 配置</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    最近把博客从虚拟主机搬到 VPS 上，自然一番折腾。估计围绕这一过程，写三四篇博客不是梦。
  </p>
  
  <p>
    这是第一篇，服务器端的压缩功能 &#8211; 服务器在返回内容前先对内容做 gzip 压缩，以减小传输的文件大小 &#8211; 照 <a href="https://developers.google.com/speed/docs/insights/EnableCompression">Google 的说法</a>，能减小 90%，但这也不是重点，重点是服务器端不开启 gzip 压缩的话，Google PageSpeed 的测试就会<a href="https://developers.google.com/speed/pagespeed/insights/?url=http://www.zfanw.com/blog/&tab=desktop">扣分</a> &#8211; 我个人特别在意这个分数。
  </p>
  
  <p>
    Apache 下，压缩功能由 <a href="http://httpd.apache.org/docs/2.4/mod/mod_deflate.html">mod_deflate</a> 模块控制。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">安装</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    我的 VPS 系统装的是 openSUSE 13.1 64 位系统，Apache 版本为 2.4。首先查看下系统中是否已经安装 <em>mod_deflate</em>模块，我知道的有两种方法：
  </p>
  
  <ol>
    <li>
      <p>
        当前用户下 执行命令 <code>httpd2 -M</code>，输出的内容大致如下：
      </p>
      
      <pre><code>chenxsan@zfanw.com:~&gt; httpd2 -M
[Fri Oct 31 13:13:59.278203 2014] [so:warn] [pid 9292] AH01574: module deflate_module is already loaded, skipping
Loaded Modules:
core_module (static)
access_compat_module (static)
so_module (static)
http_module (static)
mpm_prefork_module (static)
unixd_module (static)
systemd_module (static)
actions_module (shared)
alias_module (shared)
auth_basic_module (shared)
authn_file_module (shared)
authz_host_module (shared)
authz_groupfile_module (shared)
authz_user_module (shared)
autoindex_module (shared)
cgi_module (shared)
dir_module (shared)
env_module (shared)
expires_module (shared)
include_module (shared)
log_config_module (shared)
mime_module (shared)
negotiation_module (shared)
setenvif_module (shared)
ssl_module (shared)
userdir_module (shared)
reqtimeout_module (shared)
authn_core_module (shared)
authz_core_module (shared)
php5_module (shared)
rewrite_module (shared)
deflate_module (shared)
</code></pre>
    </li>
    
    <li>
      <p>
        查看 <em>/etc/sysconfig/apache2</em> 文件内容，可以直接打开文件，也可以使用 <code>grep</code> 命令：
      </p>
      
      <pre><code>grep "APACHE_MODULES=" /etc/sysconfig/apache2
</code></pre>
      
      <p>
        得出的结果大致如下：
      </p>
      
      <blockquote>
        <p>
          APACHE_MODULES=&#8221;actions alias auth_basic authn_file authz_host authz_groupfile authz_user autoindex cgi dir env expires include log_config mime negotiation setenvif ssl userdir reqtimeout authn_core authz_core mod-userdir php5 mod_rewrite mod_deflate deflate&#8221;
        </p>
      </blockquote>
    </li>
  </ol>
  
  <p>
    我这里显示的结果是已经安装加载了 <em>mod_deflate</em> 模块。
  </p>
  
  <p>
    假如没有，则使用 <a href="http://man.he.net/man8/a2enmod"><code>a2enmod</code></a> 来启用：
  </p>
  
  <pre><code>sudo a2enmod deflate
</code></pre>
  
  <p>
    等等，为什么没说安装直接进入启用阶段？因为 <em>mod_deflate</em> 模块在安装 Apache 时已经捎带装上，所以可以跳过安装这个步骤。
  </p>
  
  <p>
    启用 <em>mod_deflate</em> 模块后，需要<a href="https://activedoc.opensuse.org/book/opensuse-reference/chapter-20-the-apache-http-server#sec.apache2.start_stop">重启 Apache 服务器</a>：
  </p>
  
  <pre><code>sudo rcapache2 restart
</code></pre>
  
  <h2 class="storycontent-h2">
    <span id="i-2">启用</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    如上所述。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-3">配置</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-3" href="#i-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    启用 <em>mod_deflate</em> 模块后，就可以开始配置了。
  </p>
  
  <p>
    可以照 openSUSE 的<a href="https://en.opensuse.org/SDB:Linux_Apache_MySQL_PHP#mod_deflate">操作说明</a>一步步来，也可以粗野直接点，修改 <em>/etc/apache2/httpd.conf</em> 文件，在文件末加入如下代码：
  </p>
  
  <pre><code>SetOutputFilter DEFLATE
SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ \
    no-gzip dont-vary
SetEnvIfNoCase Request_URI \
    \.(?:exe|t?gz|zip|bz2|sit|rar|7z)$ \
    no-gzip dont-vary
SetEnvIfNoCase Request_URI \.pdf$ no-gzip dont-vary

BrowserMatch ^Mozilla/4 gzip-only-text/html
BrowserMatch ^Mozilla/4\.0[678] no-gzip
BrowserMatch \bMSIE !no-gzip !gzip-only-text/html
</code></pre>
  
  <p>
    或者可以考虑 h5bp 提供的<a href="https://github.com/h5bp/server-configs-apache/blob/master/src/web_performance/compression.conf">配置</a>。
  </p>
  
  <p>
    然后重启 Apache：
  </p>
  
  <pre><code>sudo rcapache2 restart
</code></pre>
  
  <p>
    再跑一趟 PageSpeed，就不会再提服务器压缩的事 &#8211; 恭喜，你已经压缩掉 90% 的传输文件大小，为用户节省大量带宽与时间。
  </p>
</div>