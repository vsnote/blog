---
title: WordPress 使用 Markdown 语法
author: 陈 三
layout: post
date: 2012-09-28T16:59:07+00:00
url: /wordpress-markdown.html
views:
  - 3088
dsq_thread_id:
  - 863650636
categories:
  - WordPress
tags:
  - Markdown
  - Wordpress

---
现在很多网站都支持 [Markdown][1] 语法，比如 StackOverflow，tumblr。WordPress 官方目前没有提供 Markdown 支持，不过 WordPress 扩展性很强，有插件可以使用。

我安装的这个 WordPress 插件叫 PHP Markdown，安装很简单：

  1. 首先从[它的网站][2]下载 zip 压缩包
  2. 登录 WordPress 后台
  3. 选择 插件 -> 新插件
  4. 选择下载的 zip 包，安装并启用插件
  5. 此后新建的 post 及 page 的内容区域都将默认使用 Markdown 语法

PHP Markdown 所应用的 Markdown 语法是忠于原语法的，更加适用平时仅仅是写作的人们使用。而如果要处理其他，比如很多代码，则会带来一些麻烦。譬如我要在 post 里输入代码，则需要按四个空格或一个 Tab 缩进来表示，这还算好，如果要在列表里输入代码呢？需要空出八个空格或两个 Tab 缩进来表示。当然，我可以用 wp-sytax 这样的代码高亮工具管理，但这是题外话。

也因此，上面介绍的这款插件其实还有加强版的，[PHP Markdown Extra][3]。在这个加强版里，可以做到很多超出 Markdown 默认语法的东西，比如，可以给标题加 id：

    ##这是用 Markdown 语法写的标题二 {#markdown}
    

转换成 html 后是下面这样：

    <h2 id="markdown">这是用 Markdown 语法写的标题二</h2>
    

不过，目前这种用法仅限于标题。

另外，代码块还可以使用上下两条波浪线包围，注意它们的数量必须大于或等于 3,并且上下两条线数量要一致：

    ~~~
    ~~~
    

而如果是表格，可以使用以下格式，而不用直接书写 table、thead 等一堆 HTML 代码：

    语文|英语|数学
    ---|---|----
    80|90|100
    

结果是如下表格：

<table class="table table-bordered table-striped table-condensed">
  <tr>
    <th>
      语文
    </th>
    
    <th>
      英语
    </th>
    
    <th>
      数学
    </th>
  </tr>
  
  <tr>
    <td>
      80
    </td>
    
    <td>
      90
    </td>
    
    <td>
      100
    </td>
  </tr>
</table>

比直接书写 table 的代码快捷。

这样，很多时候，我甚至不用启动 [vim + zencoding.vim 写 html 代码][4]。

附一张用 Markdown 写的这篇 blog 的截图，这比满屏的 html 代码可读性强多了：

<img src="http://www.zfanw.com/blog/wp-content/uploads/2012/09/Screenshot-from-2012-09-28-231357.png" alt="php markdown 内容" width="590" />

**Update**：2014.8.28 发现评论区域也可以使用 Markdown。

## 扩展阅读

  1. [markdown 的各种实施][5]

 [1]: http://daringfireball.net/projects/markdown/
 [2]: http://michelf.ca/projects/php-markdown/
 [3]: http://michelf.ca/projects/php-markdown/extra/
 [4]: http://www.zfanw.com/blog/zencoding-vim-tutorial-chinese.html
 [5]: http://en.wikipedia.org/wiki/List_of_Markdown_implementations