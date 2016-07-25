---
title: Firefox 收藏的秘密
author: 陈 三
layout: post
date: 2013-02-20T23:38:26+00:00
url: /firefox-keyword-search.html
views:
  - 1101
dsq_thread_id:
  - 1095697173
categories:
  - Firefox
  - Ubuntu
  - vimperator
tags:
  - Firefox
  - vimperator

---
Firefox 下，收藏页面可以通过「书签」菜单，或直接按 <kbd>Ctrl-D</kbd>，或点击地址栏右侧的**星星**来收藏，前两种方法中，firefox 会弹出对话框，如下：

<div id="attachment_8155" style="width: 310px" class="wp-caption alignnone">
  <a href="https://www.zfanw.com/blog/wp-content/uploads/2013/02/firefox-bookmark-webpage1.jpg"><img src="https://www.zfanw.com/blog/wp-content/uploads/2013/02/firefox-bookmark-webpage1-300x187.jpg" alt="firefox 收藏网页对话框" width="300" height="187" class="size-medium wp-image-8155" srcset="https://www.zfanw.com/blog/wp-content/uploads/2013/02/firefox-bookmark-webpage1-300x187.jpg 300w, https://www.zfanw.com/blog/wp-content/uploads/2013/02/firefox-bookmark-webpage1.jpg 331w" sizes="(max-width: 300px) 100vw, 300px" /></a>
  
  <p class="wp-caption-text">
    图1
  </p>
</div>

Tags 部分表示页面标签，可填可不填，填写的话，可以方便后期检索。

除此之外，firefox 其实还有一种收藏页面的方式，不过与上面所述方法有所不同，如下：

<div id="attachment_8022" style="width: 310px" class="wp-caption alignnone">
  <a href="https://www.zfanw.com/blog/wp-content/uploads/2013/02/Screenshot-from-2013-02-16-225505.png"><img src="https://www.zfanw.com/blog/wp-content/uploads/2013/02/Screenshot-from-2013-02-16-225505-300x124.png" alt="firefox 收藏 关键字" width="300" height="124" class="alignnone size-medium wp-image-8022" srcset="https://www.zfanw.com/blog/wp-content/uploads/2013/02/Screenshot-from-2013-02-16-225505-300x124.png 300w, https://www.zfanw.com/blog/wp-content/uploads/2013/02/Screenshot-from-2013-02-16-225505.png 400w" sizes="(max-width: 300px) 100vw, 300px" /></a>
  
  <p class="wp-caption-text">
    图2
  </p>
</div>

图2中显示的这个对话框，是右击我的博客的搜索框后，选择弹出菜单中的 「Add a Keyword for this Search&#8230;」 菜单项后出来的。可以看到，对话框的标题为 &#8220;New Bookmark&#8221;。

在 &#8220;Keyword&#8221; 框中填入你要设置的**关键字**，比如，zf。之后按 <kbd>Alt-D</kbd> 或按 <kbd>Ctrl-L</kbd> 或通过鼠标聚焦 [firefox 的导航栏][1]，然后输入 「zf firefox」 就可以搜索博客中带有 「firefox」 关键词的文章，如图3：

<div id="attachment_8031" style="width: 310px" class="wp-caption alignnone">
  <a href="https://www.zfanw.com/blog/wp-content/uploads/2013/02/firefox-awesome-bar-search1.jpg"><img src="https://www.zfanw.com/blog/wp-content/uploads/2013/02/firefox-awesome-bar-search1-300x134.jpg" alt="firefox 导航栏自动补齐搜索" width="300" height="134" class="alignnone size-medium wp-image-8031" srcset="https://www.zfanw.com/blog/wp-content/uploads/2013/02/firefox-awesome-bar-search1-300x134.jpg 300w, https://www.zfanw.com/blog/wp-content/uploads/2013/02/firefox-awesome-bar-search1.jpg 313w" sizes="(max-width: 300px) 100vw, 300px" /></a>
  
  <p class="wp-caption-text">
    图3
  </p>
</div>

在上面，我强调说，这种方法是别一种**收藏页面**的方法，因为我们可以从书签管理中找到第二种方法收藏的链接，如下所示，在侧边栏中打开书签管理并搜索：

<div style="width: 285px" class="wp-caption alignnone">
  <a href="https://www.zfanw.com/blog/wp-content/uploads/2013/02/firefox-bookmark-search.jpg"><img src="https://www.zfanw.com/blog/wp-content/uploads/2013/02/firefox-bookmark-search.jpg" alt="firefox 书签管理" width="275" height="194" class="alignnone size-full wp-image-8033" /></a>
  
  <p class="wp-caption-text">
    图4
  </p>
</div>

你可以看到，当鼠标放到该链接上时，会浮动出一个 tooltip，显示 Name 与收藏的网址：

    Search 陈三
    http://www.zfanw.com/blog/?s=%s
    

这正是第二种方法收藏的页面路径。

请注意 **%s** 部分。这是 firefox 的 [Keyword search][2] 背后实现。

当我输入 zf firefox&#8221; 时，firefox 其实自动将收藏的网址 &#8220;https://www.zfanw.com/blog/?s=%s&#8221; 中的 「%s」 替换为 &#8220;zf&#8221; 这个关键字空格后的所有内容即 &#8220;firefox&#8221;，也就是说，访问的页面网址实际上变成

    http://www.zfanw.com/blog/?s=firefox
    

这样我们就清楚知道这个功能背后的原理。

当右击搜索框添加关键字保存的页面实现不正常或无法添加关键字时，我们可以自己手动设置收藏地址。

举 Google+ 为例，如果通过 「Add a Keyword for this Search&#8230;」 方法来添加 「gp」 为关键字，保存的链接地址是 &#8220;https://plus.google.com/s/_/search/form?q=%s&#8221;，很不幸，这个搜索网址并不正确。

但我们可以试着输入一两个关键词看看其结构，仍试 &#8220;firefox&#8221;，其链接结构如下：

    https://plus.google.com/s/firefox
    

这样我们就可以将先前收藏的链接地址修改为 &#8220;https://plus.google.com/s/%s&#8221;，之后在导航栏输入 &#8220;gp firefox&#8221; 即可搜索 Google+ 里的 firefox 内容。

通过这种办法，我们实际上可以给 firefox 添加无数的「搜索引擎」，而不仅仅默认的 Google、Bing，又或是通过扩展组件添加的搜索引擎。

如果再配上 Vimperator，则简直行云流水了。

## 参考

  1. [Google+ vimperator 中文社群][3] 及其评论

 [1]: http://support.mozilla.org/en-US/kb/awesome-bar-find-your-bookmarks-history-and-tabs
 [2]: http://kb.mozillazine.org/Using_keyword_searches
 [3]: https://plus.google.com/104787680206754797134/posts/LHrhpc9DS3V