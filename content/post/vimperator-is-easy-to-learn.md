---
title: Vimperator 其实很简单
author: 陈 三
layout: post
date: 2012-05-31T02:16:30+00:00
url: /vimperator-is-easy-to-learn.html
views:
  - 2965
dsq_thread_id:
  - 708976402
categories:
  - vimperator
tags:
  - vimperator
  - 教程

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_Vimperator"><span class="toc_number toc_depth_1">1</span> 设置 Vimperator 界面</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">2</span> 打开网页</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">3</span> 浏览网页</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-3"><span class="toc_number toc_depth_1">4</span> 打开页面链接</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-4"><span class="toc_number toc_depth_1">5</span> 历史导航</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-5"><span class="toc_number toc_depth_1">6</span> 关闭页面</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-6"><span class="toc_number toc_depth_1">7</span> 标签页管理</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_Vimperator-2"><span class="toc_number toc_depth_1">8</span> 退出 Vimperator</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-7"><span class="toc_number toc_depth_1">9</span> 帮助</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-8"><span class="toc_number toc_depth_1">10</span> 修订历史</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    在提到 Vimperator 时，许多教程都会说及 Vim，毕竟 Vimperator 的理念来自 Vim，不提下祖籍何方好像不应当，但藉此他们也说，Vimperator 的学习曲线很陡。这句话对没学过 Vim 的人来说，真的阻碍很大。但我个人觉得不必这样描述，试着回想一下，大家平时最常用的操作，大概不会超过几个，只要熟悉这几个，已经可以很大提高浏览网页效率，减少使用鼠标的频次，至于更高阶些的应用，比如自定义命令等等，那完全看个人兴趣，没必要让这些高阶应用成为新手尝试 Vimperator 的拦路虎。
  </p>
  
  <p>
    虽然以前写过一篇 <a href="http://www.zfanw.com/blog/vimperator-firefox.html" title="打开文章">Firefox 利器 Vimperator</a>，但内容还是偏多，这篇再行精减，挑出最常用的操作。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Vimperator">设置 Vimperator 界面</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Vimperator" href="#_Vimperator"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Vimperator 默认界面并没有工具栏、菜单栏，新手可能无法习惯这种简陋。在 Vimperator 下执行：
  </p>
  
  <pre><code>:set gui=menu
</code></pre>
  
  <p>
    就可以显示菜单。
  </p>
  
  <p>
    在我们上手基本快捷键后，可以再隐藏它：
  </p>
  
  <pre><code>:set gui=nomenu
</code></pre>
  
  <h2 class="storycontent-h2">
    <span id="i">打开网页</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    有两种方式打开网页，
  </p>
  
  <ol>
    <li>
      在当前页打开
    </li>
    <li>
      在新标签页中打开
    </li>
  </ol>
  
  <p>
    前面一种按 <kbd>o</kbd> 键，后面一种按 <kbd>t</kbd> 键，o 指 open，t 指 tabopen，之后就可以在命令行模式里输入要打开的网址。
  </p>
  
  <p>
    上面的两个按键都是小写，它们有大写的变体，<kbd>O</kbd> 与 <kbd>T</kbd>，意义与小写接近，不过网址不是你自己输入的，而是基于当前网页的网址进行编辑，然后再决定是当前页打开还是新标签页里打开。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">浏览网页</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    打开网页后，常见的操作该是浏览，上下左右滚动页面，平时可能要用鼠标滚轮，或者拉动滚动条，但 Vimperator 里，你可以使用简单的几个键：
  </p>
  
  <p>
    <kbd>h</kbd> &#8211; 左
  </p>
  
  <p>
    <kbd>l</kbd> &#8211; 右
  </p>
  
  <p>
    <kbd>j</kbd> &#8211; 下
  </p>
  
  <p>
    <kbd>k</kbd> &#8211; 上
  </p>
  
  <p>
    刚用可能会不习惯，但多用几次，手部肌肉有了记忆，自然就流畅了 &#8211; Vim 之所以用这几个键来表示上下左右，是因为 vi 的开发者当时使用的机器上，<a href="http://www.catonmat.net/blog/why-vim-uses-hjkl-as-arrow-keys/" title="vim 的 hljk 移动的由来">上下左右箭头键就刻在这几个键上</a>。
  </p>
  
  <p>
    大家在浏览网页时，可能会经常看见“返回顶部”的按钮，但应该没人见过“去到底部”的按钮。Vimperator 返回顶部命令是 <kbd>gg</kbd>，到底部是 <kbd>G</kbd>，而且你还能明确指定整个页面的百分位置，比如，页面中间是 <kbd>50G</kbd>，其他可类推。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-3">打开页面链接</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-3" href="#i-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    互联网的发展始于超链接，你打开的任一网页，基本都会有一个以上的链接，你可能想打开这个链接，用鼠标的话可以左键点击，Vimperator 使用一个 hints 模式，你只要按下 <kbd>f</kbd> 就可以进入该模式，进入 hint 模式后，Vimperator 会给页面内看得见的链接添加标记（默认为数字，可以自定义），然后键入数字就可以直接在当前页打开该链接。意料之中的是，大写的 <kbd>F</kbd> 的作用是在新标签页中打开链接。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-4">历史导航</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-4" href="#i-4"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    打开页面 -> 打开页面 -> &#8230;&#8230; 如此重复几次后，你可能想后退，想前进，这时可以用 <kbd>H</kbd> 后退，<kbd>L</kbd> 前进，也可以 <ctrl-i>/<ctrl-o>来前进后退。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-5">关闭页面</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-5" href="#i-5"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    你想关闭页面，简单一个 <kbd>d</kbd> 就可以关闭当前页面。这时，置为当前的页面是被关闭页面的右侧标签页，如果要激活左侧标签页为当前页面，则是按 <kbd>D</kbd>。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-6">标签页管理</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-6" href="#i-6"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    开了好多个标签页，这时可能需要切换:
  </p>
  
  <p>
    <kbd>gt</kbd> &#8211; 下一个标签页
  </p>
  
  <p>
    <kbd>gT</kbd> &#8211; 上一个标签页
  </p>
  
  <p>
    <kbd>ctrl-n</kbd> &#8211; 下一个标签页
  </p>
  
  <p>
    <kbd>ctrl-p</kbd> &#8211; 上一个标签页
  </p>
  
  <p>
    <kbd>b</kbd> &#8211; 个人觉得是最便利的方法，它通过过滤 url 地址来选择页面
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Vimperator-2">退出 Vimperator</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Vimperator-2" href="#_Vimperator-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    <kbd>:exit</kbd> &#8211; 退出，不保存当前会话历史，下次启动一切再从头
  </p>
  
  <p>
    <kbd>:wqall</kbd> &#8211; 退出，保存当前会话历史，下次启动则恢复此次浏览状况
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-7">帮助</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-7" href="#i-7"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    <kbd>:help</kbd> &#8211; 目前的帮助文件为英文、日文两种语言，没有中文。
  </p>
  
  <div class='timeline'>
    <h2 class="storycontent-h2">
      <span id="i-8">修订历史</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-8" href="#i-8"><span class="" aria-hidden="true">#</span></a>
    </h2>
    
    <ul>
      <li>
        <span itemprop='dateModified'>2015-06-12</span> 修订错误，改善排版
      </li>
    </ul>
  </div>
</div>