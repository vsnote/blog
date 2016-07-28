---
title: IE6、7下的 z-index 问题
author: 陈 三
layout: post
date: 2013-08-18T12:48:27+00:00
excerpt: 怎样调试 IE6、7 下的 z-index 问题。
url: /ie6-7-z-index-bug.html
dsq_thread_id:
  - 1746880831
views:
  - 554
categories:
  - 前端开发
tags:
  - ie6
  - ie7
  - z-index

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_z-index"><span class="toc_number toc_depth_1">1</span> 现代浏览器下 z-index 值比较</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#IE67_z-index"><span class="toc_number toc_depth_1">2</span> IE6、7下 z-index 值比较</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">3</span> 调试、解决</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    一般在使用 z-index 时，哪怕我们不十分清楚 z-index 概念，也很少会碰上问题。
  </p>
  
  <p>
    但 IE6、7 对 z-index 层叠上下文(stacking context) 生成条件有点误会，会对现实应用造成困扰，也就是常见的 z-index 失效问题。
  </p>
  
  <p>
    看一个别人的 <a href="http://therealcrisp.xs4all.nl/meuk/IE-zindexbug.html">demo</a>。Demo 中，IE6、7 下， <code>position:relative</code> 也生成一个上下文。而根据 <a href="http://www.w3.org/TR/CSS21/visuren.html#z-index">W3C 规范</a>，这是错误的。
  </p>
  
  <p>
    且按照 IE6、7 的错误理解，来分析下 z-index 是怎么比较大小的。
  </p>
  
  <p>
    Demo 的 HTML 代码如下：
  </p>
  
  <pre><code>&lt;div id="container"&gt;
    &lt;div id="box1"&gt;This box should be on top&lt;/div&gt;
&lt;/div&gt;

&lt;div id="box2"&gt;This box should not be on top; IE however seems to create a new stacking context for positioned elements, even when the computed z-index of that element is 'auto'.&lt;/div&gt;
</code></pre>
  
  <p>
    CSS 代码：
  </p>
  
  <pre><code>#container {
    position: relative;
}
#box1 {
    background-color: yellow;
    height: 200px;
    left: 510px;
    position: absolute;
    top: 100px;
    width: 200px;
    z-index: 20;
}
#box2 {
    background-color: lime;
    height: 200px;
    left: 460px;
    position: absolute;
    top: 50px;
    width: 200px;
    z-index: 10;
}
</code></pre>
  
  <h2 class="storycontent-h2">
    <span id="_z-index">现代浏览器下 z-index 值比较</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_z-index" href="#_z-index"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    在现代浏览器中，绝对定位的 #box1 与 #box2 元素均参照初始包含块比较 z-index 值，假定初始包含块 z-index 值为0：
  </p>
  
  <table>
    <tr>
      <th>
      </th>
      
      <th>
        #box1
      </th>
      
      <th>
        #box2
      </th>
    </tr>
    
    <tr>
      <td>
        html
      </td>
      
      <td>
      </td>
      
      <td>
      </td>
    </tr>
    
    <tr>
      <td>
        自身
      </td>
      
      <td>
        20
      </td>
      
      <td>
        10
      </td>
    </tr>
  </table>
  
  <p>
    如果我们也按 CSS 规则的权重排列来理解上面的值：
  </p>
  
  <pre><code>#box1 - 0,20
#box2 - 0,10
</code></pre>
  
  <p>
    显然，#box1 要排在 #box2 上面，即黄色块在绿色块上。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="IE67_z-index">IE6、7下 z-index 值比较</span><a title="标题链接地址" class="u-floatRight hidden" id="heyIE67_z-index" href="#IE67_z-index"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    因为 <code>position:relative</code> 也生成了一个上下文，于是上面的表格会变成：
  </p>
  
  <table>
    <tr>
      <th>
      </th>
      
      <th>
        #box1
      </th>
      
      <th>
        #box2
      </th>
    </tr>
    
    <tr>
      <td>
        html
      </td>
      
      <td>
      </td>
      
      <td>
      </td>
    </tr>
    
    <tr>
      <td>
        &#35;container
      </td>
      
      <td>
      </td>
      
      <td>
        &#8211;
      </td>
    </tr>
    
    <tr>
      <td>
        自身
      </td>
      
      <td>
        20
      </td>
      
      <td>
        10
      </td>
    </tr>
  </table>
  
  <p>
    对比如下：
  </p>
  
  <pre><code>#box1 - 0,0,20
#box2 - 0,10
</code></pre>
  
  <p>
    这样，#box2 变成在 #box1 上面。
  </p>
  
  <p>
    解决办法是给 <code>#container</code> 元素设置一个大于10的 z-index 值：
  </p>
  
  <pre><code>#box1 - 0,11,20
#box2 - 0,10
</code></pre>
  
  <p>
    你可能想问设置为10为什么不行，因为同一个 z-index 值，后绘制的与之前的内容如果有交叉区域，则会覆盖之前的内容 &#8211; 这是我的理解。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">调试、解决</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    当给一个元素设置 <code>z-index:9999</code> 时，IE6、7 下元素层叠还是无效，则可以按上面所描述的，从初始包含块开始，找出所有层叠上下文，然后对比 z-index 值。一旦 z-index 链路明确，也就知道该在哪个节点下手。
  </p>
</div>