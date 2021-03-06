---
title: jQuery 插件 – Tab(选项卡)
author: 陈 三
layout: post
date: 2013-08-26T13:16:02+00:00
excerpt: 一个简单的 jQuery 选项卡插件
url: /jquery-plugin-tab.html
dsq_thread_id:
  - 1745571850
views:
  - 947
categories:
  - 前端开发
tags:
  - jQuery Plugin

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 代码</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 效果</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    我试过不少 jQuery 的 tab(选项卡) 插件，它们多数功能齐全，并且可自定义参数。但除非我去看它们的源代码，否则用起来总像黑盒子，一旦出问题，调试也觉得麻烦，所以干脆自己试手，写一个简单、适用自己项目的选项卡插件。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">代码</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <pre><code>/*===================================
    Module Name: tabview
    默认 hover 触发，可传入 click 事件
    Author: 陈三
    Blog: http:www.zfanw.com/blog/
    Time: 2013.8.6
    version: 1.0
    Dependency: jQuery
    ==================================*/
/*jQuery Plugin*/
//div.js-tabview
//    - ul.tab
//      + li.tab-item&gt;a[data-target="first"]
//      + li.tab-item&gt;a[data-target="second"]
//    - div#first
//    - div#second
;
(function ($) {
    function processing(e) {
    var li = $(this);
    li.siblings('.tab-item').removeClass('on');
    li.siblings('.tab-item').children('a').removeClass('selected');
    li.addClass('on');
    li.children('a').addClass('selected');
    var currentTab = li.children('a').attr('data-target');
    li.closest('.js-tabview').find('div[id]').addClass('is-hide'); //加id是防止误伤其他 div
    $(currentTab).removeClass('is-hide');
    e.preventDefault();
    }
    $.fn.tabview = function (options) {
    var settings = $.extend({
        trigger: "hover"
    }, options);
    return this.each(function () {
        var el = $(this).find('.tab').children('.tab-item').filter(function () {
            return !!$(this).children('a').attr('data-target');
        });
        if (settings.trigger === "hover") {
            el.hover(processing);
        }
        if (settings.trigger === "click") {
            el.click(processing);
        }
    });

    };
}(jQuery));
</code></pre>
  
  <p>
    HTML代码结构如下：
  </p>
  
  <pre><code>&lt;div class="js-tabview"&gt;
    &lt;ul class="tab"&gt;
        &lt;li class="on tab-item"&gt;&lt;a data-target="#tab1" href="" class="selected"&gt;选项卡一&lt;/a&gt;&lt;/li&gt;
        &lt;li class="tab-item"&gt;&lt;a data-target="#tab2" href=""&gt;选项卡二&lt;/a&gt;&lt;/li&gt;
        &lt;li class="tab-item"&gt;&lt;a data-target="#tab3" href=""&gt;选项卡三&lt;/a&gt;&lt;/li&gt;
    &lt;/ul&gt;
    &lt;div id="tab1" class=""&gt;选项卡一对应的内容块&lt;/div&gt;
    &lt;div id="tab2" class="is-hide"&gt;选项卡二对应的内容块&lt;/div&gt;
    &lt;div id="tab3" class="is-hide"&gt;选项卡三对应的内容块&lt;/div&gt;
&lt;/div&gt;
</code></pre>
  
  <p>
    CSS 如下：
  </p>
  
  <pre><code>.is-hide{display:none;}
</code></pre>
  
  <p>
    之所以添加 <code>.is-hide</code>，是为了防止 fouc(<a href="http://en.wikipedia.org/wiki/Flash_of_unstyled_content">flash of unstyled content</a>)，本来 js 中即可完成隐藏元素的结果。
  </p>
  
  <p>
    在页面中引入 jquery 与 tabview 插件后，JavaScript 部分书写如下：
  </p>
  
  <pre><code>$(function(){$('.js-tabview').tabview();});
</code></pre>
  
  <h2 class="storycontent-h2">
    <span id="i-2">效果</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    如下：
  </p>
  
  <div class="js-tabview">
    <ul class="list-unstyled list-inline">
      <li class="on">
        <a href="http://www.zfanw.com/blog/" data-target="#tab1" class="selected">选项卡一</a>
      </li>
      <li>
        <a href="" data-target="#tab2">选项卡二</a>
      </li>
      <li>
        <a href="" data-target="#tab3">选项卡三</a>
      </li>
    </ul>
    
    <div id="tab1" class="" style="background:red;">
      选项卡一对应的内容块
    </div>
    
    <div id="tab2" class="is-hide" style="background:green;">
      选项卡二对应的内容块
    </div>
    
    <div id="tab3" class="is-hide" style="background:orange;">
      选项卡三对应的内容块
    </div>
  </div>
  
  <p>
  </p>
  
  <p>
    插件默认鼠标浮过(hover)触发，也可以传入参数 &#8216;click&#8217; 触发：
  </p>
  
  <pre><code>    $('.js-tabview').tabview({trigger:'click'});
</code></pre>
</div>