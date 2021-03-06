---
title: 博客改版
author: 陈 三
layout: post
date: 2015-05-02T10:43:34+00:00
url: /blog-change-again.html
views:
  - 497
categories:
  - 未分类

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 颜色</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 导航菜单</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-3"><span class="toc_number toc_depth_1">3</span> 翻页</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-4"><span class="toc_number toc_depth_1">4</span> 列表的分类</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-5"><span class="toc_number toc_depth_1">5</span> 移动端的几个问题</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    ​我是长期从事前端开发一块的，用户体验以及设计两块，基本属于”人云亦云“的水平。但那句话说，没见过猪跑，还没吃过猪肉吗？所以这一次的博客改版，​​想特地写一篇。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">颜色</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    我不是色盲，但很难说我用得好色彩 &#8211; 因为基础全无 &#8211; 一个非常糟糕的理由。好在 Google Material Design 有<a href="http://www.google.com/design/spec/style/color.html">色彩一块</a>说明，所以这次基本是基于它的指导：选三种主色，然后加一个强调色。
  </p>
  
  <p>
    链接颜色基本使用蓝色，主要出于<a href="http://www.nngroup.com/articles/guidelines-for-visualizing-links/">用户可用性</a>上的考量。内容区域的链接有加轻薄的下划线 &#8211; 值也是参照 Material Design，rgba(0, 0, 0, .12)。因为我不再支持 IE10 以下的 IE 浏览器，所以对于 IE8 不支持 <code>rgba</code> 的情况也没做备选方案。
  </p>
  
  <p>
    顶部面包屑导航区，会根据所处页面类型更换背景色 &#8211; 本意是出于区分，比如<strong>分类</strong>页、<strong>内容</strong>页，但其实用户记不住这些，所以只是为了好玩。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">导航菜单</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    此前的菜单是基于 Bootstrap 做的，中规中矩，移动设备上会收起来，然后点击一个菜单键下拉出来。这次换成抽屉式的，目下也是成风了。不过因为用到 CSS3 的 transition，所以<a href="http://caniuse.com/#feat=css-transitions">不支持 IE10 以下</a>，好在我已经<strong>宣称过</strong>不支持 IE10 以下了 &#8211; Google 的准则是，仅支持各大浏览器最新两个版本，比如 IE 出到 11，它的网站就支持到 IE10。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-3">翻页</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-3" href="#i-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    翻页的设计，基本抄自 <a href="https://www.google.com/intl/zh-CN_ALL/trends/2014/story/tv.html">Google Trends</a>，当然，CSS 是自己写的，CSS 类的命名则遵循 <a href="https://en.bem.info/">BEM</a>。
  </p>
  
  <p>
    翻页上有一个小小细节。一开始，我是用<strong>上一页</strong>、<strong>下一页</strong>这样的字眼，后来想想，这样对突然闯入的阅读者来说没有任何意义 &#8211; 她根本不知道上是哪里、下又是什么。于是换成了[旧一页]、[新一页]，揉合了时间概念。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-4">列表的分类</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-4" href="#i-4"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    在首页上，原先每一条标题下并没有加入文章所属的分类，后来加入了，是觉得一个标题、时间以及有时有有时没有的摘选不足以帮助用户定位一条信息是否是她想点进去的。希望分类能增加一点信息量，帮助用户下决心点下去还是不点。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-5">移动端的几个问题</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-5" href="#i-5"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    [resp_image id=&#8217;15800&#8242; caption=&#8221; ]
  </p>
  
  <p>
    上面的截图里有两个问题：
  </p>
  
  <ol>
    <li>
      顶部面包屑被截断 &#8211; 因为标题太长了，目前没有什么好的解决办法，只能粗暴截断
    </li>
    <li>
      底部的上、下文章链接高度不一，这个目前也没什么好的解决办法
    </li>
  </ol>
  
  <p>
    还有一个问题，也是移动端上有的，就是左侧抽屉拉出来后，会导致已经滚动了某些距离的页面重新滚回顶部。这个是因为抽屉出来后，动态设置了 <code>html</code> 及 <code>body</code> 的高度导致的，Google Trends 页面同样有这个问题。
  </p>
</div>