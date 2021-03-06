---
title: jQuery 插件 – Carousel(幻灯片)
author: 陈 三
layout: post
date: 2013-10-08T11:40:52+00:00
url: /jquery-plugin-carousel-slide.html
views:
  - 762
categories:
  - 前端开发
tags:
  - jQuery

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
      <a href="#demo"><span class="toc_number toc_depth_1">2</span> demo</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    不确定这个插件效果是该称作幻灯片还是走马灯或者旋转木马。相对此前写过的几个 jQuery 插件，这个插件相对要复杂些。我也是在写这个插件的过程中，才稍稍明白，计算机里一直说的算法大概是什么 &#8211; 解法有很多种，看我怎么选择。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">代码</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <pre><code>//Module Name: Carousel
//幻灯片效果
//Author: 陈三
//Blog: http:www.zfanw.com/blog/
//Time: 2013.10.01
//version: 1.0
//Dependency: jQuery
;
(function ($) {
    //HTML 结构
    //-div.carousel.js-carousel
    //      +ul.carousel-inner
    //          +li.carousel-item
    //-div.carousel-control
    //      +a.prev
    //      +a.next
    //-ol.carousel-indicators
    //      +li.carousel-indicator.active{$}
    //避免 fouc 现象的 CSS
    //示例：
    //// .carousel-inner{height:260px;overflow:hidden;}
    //// .carousel-item{float:left;}
    //参数
    ////可自定义的参数：
    ////1. 显示的幻灯片数目 showNum 数值型
    ////2. 动画的时间 duration 数值型
    ////3. 是否自动切换 autoSlide 布尔型
    ////4. 自动切换的时间间隔 interval 数值型
    //Bug 列表
    ////1. ie6 下，可能出现 .carousel 的 overflow 失效问题，目前已知给 .carousel 元素设置 position:relative 可以解决
    $.fn.carousel = function (options) {
        var settings = $.extend({
            showNum: 1,
            duration: 400,
            interval: 2000,
            autoSlide: false
        }, options);
        return this.each(function () {
            var that = $(this),
                li = that.children('.carousel-inner').children('.carousel-item'), //将 $('.carousel') 保存到 that 对象中
                //li.css('float', 'left'); //左浮动最好由 CSS 来完成
                itemWidth = li.outerWidth(true), //包含 margin
                itemCount = li.length,
                stage = itemWidth * (settings.showNum),
                currentSlide = 1, //当前 slide，从1开始
                slideMaxIndex = Math.floor(itemCount / (settings.showNum)), //最末一个 slide 的 index 值
                activeIndicator = 0, //当前 slide 图示位置
                indicator = that.siblings('.carousel-indicators').children('.carousel-indicator'),
                next = that.siblings('.carousel-control').children('.next'),
                prev = that.siblings('.carousel-control').children('.prev');
            that.width(stage); //设置舞台宽度，即显示多少个幻灯
            that.children('.carousel-inner').width(itemWidth * itemCount);
            that.css({
                'overflow': 'hidden'
            });
            that.scrollLeft(0); //刷新页面时重置

            function setIndicator(i) {
                indicator.removeClass('active');
                indicator.eq(i).addClass('active');
            }

            function slideNext() {
                if (!(that.is(":animated"))) { //除非动画不在进行中才执行
                    //如果到最末一条
                    var scrollLeftMax = (itemCount - settings.showNum) * itemWidth; //取得可滚动的最大距离
                    if (currentSlide === slideMaxIndex) {
                        that.animate({
                            "scrollLeft": "-" + scrollLeftMax
                        }, settings.duration);
                        currentSlide = 1;
                        setIndicator(currentSlide - 1);
                    } else {
                        that.animate({
                            "scrollLeft": "+=" + (itemWidth * settings.showNum)
                        }, settings.duration);
                        currentSlide++;
                        setIndicator(currentSlide - 1);
                    }
                } //end animated check
            }

            function slidePrev() {
                if (!(that.is(":animated"))) {
                    var scrollLeftMax = (itemCount - settings.showNum) * itemWidth;
                    if (currentSlide === 1) {
                        that.animate({
                            "scrollLeft": scrollLeftMax
                        }, settings.duration);
                        currentSlide = slideMaxIndex;
                        setIndicator(currentSlide - 1);
                    } else {
                        that.animate({
                            "scrollLeft": "-=" + (itemWidth * settings.showNum)
                        }, settings.duration);
                        currentSlide--;
                        setIndicator(currentSlide - 1);
                    }
                }
            }
            next.on('click', function (e) {
                slideNext();
                e.preventDefault();
            });
            prev.on('click', function (e) {
                slidePrev();
                e.preventDefault();
            });
            indicator.on('click', function (e) { //如果要用 mouseenter 事件，则底下判断 animated 的条件需要去除
                var clickIndex = $(this).prevAll().length; //点击了哪个指示图标，从0起
                if (clickIndex &gt; activeIndicator) {
                    if (!(that.is(":animated"))) {
                        that.animate({
                            "scrollLeft": (clickIndex - activeIndicator) * (itemWidth * settings.showNum)
                        }, settings.duration);
                        currentSlide = clickIndex + 1;
                        setIndicator(clickIndex);
                    }
                } else {
                    if (!(that.is(":animated"))) {
                        that.animate({
                            "scrollLeft": -((clickIndex - activeIndicator) * (itemWidth * settings.showNum))
                        }, settings.duration);
                        currentSlide = clickIndex + 1;
                        setIndicator(clickIndex);
                    }
                }
                e.preventDefault();
            });
            (function () { //自动
                if ( !! settings.autoSlide) {
                    var mouse_is_over = false;
                    window.setInterval(function () {
                        if (!mouse_is_over) {
                            slideNext();
                        }
                    }, settings.interval);
                    that.add(prev).add(next).add(indicator).on('mouseenter mouseleave', function (e) {
                        mouse_is_over = e.type === 'mouseenter';
                    });
                }
            }());


        });
    };
}(jQuery));
</code></pre>
  
  <p>
    HTML 代码结构如下：
  </p>
  
  <pre><code>&lt;div class="js-carousel carousel"&gt;
    &lt;ul class="carousel-inner clearfix"&gt;
        &lt;li class="carousel-item"&gt;
            &lt;img src="http://placehold.it/200x200/ff00000" /&gt;
        &lt;/li&gt;
        &lt;li class="carousel-item"&gt;
            &lt;img src="http://placehold.it/200x200/00ff00" /&gt;
        &lt;/li&gt;
        &lt;li class="carousel-item"&gt;
            &lt;img src="http://placehold.it/200x200/0000ff" /&gt;
        &lt;/li&gt;
    &lt;/ul&gt;
