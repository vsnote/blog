---
title: WordPress body_class添加自定义类
author: 陈 三
layout: post
date: 2014-08-09T14:47:51+00:00
url: /wordpress-body_class-customize.html
views:
  - 733
categories:
  - WordPress
tags:
  - Wordpress

---
WordPress的PHP代码里，有如下一段：

    <body <?php body_class(); ?>
    

这段代码[^13295.1]根据当前页面的状态，输出相应的CSS类，比如：

    <body class="single single-post postid-13295 single-format-standard logged-in"
    

这些CSS类都是WordPress自动计算的，如果我们要添加自定义的CSS类，却不能直接在PHP代码中添加。而需要通过WordPress提供的filter。

打开functions.php文件，添加如下代码：

    <?php
    function add_custom_body_class( $classes ) {
      global $post;
      if ( isset( $post ) ) {
        $classes[] = 'Grid';
      }
      return $classes;
    }
    add_filter( 'body_class', 'add_custom_body_class' );
    ?>
    

这样就给WordPress的`body`标签加了一个`Grid`的CSS自定义类。

[^13295.1]:    
    [Function Reference/body class « WordPress Codex][1]

 [1]: http://codex.wordpress.org/Function_Reference/body_class