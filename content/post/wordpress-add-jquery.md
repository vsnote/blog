---
title: WordPress 引用 jQuery
author: 陈 三
layout: post
date: 2012-08-06T12:56:54+00:00
url: /wordpress-add-jquery.html
views:
  - 1845
dsq_thread_id:
  - 796896311
categories:
  - WordPress
tags:
  - jQuery
  - Wordpress

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 方法</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 时机</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-3"><span class="toc_number toc_depth_1">3</span> 参考</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    WordPress 安装文件中默认包含有 jQuery 库，因此如果要引用 jQuery，可以直接引用安装文件中（在 wp-includes/js/jquery/ 文件夹下）的 jquery.js，也可以使用 Google 等 CDN 提供的 &#8211; 它们间的区别仅在于安装文件中的 jquery.js 在文件最后加了一行：
  </p>
  
  <pre><code>jQuery.noConflict()
</code></pre>
  
  <p>
    该语句用于保证 WordPress 下 jQuery 库与其他库如 prototype.js 的兼容。
  </p>
  
  <p>
    但无论是哪种引用方法，WordPress 都不推荐使用硬编码的方式，那样一来可能导致库文件多次载入，二来无法处理代码间的依存关系。所以，WordPress 推荐使用 wp_enqueue_script() 函数。注：以下代码均需写入 functions.php 文件。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">方法</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    简单的用法如下：
  </p>
  
  <pre><code>wp_enqueue_script('jquery');
</code></pre>
  
  <p>
    而如果要从 Google 的 CDN 上引用：
  </p>
  
  <pre><code>wp_deregister_script( 'jquery' );
wp_register_script( 'jquery', 'http://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js');
wp_enqueue_script( 'jquery' );
</code></pre>
  
  <p>
    先在 WordPress 中取消注册 jquery，然后将其注册到 googleapis 上的地址，最后再引用。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">时机</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    上面讲的是 WordPress 引用 jQuery 的方法，这里讲的是时机，即什么情况下引用 jQuery。
  </p>
  
  <h3>
    1. 前台页面引用
  </h3>
  
  <p>
    wp_enqueue_scripts 是一个 WordPress action（动作），可以保证仅在前台页面里引用 jquery。用法如下：
  </p>
  
  <pre><code>&lt;?php
function add_jquery_support() {
    wp_deregister_script( 'jquery' );
    wp_register_script( 'jquery', 'http://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js');
    wp_enqueue_script( 'jquery' );
}    
add_action('wp_enqueue_scripts', 'add_jquery_support');
?&gt;
</code></pre>
  
  <h3>
    2. 后台引用
  </h3>
  
  <p>
    使用 admin_enqueue_scripts 动作勾子，用法同上。但这个要谨慎使用，因为可能造成后台管理功能或插件功能的丢失。
  </p>
  
  <h3>
    3. 针对某些页面引用
  </h3>
  
  <p>
    比如，在创建新的主题时，可能会在后台增加一个管理页面，用于设置一些选项(options)，那么，我们可能想只针对这个页面引用 jquery 及其他脚本。
  </p>
  
  <pre><code>&lt;?php
add_action('admin_menu', 'create_theme_options_menu');
function create_theme_options_menu() {  
    $themepage=add_theme_page('Theme Options', 'Theme Options', 'administrator', __FILE__, 'build_options_page');
    add_action('admin_print_styles-' . $themepage, 'my_theme_admin_styles');
}
function my_theme_admin_styles(){
    wp_enqueue_script('media-upload');
        wp_enqueue_script('thickbox');
        wp_enqueue_script('jquery');
        wp_enqueue_style('thickbox');
        wp_enqueue_script('farbtastic');
        wp_enqueue_style('farbtastic');
        wp_enqueue_script(//加载 jQuery 运行函数
        'color-picker-script', get_template_directory_uri() . '/js/colorpicker.js', array (
            'farbtastic',
            'jquery'
        ));
}
</code></pre>
  
  <p>
    上面的代码在 WordPress 后台 Appearance 下生成一个 Theme options 管理页面，并且仅在该页面加载上面代码列出的脚本。这样就不会对其他管理页面造成未知的影响了。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-3">参考</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-3" href="#i-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <a href="http://codex.wordpress.org/Function_Reference/wp_enqueue_script">http://codex.wordpress.org/Function_Reference/wp_enqueue_script</a>
    </li>
    <li>
      <a href="http://codex.wordpress.org/Function_Reference/add_theme_page">add_theme_page</a>
    </li>
  </ol>
</div>