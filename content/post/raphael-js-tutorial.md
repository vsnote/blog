---
title: Raphael.js 教程
author: 陈 三
layout: post
date: 2013-06-20T16:12:06+00:00
url: /raphael-js-tutorial.html
dsq_thread_id:
  - 1415613649
dsq_needs_sync:
  - 1
views:
  - 4611
categories:
  - 前端开发

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 调用</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 用法</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-3"><span class="toc_number toc_depth_1">3</span> 参考</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    Raphael.js 官网的<a href="http://raphaeljs.com/">教程</a>非常简单，仅首页一段代码，其它就是 <a href="http://raphaeljs.com/reference.html">Reference</a>。但作者在 Reference 部分也惜墨如金，不肯多费几句。所以这一篇，简单介绍如何使用 Raphael.js 。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">调用</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    两种方式：
  </p>
  
  <ol>
    <li>
      <p>
        用 <code>script</code> 标签，如下：
      </p>
      
      <pre><code>&lt;script src="raphael.js"&gt;&lt;/script&gt;
</code></pre>
    </li>
    
    <li>
      <p>
        AMD 规范的加载方式，如下：
      </p>
      
      <pre><code>define([ "path/to/raphael" ], function( Raphael ) {
  console.log( Raphael );
});
</code></pre>
    </li>
  </ol>
  
  <h2 class="storycontent-h2">
    <span id="i-2">用法</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    用 <a href="http://raphaeljs.com/reference.html#Raphael"><code>Raphael</code> 方法</a>创建一块画布，
  </p>
  
  <pre><code>// 在浏览器窗口中，坐标 (10, 50) 位置创建一个 canvas 对象，长 320px，宽 200px。
var paper = Raphael(10, 50, 320, 200);
</code></pre>
  
  <p>
    我们随后的操作都在这块画布上。
  </p>
  
  <h3>
    绘制基本图形
  </h3>
  
  <p>
    比如，以画布坐标 (50,100) 为中心，画一个半径 50px 的圆，并填充红色：
  </p>
  
  <pre><code>var circle = paper.circle(50, 100, 50);
circle.attr({"fill":"red"}); // attr 方法用于设定对象属性
</code></pre>
  
  <p>
    另外，Raphael 方法还可以在 HTML 元素中创建画布：
  </p>
  
  <pre><code>&lt;div id="raphael1"&gt;&lt;/div&gt;
&lt;script&gt;
    //在 id 为 raphael1 元素中创建画布
    var paper = Raphael("raphael1", 320, 200);
    var circle = paper.circle(100, 100, 50);
    circle.attr({"fill":"green"});
&lt;/script&gt;
</code></pre>
  
  <p>
    除了圆(<a href="http://raphaeljs.com/reference.html#Paper.circle">circle</a>)以外，Raphael.js 还提供其他常规图形的绘制方法，比如方形(<a href="http://raphaeljs.com/reference.html#Paper.rect">rect</a>)、椭圆(<a href="http://raphaeljs.com/reference.html#Paper.ellipse">ellipse</a>)、路径(<a href="http://raphaeljs.com/reference.html#Paper.path">path</a>)等。
  </p>
  
  <h3>
    修改对象属性
  </h3>
  
  <p>
    在画布上创建 Raphael 对象后，我们可以修改对象属性。
  </p>
  
  <p>
    比如，先使用 <code>text</code> 方法生成文字，然后修改字体大小为 30px，填充蓝色，红色描边，透明度 50%：
  </p>
  
  <div id="raphael2">
  </div>
  
  <p>
    代码如下：
  </p>
  
  <pre><code>&lt;div id="raphael2"&gt;&lt;/div&gt;
