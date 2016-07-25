---
title: WordPress wp_title 过滤器
author: 陈 三
layout: post
date: 2012-07-13T10:54:09+00:00
url: /wordpress-wp_title-filter.html
views:
  - 1037
dsq_thread_id:
  - 763478664
categories:
  - WordPress
tags:
  - Wordpress
  - wp_title

---
WordPress 里，wp_title() 函数用于显示或返回页面标题 (title of page)，可以用在 header.php 里，但是 WordPress 的文档中又不建议直接在 header.php 中使用。

> The wp\_title() function should not be used by a theme in conjunction with other strings or functions (like concocting with bloginfo(&#8216;name&#8217;) ) to set the title because it will render plugins unable to rewrite page titles correctly. The best practice is to use the wp\_title filter with a callback function. This method is now a requirement for themes.

就是说，以下形式的用法并不推荐，因为可能会造成 WordPress 插件无法正确重写标题：

    <?php
        wp_title();
        bloginfo('name');
    ?>
    

WordPress 文档的建议的方法是使用 wp_title 过滤器(filter)。

> filter function takes as input the unmodified data, and returns modified data (or in some cases, a null value to indicate the data should be deleted or disregarded).

按上述定义，过滤器函数接受数据，然后返回改变后的数据。

也就是说，我们把 wp\_title() 函数用 wp\_title 过滤器改造。但这个改造有两个条件，一是过滤函数 &#8211; 下面语句中的 $function\_to\_add，决定怎么改造，一个是过滤勾子(hook) &#8211; 如下的 $tag，决定改造什么内容。

    <?php add_filter( $tag, $function_to_add, $priority, $accepted_args ); ?> 
    

我们先在 function.php 中定义一个 wp_title 过滤函数：

    <?php
        function yl_filter_wp_title($title,$sep,$seplocation){
        global $paged,$page;//$paged 定义博客分页的页码，$page 定义单篇内容分页处理的页码
            $sep=" ".$sep." ";//给分隔符号前后添加空格
        if ($seplocation=='right'){//判断分隔符位置是左还是右
            $title=$title.get_bloginfo('name');
        }else{
            $title=get_bloginfo('name').$title;
            }
        if ( $paged >= 2 || $page >= 2 ){
            if ($seplocation=='right')
            $title=sprintf( __( 'Page %s', '' ), max( $paged, $page ) ).$sep.$title;
            else
                $title.=$sep.sprintf( __( 'Page %s', '' ), max( $paged, $page ) );
        }
        return $title;//返回处理后的 $title 值
        }
    ?>
    

接着在 function.php 中加入过滤勾子：

    <?php
        add_filter('wp_title','yl_filter_wp_title',10,3);
    ?>
    

之后在 header.php 中调用 wp_title() 时就会触发过滤器函数，根据具体情况打印出不同页面标题。

在编写过滤器函数时，我曾经使用函数名 filter\_wp\_title，然后出现错误：Warning: Cannot modify header information &#8211; headers already sent by (output started at&#8230;&#8230;，将函数名称改成 yl\_filter\_wp_title 后错误就消失，大概是函数名已然被占用。

## 扩展阅读：

  1. [http://codex.wordpress.org/Function\_Reference/wp\_title][1]
  2. [http://codex.wordpress.org/Plugin\_API/Filter\_Reference/wp_title][2]
  3. <http://www.kutailang.com/wordpress/158.html/>

 [1]: http://codex.wordpress.org/Function_Reference/wp_title
 [2]: http://codex.wordpress.org/Plugin_API/Filter_Reference/wp_title