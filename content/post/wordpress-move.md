---
title: WordPress 迁移
author: 陈 三
layout: post
date: 2014-11-02T01:11:55+00:00
excerpt: WordPress 转移服务器总结
url: /wordpress-move.html
views:
  - 1022
categories:
  - WordPress
tags:
  - Wordpress

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 备份旧服务器上的数据库</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 备份旧服务器上的文件</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-3"><span class="toc_number toc_depth_1">3</span> 导入旧数据库到新服务器</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-4"><span class="toc_number toc_depth_1">4</span> 复制旧文件到新服务器</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-5"><span class="toc_number toc_depth_1">5</span> 解析域名</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-6"><span class="toc_number toc_depth_1">6</span> 错误情况</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    前些日子我终于下定决心买 VPS，然后就把这个博客从虚拟主机上迁移过去。因为域名不变，只是换空间，所以大部分步骤是按 <a href="http://codex.wordpress.org/Moving_WordPress#Keeping_Your_Domain_Name_and_URLs">WordPress 提供的文档</a>操作。不过过程中碰上不少问题，最终且算是解决了，所以做一总结。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">备份旧服务器上的数据库</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    旧的虚拟主机上提供有 cPanel 界面，所以<a href="http://codex.wordpress.org/Backing_Up_Your_Database">操作</a>十分简单。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">备份旧服务器上的文件</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    同样可以借助 cPanel。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-3">导入旧数据库到新服务器</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-3" href="#i-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    因为 VPS 上没有 cPanel，所以数据库的导入是通过<a href="http://codex.wordpress.org/Restoring_Your_Database_From_Backup">命令行执行</a>的。
  </p>
  
  <p>
    首先通过 <a href="http://www.zfanw.com/blog/ssh-usage.html">SSH 登录</a>到服务器：
  </p>
  
  <pre><code>ssh zfanw
</code></pre>
  
  <p>
    然后执行 MySQL 命令：
  </p>
  
  <pre><code>sam@zfanw.com: mysql -u mysqlusername -p databaseName &lt; zfanw.com.bak.sql
</code></pre>
  
  <p>
    导入的过程非常快，如果不确信是否成功，可以执行 MySQL 命令查看：
  </p>
  
  <pre><code>use zfanwcom;
show tables;
</code></pre>
  
  <p>
    结果如下：
  </p>
  
  <pre><code>mysql&gt; show tables;
+---------------------------+
| Tables_in_zfanwcom |
+---------------------------+
| wp_PopularPostsdata       |
| wp_commentmeta            |
| wp_comments               |
| wp_links                  |
| wp_options                |
| wp_postmeta               |
| wp_posts                  |
| wp_sucuri_lastlogins      |
| wp_term_relationships     |
| wp_term_taxonomy          |
| wp_terms                  |
| wp_usermeta               |
| wp_users                  |
+---------------------------+
</code></pre>
  
  <h2 class="storycontent-h2">
    <span id="i-4">复制旧文件到新服务器</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-4" href="#i-4"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    数据库导入完成后，将虚拟主机上备份的文件上传到 VPS 并解压到相应目录。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-5">解析域名</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-5" href="#i-5"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    将域名重新解析到新的 IP 上。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-6">错误情况</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-6" href="#i-6"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    解析完成后访问新 IP 上的博客，就出现了各种情况。
  </p>
  
  <p>
    先来看下 <em>/etc/apache2/vhosts.d/</em> 目录下 <em>zfanw.com.conf</em> 这个虚拟主机文件的配置：
  </p>
  
  <pre><code>&lt;VirtualHost *:80&gt;
    ServerName zfanw.com
    ServerAlias www.zfanw.com
    ServerAdmin chenxsan@gmail.com

    DocumentRoot /srv/www/vhosts/zfanw.com

    &lt;Directory "/srv/www/vhosts/zfanw.com"&gt;
        AllowOverride All
        Options FollowSymLinks

        Order allow,deny
        Allow from all

    &lt;/Directory&gt;

&lt;/VirtualHost&gt;
</code></pre>
  
  <h3>
    404 错误
  </h3>
  
  <p>
    我碰到的情况中，有一种错误是这样：
  </p>
  
  <blockquote>
    <p>
      Object not found!
    </p>
    
    <p>
      The requested URL was not found on this server. The link on the referring page seems to be wrong or outdated. Please inform the author of that page about the error.
    </p>
    
    <p>
      If you think this is a server error, please contact the webmaster.
    </p>
    
    <p>
      Error 404
    </p>
    
    <p>
      www.zfanw.com
    </p>
    
    <p>
      Apache/2.4.6 (Linux/SUSE)
    </p>
  </blockquote>
  
  <p>
    网上的资料有说是 <em>.htaccess</em> 文件的问题，因为我自定义了 WordPress 的固定链接。但我的 <em>.htaccess</em> 文件内容如下：
  </p>
  
  <pre><code># BEGIN WordPress
&lt;IfModule mod_rewrite.c&gt;
RewriteEngine On
RewriteBase /
RewriteRule ^index\.php$ - [L]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /index.php [L]
&lt;/IfModule&gt;
# END WordPress
</code></pre>
  
  <p>
    这是 <a href="http://codex.wordpress.org/htaccess#Basic_WP">WordPress 默认</a>的。另外，使用<a href="http://www.zfanw.com/blog/apache-mod_deflate.html">上一篇</a>介绍的方法，可以看到我的服务器上已经安装了 <em>mod_rewrite</em> 模块。
  </p>
  
  <p>
    我的情况下，问题出在 <em>/etc/apache2/httpd.conf</em> 文件，<a href="http://codex.wordpress.org/Permalinks#Fixing_Other_Issues">WordPress 说明如下</a>：
  </p>
  
  <blockquote>
    <p>
      Your server may not have the AllowOverride directive enabled. If the AllowOverride directive is set to None in your Apache httpd.config file, then .htaccess files are completely ignored. In this case, the server will not even attempt to read .htaccess files in the filesystem. When this directive is set to All, then any directive which has the .htaccess Context is allowed in .htaccess files.
    </p>
  </blockquote>
  
  <p>
    如果 Apache 的 <em>httpd.conf</em> (openSUSE 下安装的 Apache 里配置文件是叫这个) 中 <code>AllowOverride</code> 被设置为 <em>None</em>，则 <em>.htaccess</em> 文件完全被忽视，所以我需要修改 <em>httpd.conf</em> 文件内容，结果如下：
  </p>
  
  <pre><code> &lt;Directory /&gt;
    Options FollowSymLinks
    AllowOverride All
 &lt;/Directory&gt;
</code></pre>
  
  <p>
    重启 Apache 服务器：
  </p>
  
  <pre><code>sudo rcapache2 restart
</code></pre>
  
  <p>
    再度访问博客，问题消失了。
  </p>
  
  <p>
    不过这篇是事后整理，碰上的许多枝末问题已经遗忘，不一定完整。
  </p>
</div>