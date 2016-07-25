---
title: HTMLBars 语法
author: 陈 三
layout: post
date: 2015-03-12T12:33:58+00:00
url: /htmlbars-syntax.html
views:
  - 645
categories:
  - 前端开发
tags:
  - ember.js

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 属性可直接绑定</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 变量可任意位置使用</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#if"><span class="toc_number toc_depth_1">3</span> if 可行内使用</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-3"><span class="toc_number toc_depth_1">4</span> 参考</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    HTMLBars 是 Ember.js 的新模板语言，基于 handlebars.js，但更为强大、直观。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">属性可直接绑定</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    原先我们要给 HTML 标签绑定属性需要借助 <code>bind-attr</code>：
  </p>
  
  <pre><code>&lt;a {{bind-attr href=url}}&gt;点我&lt;/a&gt;
</code></pre>
  
  <p>
    现在可以这样写：
  </p>
  
  <pre><code>&lt;a href={{url}}&gt;点我&lt;/a&gt;
</code></pre>
  
  <p>
    更加直观，明了。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">变量可任意位置使用</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    借由上一步的功能，我们现在可以在模板的任意位置中使用变量：
  </p>
  
  <pre><code>&lt;a href="http://www.zfanw.com/blog/{{name}}"&gt;陈三&lt;/a&gt;
</code></pre>
  
  <p>
    又比如：
  </p>
  
  <pre><code>&lt;a style="color: {{linkColor}}"&gt;陈三&lt;/a&gt;
</code></pre>
  
  <h2 class="storycontent-h2">
    <span id="if"><code>if</code> 可行内使用</span><a title="标题链接地址" class="u-floatRight hidden" id="heyif" href="#if"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    <code>if</code> 判断语句可以在行内使用：
  </p>
  
  <pre><code>&lt;a href="http://www.zfanw.com/blog/{{if name '陈三' '不认识'}}"&gt;陈三&lt;/a&gt;
</code></pre>
  
  <p>
    不必以下这种写法：
  </p>
  
  <pre><code>{{#if name}}
'陈三'
{{else}}
'不认识'
{{/if}}
</code></pre>
  
  <h2 class="storycontent-h2">
    <span id="i-3">参考</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-3" href="#i-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <a href="http://talks.erikbryn.com/htmlbars-emberconf/#/">HTMLBars: The Next-Generation of Templating in Ember.js</a>
    </li>
  </ol>
</div>