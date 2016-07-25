---
title: WordPress 代码高亮插件 Highlight.js
author: 陈 三
layout: post
date: 2013-04-24T23:40:46+00:00
url: /wordpress-plugin-syntax-highlight-js.html
dsq_thread_id:
  - 1234000893
views:
  - 938
categories:
  - WordPress
tags:
  - highlight.js
  - Wordpress
  - 插件

---
[Highlight.js][1] 支持71种程序代码的语法高亮，提供[44种样式][2]及各种[扩展插件][3]，其中包括 [WordPress 插件][4]。

但用 WordPress 插件做**代码高亮**时，[Google PageSpeed 测试中][5]，会出现如下建议：

> The following external CSS files were included after an external JavaScript file in http://www.zfanw.com/blog/wordpress-add-jquery.html. To ensure CSS files are downloaded in parallel, always include external CSS before external JavaScript.
> 
> http://www.zfanw.com/blog/wp-content/plugins/wp-highlightjs/styles/default.css

Highlight.js 插件将 CSS 文件附加到 JS 文件后，并且插件设置中没有提供任何调整顺序的选项。这会导致 CSS 文件不能并行请求。

* * *

类似于 Google 提供的第三方库 CDN 服务，Yandex(俄罗斯的搜索引擎) 也有提供[类似的公共服务][6]，并且有 highlight.js，我可以在 WordPress 里直接引用 highlight 的 js 与 css 文件，文件出现的顺序就变得可控。

打开 WordPress 的 functions.php 文件，加入如下代码：

    <?php
        function zfanw_add_highlight_js(){
            wp_enqueue_style('highlightcss','http://yandex.st/highlightjs/8.0/styles/default.min.css');
            wp_enqueue_script('highlightjs','http://yandex.st/highlightjs/8.0/highlight.min.js',array(),null,true);
        }
        add_action('wp_enqueue_scripts', 'zfanw_add_highlight_js');
    ?>
    

最后在 Footer.php 或 Header.php 文件中触发：

    <script>hljs.initHighlightingOnLoad();</script>
    

保存后，highlight.js 会查找页面内的代码片段，自动判断语言类型，并根据 CSS 样式主题高亮显示不同语法。如本页面所示的代码样式。

如果要换掉代码高亮的样式主题，则只要将调用的 CSS 路径替换掉即可，比如，要从默认主题换成 Zenburn 主题：

     wp_enqueue_style('highlightcss','http://yandex.st/highlightjs/8.0/styles/zenburn.min.css');
    

## 参考

  1. [highlight.js 说明][7]
  2. [wp\_enqueue\_script][8]

 [1]: http://highlightjs.org/
 [2]: http://highlightjs.org/static/test.html
 [3]: http://softwaremaniacs.org/soft/highlight/en/addons/
 [4]: http://wordpress.org/extend/plugins/wp-highlightjs/
 [5]: https://developers.google.com/speed/pagespeed/insights
 [6]: http://api.yandex.ru/jslibs/libs.xml
 [7]: https://github.com/isagalaev/highlight.js
 [8]: https://codex.wordpress.org/Function_Reference/wp_enqueue_script