&lt;/div&gt;
&lt;div class="carousel-control"&gt; 
 &lt;a class="prev"&gt;上一张&lt;/a&gt;
 &lt;a class="next"&gt;下一张&lt;/a&gt;

&lt;/div&gt;
&lt;ol class="carousel-indicators"&gt;
    &lt;li class="carousel-indicator active"&gt;1&lt;/li&gt;
    &lt;li class="carousel-indicator"&gt;2&lt;/li&gt;
    &lt;li class="carousel-indicator"&gt;3&lt;/li&gt;
&lt;/ol&gt;
</code></pre>
  
  <h2 class="storycontent-h2">
    <span id="demo">demo</span><a title="标题链接地址" class="u-floatRight hidden" id="heydemo" href="#demo"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    <a class="jsbin-embed" href="http://jsbin.com/UNegOX/1/embed?output">JS Bin</a>
  </p>
  
  <p>
    如果你用过其他类似插件，就会发现，我这个插件里需要手动添加的 HTML 代码很多。多数插件是只要我们提供一小段 HTML 就可以的，插件会负责所有的工作，比如通过 js 创建控制按钮、指示图标。但那样的话，同一页面上如果多处使用插件，就会生成一样的结构，一样的 CSS 类，而它们的样式要求往往不一样，那会迫使我们大量使用基于父类的 CSS 选择器 &#8211; 这是我想避免的。
  </p>
  
  <p>
    另外吐槽下幻灯片的一个流行作法。假如幻灯片有三张，那么点击到最后一张时，正常是不能再点了。但流行作法却是返回到第一张，造成一种你怎么点也不会到底的感觉。我个人觉得这种作法体验不好，我们完全可以用一种平缓的方式提醒用户，嘿，你已经点击到最后一张了，再下去就没了。那样会更清晰明白。
  </p>
</div>