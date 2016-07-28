---
title: Magento 添加 jQuery 支持
author: 陈 三
layout: post
date: 2012-07-27T14:59:36+00:00
url: /magento-add-jquery-support.html
views:
  - 1407
dsq_thread_id:
  - 783950081
categories:
  - 未分类
tags:
  - Magento

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#addJs"><span class="toc_number toc_depth_1">1</span> addJs 方法</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#addItem"><span class="toc_number toc_depth_1">2</span> addItem 方法</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_headphtml"><span class="toc_number toc_depth_1">3</span> 硬编码 head.phtml</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    Magento 添加 jQuery 有许多办法，可以硬编码到 head.phtml，但也有些灵活用法。以下说几个灵活的应用法。
  </p>
  
  <p>
    假设 magento 安装在 本地 htdocs/chenxsan 目录下，新的模板文件夹名称为 lan，则先在 lan/layout/ 文件夹下新建一个 local.xml 文件：
  </p>
  
  <h2 class="storycontent-h2">
    <span id="addJs">addJs 方法</span><a title="标题链接地址" class="u-floatRight hidden" id="heyaddJs" href="#addJs"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    首先将 jquery.js 添加到 chenxsan/js/ 目录下，然后在 local.xml 中添加如下语句：
  </p>
  
  <pre><code>&lt;reference name="head"&gt;
    &lt;action method="addJs"&gt;&lt;script&gt;jquery.js&lt;/script&gt;&lt;/action&gt;
&lt;/reference&gt;
</code></pre>
  
  <p>
    刷新网页，查看源代码，里面已经添加 jquery.js：
  </p>
  
  <pre><code>&lt;script type="text/javascript" src="http://localhost/chenxsan/js/jquery.js"&gt;
&lt;/script&gt;
</code></pre>
  
  <p>
    这种用法觉见于多主题里都要调用 jQuery 的情况。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="addItem">addItem 方法</span><a title="标题链接地址" class="u-floatRight hidden" id="heyaddItem" href="#addItem"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    首先将 jquery.js 添加到 chenxsan/skin/frontend/default/lan/js/ 目录下，然后在 local.xml 文件添加以下语句：
  </p>
  
  <pre><code>&lt;reference name="head"&gt;
   &lt;action method="addItem"&gt;
       &lt;type&gt;skin_js&lt;/type&gt;
       &lt;name&gt;js/jquery.js&lt;/name&gt;
   &lt;/action&gt;
&lt;/reference&gt;
</code></pre>
  
  <p>
    刷新网页，查看源代码：
  </p>
  
  <pre><code>&lt;script type="text/javascript" src="http://localhost/chenxsan/skin/frontend/default/lan/js/jquery.js"&gt;
&lt;/script&gt;
</code></pre>
  
  <p>
    因为 Magento 本身引用 prototype js 库，也使用 $，这会造成与 jQuery 语句的冲突，为解决这冲突，在所写的 js 代码前需要引入 noConflict() ：
  </p>
  
  <pre><code>jQuery.noConflict();
 jQuery(document).ready(function(){
    //code here
  });
</code></pre>
  
  <p>
    如果嫌 jQuery 这样太长，则可以这样写：
  </p>
  
  <pre><code>var $j = jQuery.noConflict();
    $j(document).ready(function(){
   //code here
});
</code></pre>
  
  <p>
    这样，你如果要 extjs 的话，则可以放心使用 $ 了。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_headphtml">硬编码 head.phtml</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_headphtml" href="#_headphtml"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    最后再提个硬编码到 template/page/html/head.phtml 文件的办法。
  </p>
  
  <p>
    直接在合适的位置加入下列语句：
  </p>
  
  <pre><code>&lt;script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1/jquery.js"&gt;
&lt;/script&gt;
</code></pre>
  
  <p>
    以上所说的办法是将 jQuery 添加到网站前端整站，如果要针对特定的 CMS 页面 引用 jQuery，则请到后台管理的 CMS -> Pages -> Design -> Page Layout 下 “Layout Update XML” 里设置。又或要针对分类进行设置，也可以在 Catalog -> Manage categories -> Custom Design 下的 &#8220;Custom Layout Update&#8221; 下添加。
  </p>
</div>