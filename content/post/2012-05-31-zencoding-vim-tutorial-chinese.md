---
title: Emmet.vim 教程
author: 陈 三
layout: post
date: 2012-05-31T10:03:03+00:00
url: /zencoding-vim-tutorial-chinese.html
views:
  - 16496
dsq_thread_id:
  - 709330743
dsq_needs_sync:
  - 1
categories:
  - 前端开发
tags:
  - vim
  - zencoding.vim

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_Emmetvim"><span class="toc_number toc_depth_1">1</span> 下载 Emmet.vim</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_Emmetvim-2"><span class="toc_number toc_depth_1">2</span> 安装 Emmet.vim</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_Emmetvim-3"><span class="toc_number toc_depth_1">3</span> 使用 Emmet.vim</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">4</span> 余话</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    Emmet 项目原先叫 Zen Coding，2012年的时候，项目启用新名称 <a href="http://emmet.io/">Emmet</a>。
  </p>
  
  <p>
    Emmet 官方支持<a href="http://emmet.io/download/">很多文本编辑器/IDE</a>，但 <a href="https://github.com/mattn/emmet-vim/">Emmet.vim</a> 并非 Emmet 亲生，它是由日本 <a href="http://mattn.kaoriya.net/">Yasuhiro Matsumoto</a> 开发。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Emmetvim">下载 Emmet.vim</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Emmetvim" href="#_Emmetvim"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    你可以从两个地址下载，一是 <a href="http://www.vim.org/scripts/script.php?script_id=2981">Vim 插件站点</a>，一是 <a href="https://github.com/mattn/emmet-vim/">Github</a>。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Emmetvim-2">安装 Emmet.vim</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Emmetvim-2" href="#_Emmetvim-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    将下载的压缩包解压到 .vim 目录下：
  </p>
{{< highlight bash >}}
  cd ~/.vim
  unzip emmet-vim.zip
{{</ highlight >}}
  <p>
    如果你使用 <a href="http://www.vim.org/scripts/script.php?script_id=2332">pathogen.vim</a> 管理 Vim 插件：
  </p>
  
{{< highlight bash >}}
  cd ~/.vim/bundle
  unzip /path/to/emmet-vim.zip
{{</ highlight >}}
  
  <p>
    或者直接从 Github 库克隆一份：
  </p>

{{< highlight bash >}}
  cd ~/.vim/bundle
  git clone http://github.com/mattn/emmet-vim.git
{{</ highlight >}}
  
  <p>
    个人建议通过 Pathogen 或 <a href="http://www.zfanw.com/blog/vundle-vim-plugin-management.html">Vundle</a> 来安装。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Emmetvim-3">使用 Emmet.vim</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Emmetvim-3" href="#_Emmetvim-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    以下内容译自 <a href="https://github.com/mattn/emmet-vim/blob/master/TUTORIAL">Emmet.vim tutorial（Aug 6, 2013）</a>，感谢<a href="http://twitter.com/mattn_jp">作者</a>。
  </p>
  
  <h3>
    1. 展开
  </h3>
  
  <p>
    键入 <code>div&gt;p#foo$*3&gt;a</code> 然后按快捷键 <kbd>&lt;c-y&gt;,</kbd> &#8211; 表示 <<strong>Ctrl-y</strong>> 后再按<strong>逗号</strong>，不妨把 <kbd>Ctrl-y</kbd> 看成 emmet 指令的启动，就像 Vim 的 <kbd>:</kbd> 表示进入命令行模式。
  </p>
  
{{< highlight html >}}
&lt;div&gt;
    &lt;p id="foo1"&gt;
        &lt;a href=""&gt;&lt;/a&gt;
    &lt;/p&gt;
    &lt;p id="foo2"&gt;
        &lt;a href=""&gt;&lt;/a&gt;
    &lt;/p&gt;
    &lt;p id="foo3"&gt;
        &lt;a href=""&gt;&lt;/a&gt;
    &lt;/p&gt;
&lt;/div&gt;
{{< /highlight >}}
  
  <h3>
    2. 外部包住
  </h3>
  
  <p>
    如下内容：
  </p>
  
