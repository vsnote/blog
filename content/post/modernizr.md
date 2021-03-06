---
title: Modernizr 用法
author: 陈 三
layout: post
date: 2013-06-11T06:45:32+00:00
url: /modernizr.html
dsq_thread_id:
  - 1388504386
views:
  - 3152
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
      <a href="#_Modernizr"><span class="toc_number toc_depth_1">1</span> 为什么需要 Modernizr</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#Modernizr"><span class="toc_number toc_depth_1">2</span> Modernizr 的作用</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <h2 class="storycontent-h2">
    <span id="_Modernizr">为什么需要 Modernizr</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Modernizr" href="#_Modernizr"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    浏览器的发展参差不齐，以最新版 Firefox、Google Chrome、Safari 来说，它们支持的 HTML5、CSS3 特性恐怕也不尽相同，而况还有用户的情况，不同用户使用不同浏览器的不同版本，于是造成 Web 开发者在开发网站时，要面对数量庞大的浏览器种类。
  </p>
  
  <p>
    如果开发时按固定标准，比如 IE6 不支持的特性，我们统统不用，那就没 Modernizr 什么事；但我想这种情况极少，更多的开发，是在现代浏览器上使用它们支持的特性，而在早期浏览器上做一定的降级处理，这就是所谓 &#8220;Progressive Enhancement&#8221;，也是 Modernizr 要起的主要作用。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="Modernizr">Modernizr 的作用</span><a title="标题链接地址" class="u-floatRight hidden" id="heyModernizr" href="#Modernizr"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <h3>
    下载引用
  </h3>
  
  <p>
    首先，下载 <a href="http://modernizr.com/download/">Modernizr 文件</a>，然后在页面 <code>&lt;head&gt;&lt;/head&gt;</code> 中<a href="http://modernizr.com/docs/#installing">引用</a>：
  </p>
  
  <pre><code>&lt;script src="js/modernizr.js"&gt;&lt;/script&gt;
</code></pre>
  
  <p>
    需要注意这段代码的位置，放在 <code>&lt;head&gt;&lt;/head&gt;</code> 部分、所有样式表文件 <code>link</code> 后 &#8211; 之所以放样式表后面，是为了不阻塞 CSS 的加载。
  </p>
  
  <p>
    放在 <code>&lt;head&gt;&lt;/head&gt;</code> 中的原因有二：
  </p>
  
  <ol>
    <li>
      HTML5 Shiv 需要在 <code>&lt;body&gt;</code> 前执行，这样样式表才能识别 HTML5 中新增的标签
    </li>
    <li>
      防止 <a href="http://en.wikipedia.org/wiki/Flash_of_unstyled_content">FOUC</a>
    </li>
  </ol>
  
  <p>
    如果这两样你都不介意，那么请随便找个位置添加 <strong>modernizr</strong>。
  </p>
  
  <h3>
    添加 no-js
  </h3>
  
  <p>
    另外，我们还需要在 <code>&lt;html&gt;</code> 标签中添加一个 <code>no-js</code> 类：
  </p>
  
  <pre><code>&lt;html class="no-js"&gt;
</code></pre>
  
  <p>
    如果 Modernizr 正常运行，它会移除 <code>no-js</code>，添加一个 <code>js</code> 类；假如用户浏览器禁用 JavaScript，则 Modernizr 无法运行，html 标签就有 <code>no-js</code>。
  </p>
  
  <p>
    在 HTML5 Boilerplate 里，<code>&lt;html&gt;</code> 标签是这样写的，比仅加一个 <code>no-js</code> 更复杂：
  </p>
  
  <pre><code>&lt;!--[if lt IE 7]&gt;      
  &lt;html class="no-js lt-ie9 lt-ie8 lt-ie7"&gt; 
&lt;![endif]--&gt;
&lt;!--[if IE 7]&gt;           
  &lt;html class="no-js lt-ie9 lt-ie8"&gt; 
&lt;![endif]--&gt;
&lt;!--[if IE 8]&gt;         
  &lt;html class="no-js lt-ie9"&gt; 
&lt;![endif]--&gt;
&lt;!--[if gt IE 8]&gt;&lt;!--&gt; 
  &lt;html class="no-js"&gt; 
&lt;!--&lt;![endif]--&gt;
</code></pre>
  
  <p>
    页面在加载完 Modernizr.js 后，会自动运行生成一个 JavaScript 对象 <strong>Modernizr</strong>，这个对象中包含浏览器特性支持的真假值，另外，它还会给 <code>&lt;html&gt;</code> 标签添加新的类(class)，以标明浏览器对 HTML5、CSS3 特性的支持情况。以我的 Firefox 21 for Linux 为例，一个 HTML5 Boilerplate 页面的 <code>&lt;html&gt;</code> 标签在 Modernizr 作用后会变成如下：
  </p>
  
  <pre><code>&lt;html class="js no-flexbox canvas canvastext webgl no-touch geolocation postmessage no-websqldatabase indexeddb hashchange history draganddrop websockets rgba hsla multiplebgs backgroundsize borderimage borderradius boxshadow textshadow opacity cssanimations csscolumns cssgradients no-cssreflections csstransforms csstransforms3d csstransitions fontface generatedcontent video audio localstorage sessionstorage webworkers applicationcache svg inlinesvg smil svgclippaths"&gt;
</code></pre>
  
  <p>
    它表示我的浏览器支持 HTML5 的 geolocation、history，CSS3 的多背景图片等特性，一目了然。
  </p>
  
  <p>
    这样，我们在使用 CSS3 时就可以做一定的降级，比如：
  </p>
  
  <pre><code>body {
    background: url(background-top.png) top left no-repeat;
}
.multiplebgs body {
    background: url(background-top.png) top left no-repeat,
    url(background-bottom.png) bottom left repeat-x;
}
</code></pre>
  
  <p>
    早期的浏览器下，我们使用一张背景图片，而支持多背景图片的浏览器下，我们将使用两张背景图片。
  </p>
  
  <p>
    但这只是 Modernizr 的简单应用，它还有复杂应用，比如 HTML5 特性:
  </p>
  
  <pre><code>if (Modernizr.canvas) {
  // 可以使用 canvas
} else {
  // 浏览器没有原生的 canvas 支持，做一定的降级处理，或是加载 polyfills
}
</code></pre>
  
  <p>
    基本上所有 HTML5 特性都有<a href="https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-browser-Polyfills">相应的 Polyfills</a> 进行处理，至于是否必要，那就看项目需要了：有时候，你可以，不一定代表你要。毕竟，在 IE6 上支持 Geolocation 这样的特性意义不大。
  </p>
  
  <p>
    另外，Modernizr 脚本中已经添加 HTML5 浏览器支持脚本 <a href="https://code.google.com/p/html5shiv/">html5shiv</a>，我们只要引用 Moernizr.js 文件，IE9 以下的 IE 浏览器就支持 HTML5 添加的语义标签如 <code>nav、section、article</code> 等，也可以使用 CSS 对它们进行样式化。
  </p>
</div>