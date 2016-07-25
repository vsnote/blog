---
title: jQuery next()
author: 陈 三
layout: post
date: 2012-04-25T09:04:22+00:00
url: /jquery-next.html
views:
  - 1890
dsq_thread_id:
  - 663364938
categories:
  - 前端开发
tags:
  - JavaScript
  - jQuery

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 单一对象</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#jQuery"><span class="toc_number toc_depth_1">2</span> jQuery 对象集合</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#nextselector"><span class="toc_number toc_depth_1">3</span> next([selector])</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">4</span> 参考</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    调用 <code>next()</code> 方法的 jQuery 对象分两种，一是单一对象，二是对象集合，下面分开说明：
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">单一对象</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    假定以下 HTML 代码：
  </p>
  
  <pre><code>&lt;div id="wrapper"&gt;
   &lt;ul class="nav"&gt;
        &lt;li&gt;first line&lt;/li&gt;
        &lt;li&gt;second line，将会被下面的 jQuery 语句选中并改变背景颜色&lt;/li&gt;
        &lt;li&gt;third line&lt;/li&gt;   
        &lt;li&gt;four line&lt;/li&gt;    
  &lt;/ul&gt;
&lt;/div&gt;
</code></pre>
  
  <p>
    CSS 语句为:
  </p>
  
  <pre><code>#wrapper li{   
    color:white;    
    background:#333;   
}
</code></pre>
  
  <p>
    所用 jQuery 语句如下：
  </p>
  
  <pre><code>$("#wrapper li:first-child").next().css("background", "#0175cc");
</code></pre>
  
  <p>
    <code>$("#wrapper li:first-child")</code> 选择无序列表 ul 第一个列表项 li，此时 jQuery 对象单一，因此调用 next() 方法，取得的是<strong>紧跟在它后面</strong>的<strong>同辈</strong> (sibling) 元素，即第二个 li。点击下面的 jsfiddle 链接，运行示例，可以看到，第二个 li 元素的背景色现在已经改变。
  </p>
  
  <p>
    示例1：<a href="http://jsfiddle.net/chenxsan/mjufm/1/">jQuery next()</a>
  </p>
  
  <p>
    这样 <code>nextAll()</code> 方法的意思也很明确了，它选定第一个 li 元素后的<strong>所有同辈元素</strong>。
  </p>
  
  <p>
    示例2：<a href="http://jsfiddle.net/chenxsan/khmBy/1/">jQuery nextAll()</a>
  </p>
  
  <h2 class="storycontent-h2">
    <span id="jQuery">jQuery 对象集合</span><a title="标题链接地址" class="u-floatRight hidden" id="heyjQuery" href="#jQuery"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    另一段 HTML 代码：
  </p>
  
  <pre><code>&lt;div id="wrapper"&gt;
   &lt;ul class="nav"&gt;
        &lt;li&gt;first line&lt;/li&gt;
        &lt;li&gt;second line&lt;/li&gt;
        &lt;li&gt;third line&lt;/li&gt;   
        &lt;li&gt;four line&lt;/li&gt;           
    &lt;/ul&gt;   
    &lt;div&gt;division after ul.nav as its sibling,&lt;/div&gt;
    &lt;ol&gt;     
        &lt;li&gt;有序列表与 jquery prev()&lt;/li&gt;     
        &lt;li&gt;有序列表与 jquery prevAll()&lt;/li&gt;   
    &lt;/ol&gt;
    &lt;div id="jquery_next"&gt;
        &lt;p&gt;jquery next() 函数示例&lt;/p&gt;  
    &lt;/div&gt;
    &lt;p&gt;last sentence&lt;/p&gt;
&lt;/div&gt;
</code></pre>
  
  <p>
    CSS 语句:
  </p>
  
  <pre><code>#wrapper li{   
    color:white;
    background:#333;
}
</code></pre>
  
  <p>
    所用 jQuery 语句:
  </p>
  
  <pre><code>$("#wrapper div").next().css("font-size", "25px");
</code></pre>
  
  <p>
    这里的 jQuery 语句 <code>$("#wrapper div")</code> 选中两个 div，一个紧跟在 <code>ul.nav</code> 后面，一个 id 为 <code>jquery_next</code>，它们是一个对象集合，因此，next() 方法将选中两个 jQuery 对象：第一个 div 后的 ol 序列，第二个 div 后的 p 段落，然后更改字体大小。
  </p>
  
  <p>
    示例3：<a href="http://jsfiddle.net/chenxsan/Rf6QX/2/">jQuery 对象集合使用 next()</a>
  </p>
  
  <p>
    <code>nextAll()</code> 同理。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="nextselector">next([selector])</span><a title="标题链接地址" class="u-floatRight hidden" id="heynextselector" href="#nextselector"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    <code>next()</code> 方法默认选取紧跟的后一个同辈元素，不管它是 <code>div</code> 还是 <code>p</code> 还是 <code>ol</code> 又或其他，但如果指定 <code>selector</code>，情况就会变化，比如 <code>selector</code> 指定为 <code>p</code>，但随后紧跟的却是 <code>div</code>，则该语句没有选中任何对象。
  </p>
  
  <p>
    其他方法如 <code>prev()</code>、<code>prevAll()</code>、<code>prev([selector])</code> 的用法，与上面描述的相近，只不过取得的结果是对象前面的元素，而非后面的元素。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">参考</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <a href="http://api.jquery.com/next/">jQuery next() api</a>
    </li>
  </ol>
</div>