{{< highlight text >}}
  test1
  test2
  test3
{{< /highlight >}}
  
  <p>
    按大写的 <code>V</code> 进入 Vim 可视模式，“行选取”上面三行内容，然后按键 <kbd>&lt;c-y&gt;,</kbd>，这时 Vim 的命令行会提示 `Tags:`，键入 `ul&gt;li*`，然后按 <kbd>Enter</kbd>，结果如下：
  </p>

{{< highlight html >}}
&lt;ul&gt;
    &lt;li&gt;test1&lt;/li&gt;
    &lt;li&gt;test2&lt;/li&gt;
    &lt;li&gt;test3&lt;/li&gt;
&lt;/ul&gt;
{{</ highlight >}}
  
  <p>
    而假如输入的 tag 是 blockquote&#8217;，则结果会变成下面这样：
  </p>
  
{{< highlight html >}}
&lt;blockquote&gt;
    test1
    test2
    test3
&lt;/blockquote&gt;
{{</ highlight >}}
  
  <h3>
    3.插入模式下根据光标位置选中整个标签
  </h3>
  
  <p>
    按 <kbd>&lt;c-y&gt;d</kbd>
  </p>
  
  <h3>
    4.插入模式下根据光标位置选中整个标签内容
  </h3>
  
  <p>
    按 <kbd>&lt;c-y&gt;D</kbd>
  </p>
  
  <h3>
    5.跳转到下一个编辑点
  </h3>
  
  <p>
    插入模式下按 <kbd>&lt;c-y&gt;n</kbd>
  </p>
  
  <h3>
    6.跳转到上一个编辑点
  </h3>
  
  <p>
    插入模式下按 <kbd>&lt;c-y&gt;N</kbd>
  </p>
  
  <h3>
    7.更新图片大小
  </h3>
  
  <p>
    移动光标到 img 标签。
  </p>
  
  {{< highlight html >}}
  &lt;img src="foo.png" /&gt;
  {{</ highlight >}}
  
  <p>
    然后按 <kbd>&lt;c-y&gt;i</kbd>，结果如下：
  </p>
  
  {{< highlight html >}}&lt;img src="foo.png" width="32" height="48" /&gt;
{{</ highlight >}}
  
  <p>
    注：仅适用本地图片，互联网上的图片并无法取得其大小。
  </p>
  
  <h3>
    8.合并行
  </h3>
  
  <p>
    选择下面的所有 `&ltli&gt;` 行
  </p>
  
{{< highlight html >}}
&lt;ul&gt;
    &lt;li class="list1"&gt;&lt;/li&gt;
    &lt;li class="list2"&gt;&lt;/li&gt;
    &lt;li class="list3"&gt;&lt;/li&gt;
&lt;/ul&gt;
{{</ highlight >}}
  
  <p>
    然后按 <kbd>&lt;c-y&gt;m</kbd>，结果如下：
  </p>
  
{{< highlight html >}}&lt;ul&gt;
    &lt;li class="list1"&gt;&lt;/li&gt;&lt;li class="list2"&gt;&lt;/li&gt;&lt;li class="list3"&gt;&lt;/li&gt;
&lt;/ul&gt;
{{</ highlight >}}
  
  <h3>
    9.移除标签对
  </h3>
  
  <p>
    首先，移动光标到块中
  </p>
  
{{< highlight html >}}&lt;div class="foo"&gt;
    &lt;a&gt;cursor is here&lt;/a&gt;
&lt;/div&gt;
{{</ highlight >}}
  
  <p>
    然后在插入模式下按 <kbd>&lt;c-y&gt;k</kbd>，结果如下：
  </p>

{{< highlight html >}}&lt;div class="foo"&gt;
&lt;/div&gt; 
{{</ highlight >}}
  
  <p>
    再次按 <kbd>&lt;c-y&gt;k</kbd> 则上面代码块中连 div 标签块都会被移除。
  </p>
  
  <h3>
    10.分割/合并标签
  </h3>
  
  <p>
    首先，移动光标到块中
  </p>
  
  {{< highlight html >}}&lt;div class="foo"&gt;
    cursor is here
