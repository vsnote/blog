---
title: Twitter bootstrap 的 affix.js 插件
author: 陈 三
layout: post
date: 2013-09-10T22:52:31+00:00
excerpt: affix 插件用法与效果说明。
url: /twitter-bootstrap-affix-js.html
dsq_thread_id:
  - 1746640545
views:
  - 4899
categories:
  - 前端开发
tags:
  - bootstrap

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#Affix"><span class="toc_number toc_depth_1">1</span> Affix 效果</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#affixaffix-topaffix-bottom"><span class="toc_number toc_depth_1">2</span> affix、affix-top、affix-bottom 类</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">3</span> 案例</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">4</span> 注意事项</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-3"><span class="toc_number toc_depth_1">5</span> 参考</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    我觉得 Twitter Bootstrap 提供的 JavaScript 插件可用性非常高，但文档多数简单。按部就班操作了，有效果当然好，没效果的话简直不知道为什么。之前我写过 <a href="http://www.zfanw.com/blog/bootstrap-scrollspy.html">Scrollspy 用法</a>，就是我在博客上折腾该插件的一点总结。
  </p>
  
  <p>
    这一篇也一样。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="Affix">Affix 效果</span><a title="标题链接地址" class="u-floatRight hidden" id="heyAffix" href="#Affix"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    从字面上翻译，则 <a href="http://getbootstrap.com/javascript/#affix">affix</a> 是固定的意义，但这个插件里，这固定是有条件的。
  </p>
  
  <p>
    先来看下 affix 的效果，本篇右侧的目录导航。
  </p>
  
  <p>
    这一目录部分，在页面刚滚动时，是随页面一起滚动的，但到达某一位置后，它开始固定在页面上；页面滚动到评论部分时，目录不再固定，又随页面一起滚动。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="affixaffix-topaffix-bottom">affix、affix-top、affix-bottom 类</span><a title="标题链接地址" class="u-floatRight hidden" id="heyaffixaffix-topaffix-bottom" href="#affixaffix-topaffix-bottom"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    页面滚动过程中，Affix 插件会根据我们的配置参数切换应用到目录部分的 CSS 类，整个滚动过程会产生三个类：
  </p>
  
  <ol>
    <li>
      affix-top
    </li>
    <li>
      affix
    </li>
    <li>
      affix-bottom
    </li>
  </ol>
  
  <p>
    插件提供的配置参数 <code>offset: { }</code>，里面包括两个值：top 和 bottom。
  </p>
  
  <p>
    整个过程用文字描述如下：
  </p>
  
  <ol>
    <li>
      页面加载完毕后，应用 affix 效果的内容会增加一个 <code>.affix-top</code> 样式类
    </li>
    <li>
      当页面向下滚动了 top 的距离时，<code>.affix-top</code> 切换成 <code>.affix</code> 类
    </li>
    <li>
      页面滚动到离底部距离为 bottom 时，<code>.affix</code> 类切换成 <code>.affix-bottom</code>
    </li>
  </ol>
  
  <p>
    这样，我们根据需要定义这三个类的样式就好了。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">案例</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    仍是本篇，
  </p>
  
  <p>
    目录部分，我添加了一个 ID <code>myaffix</code>，在引用 jQuery 与 <a href="http://www.bootstrapcdn.com/">Bootstrap.js</a> 后，添加 JavaScript 代码如下：
  </p>
  
  <pre><code>$('#myaffix').affix({
    offset: {
      top: 50
    , bottom: function () {
        return (this.bottom = $('#comments').outerHeight(true) + $('#footer').outerHeight(true))
      }
    }
});
</code></pre>
  
  <p>
    这里我通过 JavaScript 设置 offset 值，而不是直接在 HTML 标签中应用属性 <code>data-spy="affix"</code>、<code>data-offset-top</code> 与 <code>data-offset-bottom</code>，这是因为评论部分的高度无法确定，bottom 值只能动态计算。
  </p>
  
  <p>
    这样，页面加载完成后，#myaffix 有一个 <code>.affix-top</code> 类，在滚动 50px 后，#myaffix 部分有一个 <code>.affix</code> 类，在离页面底部距离 bottom 值时，#myaffix 部分的类又变成 <code>.affix-bottom</code>。
  </p>
  
  <p>
    CSS 里，我只定义了两个类：
  </p>
  
  <pre><code>.affix{position:fixed;top:30px;}
.affix-bottom{position:absolute;}
</code></pre>
  
  <p>
    插件会自动计算 <code>.affix-bottom</code> 类的 top 值，所以无需我们设置。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">注意事项</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    如果发现固定部分在滚动时有抖动现象，需要给 body 设置 <code>position:relative</code>。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-3">参考</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-3" href="#i-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <a href="https://github.com/twbs/bootstrap/issues/4647">bootstrap-affix.js issue</a>
    </li>
  </ol>
</div>