---
title: Magento 幻灯片
author: 陈 三
layout: post
date: 2012-08-01T08:15:02+00:00
url: /magento-slideshow.html
views:
  - 1077
dsq_thread_id:
  - 788046435
categories:
  - 未分类
tags:
  - Magento
  - Slider

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_jQuery"><span class="toc_number toc_depth_1">1</span> 添加 jQuery</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_Craftyslide"><span class="toc_number toc_depth_1">2</span> 引用 Craftyslide 相关文件</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">3</span> 添加幻灯片内容</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">4</span> 执行幻灯片效果</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    如果要在 Magento 主页上添加幻灯片（slideshow）效果，技术上也是比较简单的。这一节所用的材料如下：
  </p>
  
  <ol>
    <li>
      <a href="http://docs.jquery.com/Downloading_jQuery">jQuery</a>
    </li>
    <li>
      <a href="http://projects.craftedpixelz.co.uk/craftyslide/">Craftyslide</a>
    </li>
  </ol>
  
  <p>
    注：jQuery 有许多做幻灯片的插件，Craftyslide 只是一例。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_jQuery">添加 jQuery</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_jQuery" href="#_jQuery"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    首先，需要给 Magento 的主页添加 jQuery 支持，按照<a href="http://www.zfanw.com/blog/magento-add-jquery-support.html">给 Magento 添加 jQuery</a> 一篇中的说明，打开 CMS -> Pages -> Home page，将下段代码添加到 Design 标签下的 Layout Update XML 里：
  </p>
  
  <pre><code>&lt;reference name="head"&gt;
   &lt;action method="addItem"&gt;
       &lt;type&gt;skin_js&lt;/type&gt;
       &lt;name&gt;js/jquery.js&lt;/name&gt;
   &lt;/action&gt;
&lt;/reference&gt;
</code></pre>
  
  <h2 class="storycontent-h2">
    <span id="_Craftyslide">引用 Craftyslide 相关文件</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Craftyslide" href="#_Craftyslide"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    下载 Craftyslide，然后将相应文件解压到相应位置，然后在上面一个步骤代码中加入如下内容：
  </p>
  
  <p>
    <action method="addItem"> <type>skin_js</type> <name>js/craftyslide/js/craftyslide.js</name> </action> <action method="addItem"> <type>skin_css</type> <name>css/craftyslide.css</name> </action>
  </p>
  
  <p>
    这样我们在主页里调用 craftyslide 的 js 文件，并应用它的样式。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">添加幻灯片内容</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    然后该是添加幻灯片内容。打开 Home page 页，在 Content 中添加如下：
  </p>
  
  <pre><code>&lt;div id="slideshow"&gt;
&lt;ul&gt;
&lt;li&gt;&lt;img src="{{skin url='images/slider/nemo.jpg'}}" alt="" /&gt;&lt;/li&gt;
&lt;li&gt;&lt;a href="http://www.zfanw.com/blog"&gt;&lt;img title="#htmlcaption" src="{{skin url='images/slider/toystory.jpg'}}" alt="" /&gt;&lt;/a&gt;&lt;/li&gt;
&lt;li&gt;&lt;img title="This is an example of a caption" src="{{skin url=images/slider/up.jpg}}" alt="" /&gt;&lt;/li&gt;
&lt;li&gt;&lt;img src="{{skin url='images/slider/walle.jpg}}" alt="" /&gt;&lt;/li&gt;
&lt;/ul&gt;
&lt;/div&gt;
</code></pre>
  
  <h2 class="storycontent-h2">
    <span id="i-2">执行幻灯片效果</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    根据插件的使用说明，可以新建一个 slideshow.js 文件，用于执行幻灯片效果，内容如下：
  </p>
  
  <pre><code>var $j=jQuery.noConflict();
$j(window).load(function() {
    $j("#slideshow").craftyslide();
});
</code></pre>
  
  <p>
    然后在1步骤的 reference 里添加如下：
  </p>
  
  <p>
    <action method="addItem"> <type>skin_js</type> <name>js/craftyslide/slideshow.js</name> </action>
  </p>
  
  <p>
    这样就可以在主页调用该执行代码。
  </p>
  
  <p>
    保存后再刷新网页，已经有下图中的幻灯片效果：
  </p>
  
  <p>
    <a href="http://www.zfanw.com/blog/wp-content/uploads/2012/08/slideshow.png"><img src="http://www.zfanw.com/blog/wp-content/uploads/2012/08/slideshow-300x223.png" alt="Magento 幻灯片" title="slideshow" width="300" class="alignnone size-medium wp-image-4618" srcset="https://www.zfanw.com/blog/wp-content/uploads/2012/08/slideshow-300x223.png 300w, https://www.zfanw.com/blog/wp-content/uploads/2012/08/slideshow.png 686w" sizes="(max-width: 300px) 100vw, 300px" /></a>
  </p>
  
  <p>
    当然，上面的方法是直接把幻灯片内容代码写入 Magento 主页内容中，也可以创建一个 Static Blocks，然后再从主页内容里以如下形式引入静态块：
  </p>
  
  <pre><code>{{block type="cms/block" block_id="slider-show"}}
</code></pre>
  
  <p>
    这个就看个人喜好了。
  </p>
</div>