&lt;/div&gt;
{{</ highlight >}}
  
  <p>
    在插入模式下按 <kbd>&lt;c-y&gt;j</kbd>：
  </p>
  
  {{< highlight html >}}&lt;div class="foo"/&gt;
{{</ highlight >}}
  
  <p>
    再次按 <kbd>&lt;c-y&gt;j</kbd>：
  </p>
  
  {{< highlight html >}}&lt;div class="foo"&gt;

&lt;/div&gt;
{{</ highlight >}}
  
  <h3>
    11.切换注释
  </h3>
  
  <p>
    首先，移动光标到块中
  </p>
  
  {{< highlight html >}}&lt;div&gt;
    hello world
&lt;/div&gt;
{{</ highlight >}}
  
  <p>
    插入模式中按 <kbd>&lt;c-y&gt;/</kbd>：
  </p>
  
  {{< highlight html >}}&lt;!-- &lt;div&gt;
    hello world
&lt;/div&gt; --&gt;
{{</ highlight >}}
  
  <p>
    再按 <kbd>&lt;c-y&gt;/</kbd> 则恢复：
  </p>
  
  {{< highlight html >}}&lt;div&gt;
    hello world
&lt;/div&gt;
{{</ highlight >}}
  
  <h3>
    12.从 URL 地址生成锚
  </h3>
  
  <p>
    将光标移至 URL
  </p>
  
  {{< highlight html >}}http://www.google.com/
{{</ highlight >}}
  
  <p>
    按 <kbd>&lt;c-y&gt;a</kbd>
  </p>
  
  {{< highlight html >}}&lt;a href="http://www.google.com"&gt;&lt;/a&gt;
{{</ highlight >}}
  
  <h3>
    13.从 URL 地址生成引用文本
  </h3>
  
  <p>
    移动光标到 URL
  </p>
  
  {{< highlight html >}}http://github.com/
{{</ highlight >}}
  
  <p>
    按 <kbd>&lt;c-y&gt;A</kbd>
  </p>
  
  {{< highlight html >}}&lt;blockquote class="quote"&gt;
    &lt;a href="http://github.com/"&gt;&lt;/a&gt;&lt;br /&gt;
    &lt;p&gt;...&lt;/p&gt;
    &lt;cite&gt;http://github.com/&lt;/cite&gt;
&lt;/blockquote&gt;
{{</ highlight >}}
  
  <h3>
    14.安装 Emmet.vim
  </h3>
  
  <p>
    见文章头部。
  </p>
  
  <h3>
    15.为你所用的语言启用 Emmet.vim
  </h3>
  
  <p>
    你可以为你用的语言自定义行为。
  </p>
  
  {{< highlight html >}}# cat &gt;&gt; ~/.vimrc
let g:user_emmet_settings = {
\ 'php' : {
\ 'extends' : 'html',
\ 'filters' : 'c',
\ },
\ 'xml' : {
\ 'extends' : 'html',
\ },
\ 'haml' : {
\ 'extends' : 'html',
\ },
\}
{{</ highlight >}}
  
  <h2 class="storycontent-h2">
    <span id="i">余话</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    除了以上帮助，你还可以按<strong>:</strong>进入 Vim 命令行模式，然后输入 <code>help emmet</code> 在新窗口中调用 Emmet 的帮助内容。
  </p>
  
  <p>
    Emmet 在其他编辑器的触发快捷键一般是 <kbd>Tab</kbd> 或 <kbd>Ctrl+e</kbd>，如果你更习惯它们，也可以在 .vimrc 文件中加入下一行命令来修改它的触发快捷键：
  </p>
  
  {{< highlight html >}}let g:user_emmet_expandabbr_key = '&lt;Tab&gt;'
{{</ highlight >}}
  
  <p>
    这样就可以按 <kbd>Tab</kbd> 来扩展了。
  </p>
  
  <p>
    <strong>附</strong>:
  </p>
  
  <ol>
    <li>
      <a href="https://zen-coding.googlecode.com/files/ZenCodingCheatSheet.pdf">ZenCoding cheatsheet</a>
    </li>
  </ol>
</div>