---
title: CSS3 flex-basis
author: 陈 三
layout: post
date: 2014-07-13T04:32:46+00:00
url: /css3-flex-basis.html
views:
  - 628
categories:
  - 前端开发
tags:
  - css3
  - 弹性盒模型

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 计算值</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 百分比</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    WebPlatform<fnref target="13071.1" />上对<code>flex-basis</code>的解释是：
  </p>
  
  <blockquote>
    <p>
      The flex-basis CSS property describes the initial main size of the flex item before any free space is distributed according to the flex factors described in the flex property (flex-grow and flex-shrink).
    </p>
  </blockquote>
  
  <p>
    在flex container分配剩余空间前，<code>flex-basis</code>决定flex item在主方向上的大小。
  </p>
  
  <p>
    它的取值有两种<fnref target="13071.2" />：
  </p>
  
  <blockquote>
    <p>
      Percentages refer to the flex container&#8217;s inner main size
    </p>
    
    <p>
      Computed value as specified, with lengths made absolute
    </p>
  </blockquote>
  
  <ol>
    <li>
      百分比 &#8211; 根据flex container的主方向大小计算
    </li>
    <li>
      计算值 &#8211; 绝对数
    </li>
  </ol>
  
  <h2 class="storycontent-h2">
    <span id="i">计算值</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    <code>flex-grow</code>跟<code>flex-shrink</code>取默认值时，计算值的<code>flex-basis</code>类似<code>max-width</code>。
  </p>
  
  <p>
    在flex-container主方向大小不足以容纳flex items的<code>flex-basis</code>总和时，浏览器会自动缩小它们。
  </p>
  
  <p>
    举一段代码说明：
  </p>
  
  <pre><code>&lt;div class='Grid'&gt;
  &lt;div class='first'&gt;我曾在天上见过地的繁华&lt;/div&gt;
  &lt;div class='last'&gt;陈三说的&lt;/div&gt;
&lt;/div&gt;
&lt;style&gt;
.example-Grid{
  color: white;
  display: flex;
  width: 400px;
  border: 1px solid red;
}
.example-first{
  background: green;
  flex-basis: 400px;
}
.example-last{
  background: orange;
  flex-basis:200px;
}
&lt;/style&gt;
</code></pre>
  
  <p>
    样式结果如下：
  </p>
  
  <div class='example-Grid'>
    <div class='example-first'>
      我曾在天上见过地的繁华
    </div>
    
    <div class='example-last'>
      陈三说的
    </div>
  </div>
  
  <p>
  </p>
  
  <p>
    这里，.example-first的宽度是267px，.example-last的宽度是133px，它们是这样计算的：
  </p>
  
  <blockquote>
    <p>
      .example-first(宽度) = 400 * (400 / (400 + 200)) = 266.666666667
    </p>
    
    <p>
      .example-last(宽度) = 400 * (200 / (400 + 200)) = 133.333333333
    </p>
  </blockquote>
  
  <p>
    也就是说，flex container按比例分配flex items的大小。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">百分比</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    百分比的情况与计算值是一样的，如果flex container足够包含flex items的<code>flex-basis</code>总值，则10%的意思就是flex container在主方向的大小乘以10%。
  </p>
  
  <p>
    如果flex container不足以包含flex items的<code>flex-basis</code>总值，比如：
  </p>
  
  <pre><code>&lt;div class="example2-Grid"&gt;
 &lt;div&gt;&lt;/div&gt;
 &lt;div&gt;&lt;/div&gt;
 &lt;div&gt;&lt;/div&gt;
 &lt;div&gt;&lt;/div&gt;
&lt;/div&gt;
&lt;style&gt;
.example2-Grid{
     border: 3px solid black;
     display: flex;
     height: 200px;
}
.example2-Grid div:nth-of-type(1){
     background: rgb(0, 137, 250);
     flex-basis: 100%;
}
.example2-Grid div:nth-of-type(2){
     background: rgb(105, 0, 88);
     flex-basis: 20%;
}
.example2-Grid div:nth-of-type(3){
     background: rgb(255, 59, 0);
     flex-basis: 30%;
}
.example2-Grid div:nth-of-type(4){
     background: rgb(0, 197, 73);
     flex-basis: 40%;
}
&lt;/style&gt;
</code></pre>
  
  <p>
    代码的样式如下：
  </p>
  
  <div class="example2-Grid">
    <div>
      陈
    </div>
    
    <div>
      三
    </div>
    
    <div>
      是
    </div>
    
    <div>
      人
    </div>
  </div>
  
  <p>
  </p>
  
  <p>
    其中第一个flex item的<code>flex-basis</code>取值为100%，则计算时，它的main size占比是：
  </p>
  
  <blockquote>
    <p>
      100% / (100% + 20% + 30% + 40%) = 52.631578947%
    </p>
  </blockquote>
  
  <p>
    真正设计或实现页面时，我们通常不可能做这样的计算，但了解计算过程的话，心里有底，碰上问题，就知道怎么解决。
  </p>
  
  <footnotes>
    <fn name="13071.1">
      <p>
        <a href="http://docs.webplatform.org/wiki/css/properties/flex-basis">flex-basis · css · WPD · WebPlatform.org</a>
      </p>
    </fn>
    
    <fn name="13071.2">
      <p>
        <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/flex-basis">flex-basis &#8211; CSS | MDN</a>
      </p>
    </fn>
  </footnotes>
</div>