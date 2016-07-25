---
title: WordPress RSS 标题重复
author: 陈 三
layout: post
date: 2013-03-18T13:17:47+00:00
url: /wordpress-rss-title-duplicate.html
dsq_thread_id:
  - 1148048937
views:
  - 953
categories:
  - WordPress
tags:
  - Wordpress

---
我的博客标题为「陈三」，RSS 地址为 <http://www.zfanw.com/blog/feed>，古怪的是，这个 feed 地址的标题重复了一次，显示为「陈三陈三」。

WordPress 网站上也有人报告过[同样问题][1]。

在本地安装了全新的 WordPress 3.5.1，然后逐个安装插件进行排查，依然没有结果。至于以前安装的插件是否造成现在的影响，则是不得而知了。

一个粗暴、简单的解决办法是，打开 `wp-include/feed-rss2.php` 文件，查找如下：

    <channel>
        <title><?php bloginfo_rss('name');wp_title_rss(); ?></title>
    

将 `bloginfo_rss('name')` 部分移除。

但是，如上所说的，这个方法太过粗暴了。

根据 [WordPress][2] 上关于 wp\_title 过滤器的说明，则是我在写 wp\_title 这个 filter 时少写了如下判断语句：

    if ( is_feed() )
        return $title;
    

在 wp_title 函数中增加该语句后，RSS 的标题就不再重复了。

 [1]: http://wordpress.org/support/topic/rss-feed-title-doubled
 [2]: http://codex.wordpress.org/Plugin_API/Filter_Reference/wp_title