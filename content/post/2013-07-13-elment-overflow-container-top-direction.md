---
title: 伸出包含块的子元素
author: 陈 三
layout: post
date: 2013-07-13T15:40:50+00:00
url: /elment-overflow-container-top-direction.html
dsq_thread_id:
  - 1498284657
views:
  - 597
categories:
  - 前端开发
tags:
  - css
  - ie6
  - 怪异用法

---
一个菜单栏中，突出当前菜单项的背景色是很常见的：

<ul class="nav-menu clearfix">
  <li class="nav-menu__item active">
    <a href="">第一个</a>
  </li>
  <li class="nav-menu__item">
    <a href="">我第二</a>
  </li>
</ul>



如果要求当前菜单项的背景伸出父元素顶部1像素又如何？

先来看上例的代码：

    <ul class="nav-menu clearfix">
        <li class="nav-menu__item active"><a href="">第一个</a></li>
        <li class="nav-menu__item"><a href="">我第二</a></li>
    </ul>
    
    <style>
        .nav-menu{
            background:#0175cc;
            height:28px;
        }
        .nav-menu__item{
            float:left;
            font-size:14px;
            line-height:2;
            margin:0 10px;
            list-style:none;
            text-align:center;
        }
        .nav-menu__item a{
            float:left;
            background:#333;
            color:#fff;
            padding:0 10px;
        }
        .nav-menu__item.active a{
            background:red;
        }
    </style>
    

  * 给 a 元素添加1像素的顶部边框：
    
        .nav-menu__item a {border-top:1px solid #fff;}
        
    
    因为 a 的高度超出父元素，父元素默认 `overflow` 的内容可见，所以呈现的结果如下：

<ul class="nav-menu2 clearfix">
  <li class="nav-menu2__item active">
    <a href="">第一个</a>
  </li>
  <li class="nav-menu2__item">
    <a href="">我第二</a>
  </li>
</ul>



  * 把 a 元素向上偏移1像素
    
    这里我们通过 `position:relative` 来提升 a 元素的位置：
    
        .nav-menu__item a {position:relative;top:-1px;}
        
    
    因为边框颜色是白的，与大包含块背景色一样，所以我们看不到顶部边框，如下：

<ul class="nav-menu3 clearfix">
  <li class="nav-menu3__item active">
    <a href="">第一个</a>
  </li>
  <li class="nav-menu3__item">
    <a href="">我第二</a>
  </li>
</ul>



  * 修改当前菜单项的顶部边框颜色
    
        .nav-menu__item.active a {border-top-color:red;}
        

<ul class="nav-menu4 clearfix">
  <li class="nav-menu4__item nav-menu4__item-active">
    <a href="">第一个</a>
  </li>
  <li class="nav-menu4__item">
    <a href="">我第二</a>
  </li>
</ul>



于是子元素就伸出父元素顶部1像素。

因为 IE6 会[自动扩展包含块的高度][1]，所以上述方法如果要兼容 IE6,需要多做一个处理：

    .lt-ie7 .nav-menu__item{height:28px;overflow:hidden;}
    

`.lt-ie7` 的用法来自 [HTML5Boilerplate][2]

完整的代码如下：

    <ul class="nav-menu clearfix">
        <li class="nav-menu__item active"><a href="">第一个</a></li>
        <li class="nav-menu__item"><a href="">我第二</a></li>
    </ul>
    
    <style>
        .nav-menu{
            background:#0175cc;
            height:28px;
        }
        .nav-menu__item{
            float:left;
            font-size:14px;
            line-height:2;
            margin:0 10px;
            list-style:none;
            text-align:center;
        }
        .lt-ie7 .nav-menu__item{
            height: 28px;
            overflow: hidden;
        }
        .nav-menu__item a{
            float:left;
            background:#333;
            color:#fff;
            padding:0 10px;
            border-top:1px solid #fff;
            position: relative;
            top:-1px;
        }
        .nav-menu__item.active a{
            background:red;
            border-top-color: red;
        }
    </style>
    

效果如下：

<ul class="nav-menu-ie6 clearfix">
  <li class="nav-menu-ie6__item active">
    <a href="">第一个</a>
  </li>
  <li class="nav-menu-ie6__item">
    <a href="">我第二</a>
  </li>
</ul>



附：<a href="http://www.zfanw.com/demo/ie6-expanding.html" rel="nofollow" title="IE6 自动扩展包含块高度">Demo</a>

 [1]: http://www.positioniseverything.net/explorer/expandingboxbug.html
 [2]: https://github.com/h5bp/html5-boilerplate/blob/master/index.html