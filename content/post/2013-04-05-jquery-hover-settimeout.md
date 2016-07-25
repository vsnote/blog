---
title: jQuery hover 延迟
author: 陈 三
layout: post
date: 2013-04-05T14:36:04+00:00
url: /jquery-hover-settimeout.html
dsq_thread_id:
  - 1188776174
views:
  - 726
categories:
  - 前端开发
tags:
  - JavaScript
  - jQuery

---
在网页制作里，经常会有这样的需求：鼠标滑入 A 区域，显示 B 内容，滑出 A 后隐藏 B 内容。

举个简单例子，制作导航条子菜单。

    <ul class="navigation">
        <li>Home
            <ul class="sub-menu">
                <li>陈三</li>
                <li>陈四</li>
                <li>陈五</li>
            </ul>
        </li>
        <li>关于</li>
    </ul>
    

`ul.sub-menu` 部分通过 `display:none` 隐藏，之后通过 li:hover 来显示，并且鼠标可以移入 `.sub-menu` 部分。

具体 CSS 规则及代码效果见 [jsfiddle 示例][1]。

上一个例子中，`ul.sub-menu` 包含在 li 标签对中，所以代码很顺当，不会有什么问题。

再来看一个 <a href="http://www.zfanw.com/demo/jquery-hover/index.html" title="jQuery hover 鼠标滑入滑出显示/隐藏内容" rel="nofollow">demo</a>。

这是另一个常见需要：鼠标滑入 A 区域显示 B 内容，鼠标滑出 A 区域且没有滑入 B 区域则隐藏 B；如果鼠标滑出 A 区域且滑入 B 区域，则 B 仍显示。

考虑到 IE6 会[自动扩展包含块高度][2]，一般来说，要显示的区域与触发区域在 HTML 结构上要处于兄弟关系。

比如 demo 中：

    <div class="yui3-u-1-3 share-btn">
        <div class="share-btn--hover-me">
            <a class="share-btn__sns" title="" href="#">
                <img src="img/share-btn/sina-qq-small.png" alt="分享到社交网站" width="65" height="16">
            </a>
            <a class="share-btn__weixin" title="" href="#">
                <img src="img/share-btn/weixin-small.png" alt="" width="16" height="16">
            </a>
        </div>
        <ul class="share-btn__sns-list is-hide"> <!-- 我与触发区域是平行关系 -->
            <li>
                关注某站
            </li>
            <li>
                关注某站
            </li>
            <li>
                关注某站
            </li>
        </ul>                               
    </div>
    

配合上述 HTML 结构，JavaScript 代码是这样写的：

    $(function () {
    //鼠标滑入 显示;;;;;分享到社交网站 鼠标滑出 隐藏
    (function () {
        var t; //设置定时器
        var hoverMe = $('.share-btn__sns'),
            pop = $('.share-btn__sns-list');
        hoverMe.on('mouseenter', function () { // 鼠标进入触发区域，显示内容
            clearTimeout(t);
            pop.slideDown();
        });
        hoverMe.on('mouseleave', function () { // 鼠标滑出触发区域，定时 0.5 秒后隐藏内容
            t = setTimeout(function () {
                pop.slideUp();
            }, 500);
        });
        pop.on('mouseenter', function () { // 鼠标进入弹出块，则清除定时函数，不再触发
            clearTimeout(t);
        });
        pop.on('mouseleave', function () { // 鼠标滑出弹出块，则隐藏弹出块
            pop.slideUp();
        });
    }());
    
    });
    

这个代码写得有点长，mouseenter、mouseleave 其实可以用 [jQuery hover][3] 合并。

经过 setTimeout 处理，两个元素相隔很远也可以触发，并且保证点击得到另一个元素。

 [1]: http://jsfiddle.net/chenxsan/fCKrT/
 [2]: http://www.zfanw.com/blog/elment-overflow-container-top-direction.html
 [3]: http://api.jquery.com/hover/