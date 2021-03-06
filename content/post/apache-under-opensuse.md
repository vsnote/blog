---
title: openSUSE 的 Apache 配置
author: 陈 三
layout: post
date: 2014-11-27T22:26:32+00:00
excerpt: openSUSE 系统下如何配置 Apache 的虚拟主机
url: /apache-under-opensuse.html
views:
  - 685
categories:
  - openSUSE
tags:
  - apache

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#DNS_A"><span class="toc_number toc_depth_1">1</span> DNS 绑定 A 记录</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">2</span> 创建站点目录</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_Apache"><span class="toc_number toc_depth_1">3</span> 配置 Apache</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    我的目的，是在 openSUSE 13.1 系统下，配置 Apache 服务器绑定 <a href="http://en.zfanw.com" title="陈三的英文博客">en.zfanw.com</a> 域名。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="DNS_A">DNS 绑定 A 记录</span><a title="标题链接地址" class="u-floatRight hidden" id="heyDNS_A" href="#DNS_A"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    首先在 DNS 上创建 A 记录，将域名绑定到相应 IP 上。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">创建站点目录</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    在服务器上，添加 <em>/srv/www/vhosts/en.zfanw.com</em> 目录，并在该目录下创建一个 index.html 文件 &#8211; 用于测试。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Apache">配置 Apache</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Apache" href="#_Apache"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <h3>
    创建虚拟主机配置文件
  </h3>
  
  <pre><code>$ cd /etc/apache2/vhosts.d
$ sudo cp vhost.template en.zfanw.com.conf
</code></pre>
  
  <p>
    修改 en.zfanw.com.conf 文件内容如下：
  </p>
  
  <pre><code>&lt;VirtualHost *:80&gt;
    ServerName en.zfanw.com
    ServerAdmin chenxsan@gmail.com

    DocumentRoot /srv/www/vhosts/en.zfanw.com

    ErrorLog /var/log/apache2/en.zfanw.com-error_log
    CustomLog /var/log/apache2/en.zfanw.com-access_log combined

    # don't loose time with IP address lookups
    HostnameLookups Off

    # needed for named virtual hosts
    UseCanonicalName Off

    # configures the footer on server-generated documents
    ServerSignature On

    #
    # This should be changed to whatever you set DocumentRoot to.
    #
    &lt;Directory "/srv/www/vhosts/en.zfanw.com"&gt;
        AllowOverride All
        Options FollowSymLinks

        Order allow,deny
        Allow from all

    &lt;/Directory&gt;

&lt;/VirtualHost&gt;
</code></pre>
  
  <p>
    之后重启 Apache：
  </p>
  
  <pre><code>$ sudo rcapache2 restart
</code></pre>
  
  <p>
    访问 en.zfanw.com 网址，已经可以看到 index.html 文件的内容了。如果我们之前未添加 index.html 文件，访问的话，则会出现如下错误信息：
  </p>
  
  <blockquote>
    <p>
      Access forbidden!
    </p>
    
    <p>
      You don&#8217;t have permission to access the requested directory. There is either no index document or the directory is read-protected.
    </p>
    
    <p>
      If you think this is a server error, please contact the webmaster.
    </p>
    
    <p>
      Error 403
    </p>
    
    <p>
      en.zfanw.com
    </p>
  </blockquote>
</div>