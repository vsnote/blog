---
title: WordPress 搜索框追加到菜单列表中
author: 陈 三
layout: post
date: 2012-09-13T01:33:19+00:00
url: /wordpress-seach-form-append-to-menu.html
views:
  - 1601
dsq_thread_id:
  - 841874603
categories:
  - WordPress
tags:
  - Wordpress

---
我之前的博客，最上面是一个导航条，导航条左侧是博客名称，右侧是菜单。在这个菜单的右边有个搜索框，后来被我撤掉。原先放上去是因为我经常会用到搜索框来查找博客内容，而后来撤掉则是觉得可以用 Google 搜索，没有必要放个搜索框在页面上占空间，如下图：

<img src="http://www.zfanw.com/blog/wp-content/uploads/2012/09/wordpress-search-form-append-menu.png" alt="wordpress 菜单中的搜索框" width="401" />

如果分开实现，则菜单的实现很简单：

    <?php wp_nav_menu(array('menu' => 'nav' )); ?>
    

使用 wp\_nav\_menu 函数调用主题定义的菜单即可，默认情况下会生成一个无序列表 ul。

搜索框的单独调用也很简单：

    <?php get_search_form(); ?>
    

默认情况下会生成一个 form 表单。

那么，要把这个搜索框追加到菜单列表中，即是将 form 表单包含到 li 条目里，可以使用 WordPress 的 filter 功能：

    <?php
    function search_box_function( $nav, $args ) {
       return $nav."<li class='menu-item-search'>".get_search_form(false)."</li>";
    }
    add_filter('wp_nav_menu_items','search_box_function', 10, 2);
    ?>
    

如上，首先定义一个过滤函数 search\_box\_function，函数用于返回一个改造过的菜单，之后将这个函数挂勾到过滤动作 wp\_nav\_menu_items 上。这样，就把 WordPress 的搜索框追加到菜单列表最后一个 li 中。

## 鸣谢

  1. [http://codex.wordpress.org/Function\_Reference/wp\_nav_menu][1]
  2. [http://codex.wordpress.org/Function\_Reference/get\_search_form][2]
  3. [http://codex.wordpress.org/Function\_Reference/add\_filter][3]

 [1]: http://codex.wordpress.org/Function_Reference/wp_nav_menu
 [2]: http://codex.wordpress.org/Function_Reference/get_search_form
 [3]: http://codex.wordpress.org/Function_Reference/add_filter