---
title: Surround.vim
author: 陈 三
layout: post
date: 2012-09-30T13:09:14+00:00
url: /surround-vim.html
views:
  - 1163
dsq_thread_id:
  - 865291868
categories:
  - Ubuntu
tags:
  - vim script

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 修改符号</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 删除符号</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-3"><span class="toc_number toc_depth_1">3</span> 增加符号</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-4"><span class="toc_number toc_depth_1">4</span> 扩展阅读</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    如下的一段代码，如果要删除得只剩下内容该如何：
  </p>
  
  <pre><code>&lt;div class="vim"&gt;
    &lt;p&gt;
        &lt;em&gt;hi this is surround.vim from tim tpope&lt;em&gt;
    &lt;/p&gt;
&lt;/div&gt;
</code></pre>
  
  <p>
    如果在 vim 里，可以这样操作：先定位到 <div class=&#8221;vim&#8221;> 行，然后按 <kbd>2dd</kbd>，之后再定位到 </p> 行，再 <kbd>2dd</kbd>，然后剩下 em 一对标签。
  </p>
  
  <p>
    这一对 em 看着不太好删。
  </p>
  
  <p>
    这时，如果有安装 <a href="https://github.com/tpope/vim-surround">surround.vim</a> 的话，只要按 <kbd>dst</kbd> 就可以轻松删除一对 em 标签。
  </p>
  
  <p>
    Surround.vim 是一个 Vim 插件，用于管理 <strong>() [] <> &#8220;&#8221; &#8221; 及 html、xml 标签等成双成对出现的符号</strong>。用它可以很方便地<strong>删除/修改/增加</strong>这些符号，譬如上面所述的例子。
  </p>
  
  <p>
    显然，上面的例子可以通过按三次的 dst 来删除，但那样显然不够高效，因为要按 9 次字母键，如果能 3dst 这样配合数字使用就很简单。又或者调用 Vim 的重复命令按键 &#8220;.&#8221; （点号）。但目前来看，这个插件并不支持配合数字的操作，可能是意义不大，毕竟所举的案例其实很偏门；另外，Vim 里点号所重复的命令只是重复最后一次原生命令，而无法重复映射过的“整”命令。
  </p>
  
  <p>
    于是，Tim Tpope 还写了一个 <a href="https://github.com/tpope/vim-repeat">repeat.vim 的插件</a>，解决点号重复命令的问题。
  </p>
  
  <p>
    于是上述案例的解决办法变成，先按一次 <kbd>dst</kbd>，然后两次点号，这回按了 5 次按键。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">修改符号</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    以下例子中 * 表示光标位置。
  </p>
  
  <p>
    &#8220;hello w*orld&#8221; &rarr; <kbd>cs"'</kbd> &rarr; &#8216;hello world&#8217;
  </p>
  
  <p>
    可以把 cs 理解为 change surround，把 &#8221; 修改为 ‘。
  </p>
  
  <p>
    ‘hello wor*ld’ &rarr; <kbd>cs‘<q></kbd> &rarr; <q>hello world</q>
  </p>
  
  <p>
    <q>hello *world</q> &rarr; <kbd>cst"</kbd> &rarr; &#8220;hello world&#8221;
  </p>
  
  <p>
    cst 表示 change surround tag，t 表示 xml/html 成对出现的标签。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">删除符号</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    类于修改符号，删除只是换个按键，把 c 换成 d。则要删除包围的双引号可以用 ds&#8221; &#8211; delete surround &#8220;，要删除标签对，则用 <kbd>dst</kbd> &#8211; delete surround tag。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-3">增加符号</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-3" href="#i-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    如果要增加符号，比如字符串 hello，要用双引号包围，则可以按 <kbd>ysiw"</kbd>，按 surround.vim 帮助说明，可以把 y 记忆成 you，于是 <kbd>ysiw"</kbd> 意指 you surround inner word &#8220;，同理，要用标签对的话则是按 <kbd>ysiw<p></kbd>，另外，surround.vim 还提供包围整行的方法，<kbd>yss"</kbd> &#8211; you surround sentence &#8220;；至于在增加 [] () <> 这样的符号时，有一点小小区别，比如 hello 这个单词，<kbd>ysiw[</kbd> 会生成 [ hello ]，ysiw] 会成生 [hello]，hello 前后少一个空格，删除、修改亦然。
  </p>
  
  <p>
    如果要包围单行里的两个单词甚至更多，则可以使用可视模式，先进入 vim 的可视化模式选中要包围的单词，然后按 <kbd>S"</kbd> 就可以把这些单词用双引号包围。
  </p>
  
  <p>
    非常便利。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-4">扩展阅读</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-4" href="#i-4"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <a href="http://www.zfanw.com/blog/vundle-vim-plugin-management.html">vim 插件安装的便利方法</a>
    </li>
    <li>
      <a href="https://github.com/tpope">Tim Tpope 的各种其他 vim 插件</a>
    </li>
  </ol>
</div>