&lt;script&gt;
(function(){
    var paper = Raphael("raphael2", 300, 300);
    var t = paper.text(150, 150, "Hello from 陈三");
    t.attr({"font-size":"30px","fill":"blue","stroke":"red","opacity":".5"});
})();
&lt;/script&gt;
</code></pre>
  
  <p>
    这一切都是通过 <a href="http://raphaeljs.com/reference.html#Element.attr">Raphael 对象的 attr</a> 方法完成。
  </p>
  
  <h3>
    变换对象
  </h3>
  
  <p>
    除了修改对象属性，我们还可以变换(<a href="http://raphaeljs.com/reference.html#Element.transform">transform</a>)对象，比如平移、旋转、缩放。
  </p>
  
  <div id="raphael3">
  </div>
  
  <p>
    上图中的代码如下(虚线为图形变换前)：
  </p>
  
  <pre><code>&lt;div id="raphael3"&gt;&lt;/div&gt;
&lt;script&gt;
(function(){
    var paper = Raphael("raphael3", 200, 200);
    var rect = paper.rect(50, 50, 100, 100, 5);
    rect.attr({"stroke-dasharray":"-"});
    rect.transform("t100,100r45t-100,0s.5");
})();
&lt;/script&gt;
</code></pre>
  
  <p>
    Raphael 对象变换有四个命令：
  </p>
  
  <ol>
    <li>
      t &#8211; translate
    </li>
    <li>
      r &#8211; rotate
    </li>
    <li>
      s &#8211; scale
    </li>
    <li>
      m &#8211; matrix
    </li>
  </ol>
  
  <p>
    上例中 <code>t100,100r45t-100,0s.5</code> 命令翻译过来就是：
  </p>
  
  <ol>
    <li>
      对象水平方向平移 100
    </li>
    <li>
      垂直方向平移 100
    </li>
    <li>
      旋转 45 度
    </li>
    <li>
      水平方向往负方向平移 100
    </li>
    <li>
      缩小图形到原来的一半
    </li>
  </ol>
  
  <h3>
    动画效果
  </h3>
  
  <p>
    上面说到修改对象属性和变换对象，因为有开始和结束两个状态，我们就可以制作<a href="http://raphaeljs.com/reference.html#Element.animate">动画</a>效果。
  </p>
  
  <div id="raphael4">
  </div>
  
  <p>
    上图的代码如下：
  </p>
  
  <pre><code>&lt;div id="raphael4"&gt;&lt;/div&gt;
&lt;script&gt;
(function(){
    var paper = Raphael("raphael4", 400, 300);
    var circle = paper.circle(200, 150, 100);
    circle.attr({"fill":"red"});
    circle.animate({cx: 10, cy: 20, r: 8, "fill": "blue"}, 10e3);
})();
&lt;/script&gt;
</code></pre>
  
  <p>
    圆心的初始坐标 (200,130)，半径 100，填充红色，页面加载完成后，圆心坐标变成 (cx,cy)，即 (10,20)，半径缩为 8，填充蓝色，这个变化过程时长为 10e3 毫秒，即 10 秒 &#8211; 如果你没有看到动画效果，那是因为动画已经结束，请刷新页面，然后跳转到这一部分。
  </p>
  
  <h3>
    绑定事件
  </h3>
  
  <p>
    Raphael.js 还可以给对象绑定事件，比如单击、双击、拖动、鼠标移入、鼠标移出等。
  </p>
  
  <p>
    举 <a href="http://raphaeljs.com/reference.html#Element.hover">hover 方法</a>为例：
  </p>
  
  <div id="raphael5">
  </div>
  
  <p>
    代码如下：
  </p>
  
  <pre><code>&lt;div id="raphael5"&gt;&lt;/div&gt;
&lt;script&gt;
(function(){
    var paper = Raphael("raphael5", 400, 300);
    var circle = paper.circle(200, 150, 100);
    circle.attr({"fill":"red"});
    circle.hover(function(){circle.attr({"fill":"green"});},function(){circle.attr({"fill":"red"});});//给 circle 对象绑定 hover 事件
})();
&lt;/script&gt;
</code></pre>
  
  <p>
    上例中，鼠标放到圆上，填充色变成绿色，移开恢复成红色。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-3">参考</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-3" href="#i-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <a href="http://raphaeljs.com/reference.html">Reference</a>
    </li>
  </ol>
</div>