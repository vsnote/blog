---
title: Sass
author: 陈 三
layout: post
date: 2013-10-07T05:55:48+00:00
excerpt: 从一个 CSS 类命名说到 Sass 变量的应用
url: /sass.html
views:
  - 1352
categories:
  - 前端开发
tags:
  - css
  - oocss
  - sass

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#CSS"><span class="toc_number toc_depth_1">1</span> CSS 类命名</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#Sass"><span class="toc_number toc_depth_1">2</span> Sass 变量</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">3</span> 扩展阅读</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    现在为止，我还坚持一个看法，就是，如果我们对 CSS 模块化、<a href="http://www.zfanw.com/blog/css-architecture.html">架构</a>等没有一个全局把握，那么，任何 CSS 预处理器，不管它是 LESS，还是 <a href="http://sass-lang.com/">Sass</a> 或者 Stylus，带来的好处只会小于它们带来的坏处。
  </p>
  
  <p>
    但我终于想写一篇关于 Sass 的内容。一来是上一篇写 <a href="http://www.zfanw.com/blog/compass-sprite.html">Compass 与 CSS 贴图定位</a>时其实已经用到 Sass，二来自身对 CSS 架构有些了解，夸张地说，就是想试一下身手。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="CSS">CSS 类命名</span><a title="标题链接地址" class="u-floatRight hidden" id="heyCSS" href="#CSS"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    还是先来聊一下 CSS 类命名。
  </p>
  
  <p>
    页面上有一 A 块，它的 margin-top 值为20px，从类的可复用性出发，我们可能这样给它命名：
  </p>
  
  <pre><code>.mt-20 {
    margin-top:20px;
}
</code></pre>
  
  <p>
    在 HTML 代码中应用到 A 块则是如下：
  </p>
  
  <pre><code>&lt;p id="A" class="mt-20"&gt;&lt;/p&gt;
</code></pre>
  
  <p>
    假如 B、C、D 也一样的 margin-top 值，那么我们的 HTML 代码会出现如下：
  </p>
  
  <pre><code>&lt;p id="B" class="mt-20"&gt;&lt;/p&gt;
&lt;p id="C" class="mt-20"&gt;&lt;/p&gt;
&lt;p id="D" class="mt-20"&gt;&lt;/p&gt;
</code></pre>
  
  <p>
    一旦数值20发生变化，比如说要微调成21,那么，上面的代码中，我们要改 CSS 文件中2处、HTML 文件中4处。显然，情况糟透了。
  </p>
  
  <p>
    以前，我曾尝试过上述命名方法，并且见到有人鼓励这样的命名方式，但随后就发现问题不少。那么，怎样的命名方式会更合理？
  </p>
  
  <p>
    从 font-size 的可能取值里我们可以得到启发：
  </p>
  
  <pre><code>font-size: xx-small
font-size: x-small
font-size: small
font-size: medium
font-size: large
font-size: x-large
font-size: xx-large
</code></pre>
  
  <p>
    是的，我们的 .mt-20 可以考虑命名成 .mt-large，这样我们就脱离了具体的数值，也让 CSS 类名更有语义。bootstrap 的<a href="http://getbootstrap.com/css/#grid-options">网格系统</a>命名则是 .col-xs-、.col-sm-、.col-md-、.col-lg- 这样。更进一步缩减代码。Yahoo <a href="https://github.com/chenxsan/HTML5Boilerplate/blob/master/css/helper.css">走得更远</a>，它的 CSS 里是这样写的：
  </p>
  
  <pre><code>.mt-l {
    margin-top: 20px;
}
.mr-l {
    margin-right: 20px;
}
.mb-l {
    margin-bottom: 20px;
}
.ml-l {
    margin-left: 20px;
}
</code></pre>
  
  <p>
    这也是我现在采用的命名。(Yahoo 的页面里，其实有很多 <a href="http://oocss.org/">oocss</a> 的影子，上面的命名只不过是一个体现。)
  </p>
  
  <p>
    在拟定上述的命名方法后，再来说 Sass 在其中的应用。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="Sass">Sass 变量</span><a title="标题链接地址" class="u-floatRight hidden" id="heySass" href="#Sass"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    在上面代码中，我们定义 large 值为20px，假如后期需要微调，比如降成19px，这下我们又要修改起码4处的值，对的，我们又在干重复的事情。代码一旦出现重复，就会容易出错。Sass 可以解决这个问题。
  </p>
  
  <p>
    在 .scss 文件中，我们事先定义一个 $large 变量，然后在定义类时使用该变量：
  </p>
  
  <pre><code>$large: 20px;

.mt-l{margin-top: $large;}
.mr-l{margin-right: $large;}
.mb-l{margin-bottom: $large;}
.ml-l{margin-left: $large;}
</code></pre>
  
  <p>
    这样，后期 large 值出现变化，我们也只要修改一处。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">扩展阅读</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <a href="http://ianstormtaylor.com/oocss-plus-sass-is-the-best-way-to-css/">OOCSS + Sass = The best way to CSS</a>
    </li>
  </ol>
</div>