---
title: Just Use Sublime Text
author: 陈 三
layout: post
date: 2013-03-26T13:22:45+00:00
url: /just-use-sublime-text.html
dsq_thread_id:
  - 1165931762
views:
  - 2764
categories:
  - 未分类
tags:
  - vim

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#Vim"><span class="toc_number toc_depth_1">1</span> Vim: 你要它好用，则至少要读上两本书</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_Home"><span class="toc_number toc_depth_1">2</span> 把手指放在 Home 行的效率</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#1"><span class="toc_number toc_depth_1">3</span> 插件与扩展能力1: 管理</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#2"><span class="toc_number toc_depth_1">4</span> 插件与扩展能力2: 生态系统</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#3__Vimscript"><span class="toc_number toc_depth_1">5</span> 插件与扩展3: Vimscript</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#4"><span class="toc_number toc_depth_1">6</span> 插件与扩展4: 冲突</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#Vim_1"><span class="toc_number toc_depth_1">7</span> Vim 设计得很糟糕1:太太老了</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#Vim_2GUI"><span class="toc_number toc_depth_1">8</span> Vim 设计得很糟糕2:GUI</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#Vim-2"><span class="toc_number toc_depth_1">9</span> Vim 在缩进时非常差劲</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_Vim"><span class="toc_number toc_depth_1">10</span> 一生的 Vim 路，为了一个可以用的编辑器</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_Vim700_vimrc_45_Vim"><span class="toc_number toc_depth_1">11</span> 在使用四年 Vim，700行手写的 .vimrc 文件及45个插件后，我再也不能真诚推荐别人开始 Vim 旅程</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    <strong>声明</strong>：<a href="http://blog.andrewray.me/just-use-sublime-text/">原文地址</a>，本人仅作翻译，不代表本人所有观点。感谢作者 <a href="https://twitter.com/andrewray">@andrewray</a> 的翻译许可：）。
  </p>
  
  <p>
    最初我只是想回复 <a href="http://www.reddit.com/r/webdev/comments/19lobl/serious_discussion_sublime_text_2_versus_Vim_on/">reddit 上 Sublime Text 2 vs Vim</a> 的问题，但写多了，无法发布，所以我放到博客。
  </p>
  
  <p>
    TL;DR <em>虽然我在用 Vim，但我真的不向一个开发新手推荐它。</em>
  </p>
  
  <h2 class="storycontent-h2">
    <span id="Vim">Vim: 你要它好用，则至少要读上两本书</span><a title="标题链接地址" class="u-floatRight hidden" id="heyVim" href="#Vim"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    对于一般的文本编辑，Vim 并不是一个高效的编辑器。它不会让你输入更快。在使用 Vim 的前一两年时间里，由于那些虽然可爱但也古怪的键绑定，你会发现，它的效率还不如你当前用的编辑器。大约两年后，你才会很熟练。
  </p>
  
  <p>
    每个人都在谈 Vim 陡峭的学习曲线，却没人说，在你总算记住用 hjkl 来移动光标后是怎样。答案是数个月的沮丧后，你终于有一个可以用的编辑器，然后你知道一些很酷的技巧，在你日常工作中，只有1%的机会会用到。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Home">把手指放在 Home 行的效率</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Home" href="#_Home"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    关于 Vim 更高效的论据其实含糊不清，且不可验证。让手去拿鼠标或许真让你慢了下来，但现在开发者们所用的机器上，一般都可以用触控板来移动光标。通过点击屏幕上的字符，大部分新手程序员可以比 Vim 专家们的各式令人发指的招数快多了，比如键入 <kbd>20jFp;</kbd> 又或者 <kbd>/word<cr></kbd> 又或者其他[l]。
  </p>
  
  <p>
    鼠标在于让屏幕上的随意移动变得高效，并且它很擅长。不要妄想你可以打败它。只有在某些极端例子中才能勉强如此。
  </p>
  
  <p>
    关于鼠标的争论还只是次要。真正的问题其实藏得更深。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="1">插件与扩展能力1: 管理</span><a title="标题链接地址" class="u-floatRight hidden" id="hey1" href="#1"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Vim 插件社区有些既顽固又奇怪的缺点。想想看，Vim 大约于<a href="http://en.wikipedia.org/wiki/Vim_(text_editor)">1991年</a>就出来了。Pathogen，第一个被广泛使用、为人们所称赞的路径管理器，于2008年才释出！它让插件管理成为可能，而在那之前，<strong>你只能一遍遍地把插件目录拷入 Vim 文件夹中</strong>。我不开玩笑。甚至还有个狗屎一样的特殊格式用来做这些事，叫做 Vimball(VBA)，它还被人称赞着呢。许多 Vim 插件脚本现在还在用着这种格式。想卸载几个月前你拷入10个文件夹的插件？想升级它？你会疯掉的。
  </p>
  
  <p>
    Vim 吹嘘说它是一个可扩展的、可定制的编辑器，嗯，它是的。它可能是有史来可定制性最强的编辑器，但很可惜，我们直到最近才有一个不错的包管理方法。这太让人担心了。在 Pathogen 后两年多，Vundle 才出来。即便是 pathogen 和 vundle，与 Sublime Text 的 Package Control 插件比起来也差上太多。
  </p>
  
  <p>
    而 Vim 的默认配置让情况变得尤其吓人。我无法再强调，普通的 Vim 是怎样糟糕。要想 Vim 可用，插件是必需。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="2">插件与扩展能力2: 生态系统</span><a title="标题链接地址" class="u-floatRight hidden" id="hey2" href="#2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    <a href="http://www.vim.org/scripts/index.php">Vim Scripts 网站</a>。我吐。想像一下，这简直就是格式少一点、特性少一些、广告多许多的 CPAN 样子嘛。
  </p>
  
  <p>
    大多数的 Vim 插件还不曾转移到 <a href="https://github.com/">Github</a> 项目上。 Vim Scripts 网站作为一个没有特色的托管站点，这也没什么，主要是它没有提供任何的好处。它有一个糟糕的界面，还鼓励用户使用 <a href="http://vim.wikia.com/wiki/Vim_Tips_Wiki">Vim Wiki</a> 进行项目管理(后面还会聊到)。大部分的插件社区就围着这个让人呕吐的网站转。最近看到有[自动转换] Vim 脚本到 Github 项目的努力，也许不错，也许很糟糕。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="3__Vimscript">插件与扩展3: Vimscript</span><a title="标题链接地址" class="u-floatRight hidden" id="hey3__Vimscript" href="#3__Vimscript"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    啊，Vimscript。它很糟糕，而我们还在与其纠缠。如果你想写 Vim 插件，你必须要跟 Vimscript 打交道。它是个非常糟糕的语言。语法有点笨，但这可以原谅。Vimscript 最主要的问题在于，它不是<strong>别</strong>一个语言。没人知道它。大部分我认识的 Vim 老手根本不知道 Vimscript。怎么会这样？因为它的文档非常糟糕，更糟糕的是，要在它上面查找帮助简直是个不可能完成的任务。
  </p>
  
  <p>
    你也许能够在 <a href="http://vim.wikia.com/wiki/Vim_Tips_Wiki">Vim Wiki</a> 上找到一个 Vimscript 教程(试着搜索下，看看它们的搜索是多么的糟糕，又一个不要用它的理由)，但老实说，我觉得大部分作者都有些个性错乱。你找不到友好的、容易理解的、像讲故事一样的教程。它们是由机器及无感情的程序员编写的。
  </p>
  
  <p>
    让我们假设一下，你想写个函数。好的。先看看<strong>函数</strong>的帮助。<code>:help function</code>。好吧，这不是我们想要的。再试试 <code>:help vimscript</code>，我猜是这个？这他妈是什么玩意儿啊。<em>边注：几乎所有的 Vim 帮助都无比难用</em>。幸运的是，有一些好的资源站点存在(<a href="http://learnvimscriptthehardway.stevelosh.com/">Learn Vimscript the Hard Way</a>)。
  </p>
  
  <p>
    即是 Vimmer 也不想学 Vimscript。上帝保佑，希望 Vim 哪天可以有个不是 Vimscript 的语言可以给我们用。曾经有讨论说让 Vim 采用 ECMAScript(<a href="http://www.mail-archive.com/vim-dev@vim.org/msg03698.html">Re:replace VimScript</a>)，不过没人有勇气尝试，包括我自己。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="4">插件与扩展4: 冲突</span><a title="标题链接地址" class="u-floatRight hidden" id="hey4" href="#4"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    这是个大问题。Vim 缺乏现代编辑器所需的大量核心功能。比如 ctag 的整合，项目管理，项目浏览，(当然，我知道 :Sex 命令)，以及其他一些基本的东西，在 Vim 中全都没有。这是因为设计时 Vim 根本就没打算编辑任何一个语言，可能 C 除外。这再坏不过了。理论上说，借由它的扩展能力，Vim 可以编辑任何一种语言，虽然在面对大型语言如 Java 或 Scala 时会有些难过。
  </p>
  
  <p>
    嗯，我们需要一个项目式的文件浏览器。试试 <a href="https://github.com/scrooloose/nerdtree">NERDTree</a>，很多人知道它。可是等等，在我关闭缓存时，NERDTree 总是会让某些莫名东西打开着。大部分人不知道 <a href="https://github.com/jistr/vim-nerdtree-tabs">NERDTree tabs</a>，可是没有它 NERDTree 是不完整的。嘿，而且由于 Vim 对整个 UI(后面还会聊到更多) 使用 monospace 字体的限制，界面看起来糟糕透了。不过我想这还不算太坏&#8230;
  </p>
  
  <p>
    现在我们想找文件。试试 Vimgrep! 等一下，这个太烂。好吧，让我们试下 <a href="http://www.vim.org/scripts/script.php?script_id=3025">Command-T</a>。等一下，这个让人难以置信的慢，又笨重，看起来不好使。嗯，<a href="https://github.com/kien/ctrlp.vim">CtrlP</a> 好使点！可是它在做<a href="https://github.com/kien/ctrlp.vim/issues/110">模糊搜索时</a> 并不太对头，给我的结果也不准确。我是想要又慢又蠢呢，还是想快一点但却是错的？又或者我想操它丫的。
  </p>
  
  <p>
    Sublime Text 的 Command-T 则运作正常，非常地不错，扫描文件也异常轻松。[2]
  </p>
  
  <p>
    找到对的 Vim 插件就好像处在一个高级俱乐部里。大约在2年后你才会感觉好点，然后第3年又开始糟糕，然后&#8230;
  </p>
  
  <p>
    回到冲突问题。由于 Vim 默认提供太少功能，以至于有太多的插件出现功能重复。需要 snippet 补齐？好，用 <a href="http://www.vim.org/scripts/script.php?script_id=2540">snipMate</a>！可是等等，<a href="https://github.com/SirVer/ultisnips">UltiSnips</a> 要更好！再等等，如果你用 <a href="https://github.com/Shougo/neocomplcache">neocomplcache</a>，则前面两个都可以见鬼去了(边注，即使有人提供1千亿，我也无法选个比 &#8216;neocomplcache&#8217; 更糟糕的名称。)。现在则可以用 <a href="https://github.com/Shougo/neosnippet">neosnippet</a>！可是等等，如果你还有其他的自动补齐插件，它就无法工作了！所有的这些插件都保证毁掉 Vim 默认的、本已经复杂、混乱的自动补齐功能。
  </p>
  
  <p>
    你的搜索插件会跟你的自动补齐插件冲突。你的语法插件会跟你的词典冲突。冲突是什么意思？它意味着 Vim 会随机吐出500行红色高亮的文字给你，但是只有一秒，就只是让你知道有什么东西被你弄坏了。在使用 <a href="http://www.vim.org/scripts/script.php?script_id=1682">indexed-search</a>(你显然想要这个功能，但操蛋的是 Vim 默认并不提供) 时，如果你搜索的正则表达式非法，你会得到一些神秘的错误，里面有你从来没见过的函数名称。你会在启动 Vim 时看到大量闪过的红色文字，你读不到，拷不到，也保存不了，2秒后，它们就没了，然后突然的，你的编辑器慢得跟狗一样，然后你就得开始追捕插件女巫了[3]。
  </p>
  
  <p>
    啊，Vim 的扩展性。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="Vim_1">Vim 设计得很糟糕1:太太老了</span><a title="标题链接地址" class="u-floatRight hidden" id="heyVim_1" href="#Vim_1"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    每个人都将 <kbd>Leader</kbd> 值从反斜杠重映射给逗号。反斜杠被选中是因为，大约在1943年或其他什么年份里，它很容易敲到。而在现代键盘上，它的位置就太可怕了。重映射覆盖了逗号这个有用的击键，但为了避免古老的反斜杠 leader，这还是值得的。
  </p>
  
  <p>
    你知道在 Vim 中处理多文件的建议方法是什么吗？是 arglist。大部分我的 Vim 老手朋友即不用 arglist 也不知道它是什么鬼玩意儿。这是个笨重的系统，用于把多文件填充到 Vim 的一个特殊内部列表中。有时它确实挺好用的(配合一些插件)，可是，你整个 Vim 职业中可能只会用到三次。这是 Vim 的一个古怪而且过时、偏门的瑕疵。你会需要知道它的，大概在2.5年的时候。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="Vim_2GUI">Vim 设计得很糟糕2:GUI</span><a title="标题链接地址" class="u-floatRight hidden" id="heyVim_2GUI" href="#Vim_2GUI"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Vim 设计于终端窗口中运行。这是为什么它的 GUI 明确地绑定给 monospaced 字体。终端窗口无法绘制 UI。我明白，我们得要用块或下划线或你所有的什么来绘制东西。好吧。我是在服务器上，我编辑文件可能只是对一些问题做个热修复，我不需要一个漂亮的编辑器来做这种工作。我只是需要编辑文件。
  </p>
  
  <p>
    但是 Vim 注定是一个你在服务器上不必要经常用的编辑器。在服务器上，你也可以用 <a href="http://en.wikipedia.org/wiki/Pico_(text_editor)">Pico</a>，但没人长期用 Pico 编辑。后来，我们有了这些叫 GUI 的东西。它们真不错，很好看，也可用，并且针对事物会给出可视的象征。于是我们自然而然地希望我们的运行在 GUI 上的编辑器可以提供这些好处。
  </p>
  
  <p>
    你知道比起终端的 Vim，<a href="https://code.google.com/p/macvim/">MacVim</a> 带来什么好处吗，视觉上的。它有样式化的标签页。这就是我们所得到的，也会是我们未来所会得到的。文件不能也不会仅为了可读性而填充空白。你不能一次在屏幕上显示一种以上字体大小。如果你要放大你的缓存广西，你同时放大了你的文件浏览器，你的命令行，你的状态栏。如果你想要一个可读性强点，非 monospaced 字体来样式化一个对话框，我想你会很忧伤的。
  </p>
  
  <p>
    Vim 设计得很丑陋。它看起来就好像一个刚开始学会用 bash script 画牛的小孩做出来的。我们永远不会有 <a href="http://programmers.stackexchange.com/questions/156362/does-sublimes-minimap-improve-productivity">minimap</a>(一个非常漂亮的特性)。我们永远不会有多个光标。我们永远不会有一个漂亮的模糊文件查找工具，它会在合理的位置跳出来。我们不能为可用性把对话框摆放在任意地方。我们永远不会有一个可定制的对话框。你可以有的最接近的是 <a href="https://github.com/Lokaltog/vim-powerline">vim-powerline</a>，但它仍是用块画出来的。老实说，Vim 的 UI 老了。当然，我主要是编辑文本，但我一天中大部分时候在使用它。我希望它看起来不错，让人感觉好点。Vim 有许多灵巧的装饰物，但大部分只是暴露出一个问题：我们没有真正的 GUI。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="Vim-2">Vim 在缩进时非常差劲</span><a title="标题链接地址" class="u-floatRight hidden" id="heyVim-2" href="#Vim-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    不相信？好，将下面代码粘贴到一个空缓存中：
  </p>
  
  <pre><code>&lt;div&gt;
&lt;p&gt;
&lt;span&gt;foo&lt;/span&gt;
&lt;/p&gt;
&lt;/div&gt; 
</code></pre>
  
  <p>
    <code>:set ft=html</code> 然后 <kbd>gg=G</kbd>。让我知道你看到什么了。说实在的，请不要告诉我你看到了什么。
  </p>
  
  <p>
    因为某些奇迹的原因，Vim 在大多数缩进时非常差劲。你因为忘记正确缩进你的 JavaScript 文件，并且在使用 <code>cindent</code>、<code>smarttab</code> 及 <code>shiftwidth</code> 搞乱了一切后，你向插件求助，你会找到 <a href="https://github.com/pangloss/vim-javascript">javascript.vim</a>，可是它运行得不太对，虽然也还有个分支版，可惜也有错误，然后还有些人给插件取同样的名字却完全不是一个内容。我不知道为什么事情会这么混乱，也许是我的错误，没有好好调查清楚，可是为什么竟然还要我自己配置我的编辑器来缩进常见语言？你早该知道的，Vim。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Vim">一生的 Vim 路，为了一个可以用的编辑器</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Vim" href="#_Vim"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    *要在 Vim 中写程序，你得把程序跟 Vim 一起记在脑子里，你必须不停地想想你正在做什么。
  </p>
  
  <p>
    也许这是件好事。也许它鼓励程序的高效与改进。可是你知道吗，我不想应付这些。我不想自己必须记住 <kbd>@@</kbd> 是做什么的，<code>:v/\v</code> 又是做什么的，又或其他一堆东西仅为完成基本任务。虽然如此，我还是每周花至少一小时来练我的 Vim 功夫。但我真不想这样。我想编辑文件。我不想因为碰上一个难解的问题然后就得阅读另一篇教程仅为了可以正确重命名一个函数。我只是想做出东西。也许它是权宜之计。也许第10年时它一切就都值得了，因为我不用再为了做事而先想事。我不知道。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Vim700_vimrc_45_Vim">在使用四年 Vim，700行手写的 <a href="https://github.com/DelvarWorld/configs/blob/master/.vimrc">.vimrc</a> 文件及45个插件后，我再也不能真诚推荐别人开始 Vim 旅程</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Vim700_vimrc_45_Vim" href="#_Vim700_vimrc_45_Vim"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    我希望我的同事能快速编辑文件。告诉他们使用 Vim 是否会是答案？它只会让他们数个月内都变慢。在科技行业中，这不实用。也许长期来看是有好处。又或者我只是不想应付它们的 Vim 旅程。
  </p>
  
  <p>
    你看，小子，我喜欢你们，所以用 <a href="http://www.sublimetext.com/">Sublime Text</a> 吧。虽然事实是我是在 Vim 里写的这篇 post，因为我实在无法容忍在文本区域中写，大部分时候我只是输入文字，但我还是无法容忍。我是如此想念我的 Vim 移动方法。对的，我可能永远不会停止使用 Vim。
  </p>
  
  <p>
    你将要且必须了解 Vim。如果你无法远程编辑文本，在科技世界里，你将没什么用。你会在一个终端窗口中，你会用 Vim 编辑。在 bash 里，如果不通过命令行输入 <code>set -o vi</code> 把键绑定设置为 Vi 的，你就觉得活不下去了，而我也会一直歧视你直到你真的开始使用它&#8230;
  </p>
  
  <p>
    但是 Sublime 有 Vim 所没能有的东西。它是新的热门，有一个比 Vim 更加活跃的社区。而在过去一年中，如果你看到一个 Vim 插件更新了，那你真是太幸运了(不是我在贬低超级名星如 <a href="https://twitter.com/tpope">Tim Pope</a> 那惊人的贡献，而是像他这样让人着迷的真的极少)。
  </p>
  
  <p>
    Vim 是一个 <a href="http://www.rayninfo.co.uk/vimtips.html">毕生的旅程</a>。即如现在，我想把我写的这80列宽的文本转换成不固定宽度的文本，我得去找找看怎么才能搞定。也许在这过程中我还能学到点什么。在四年的使用 Vim 后。
  </p>
  
  <p>
    如果你发现 Sublime 不适合你，又或者觉得你失去了什么，那你可以试试 Vim。但只要一点点 Vim 知识就可以让你勉强应付服务器上编辑文件，你也可以使用 <code>set -o vi</code>，无需读一本书。
  </p>
  
  <p>
    我的观点可能会在几年后改变，但是目前，如果你需要做个选择，请用 Sublime Text.
  </p>
  
  <p>
    (噢，选择整个文本对象，然后 <code>:set tw=1000 | norm gqie</code>，好傻)
  </p>
  
  <p>
    <strong>译注</strong>：以下为翻译有疑问的地方：
  </p>
  
  <p>
    [1] Most novice programmers can click on a character on screen faster than an expert Vimmer can type 20jFp; or LkEEE or /word<cr> or any other nasty way Vimmers have to use because of our archaic, ingrained keystrokes.
  </p>
  
  <p>
    [2] Padding around your text to make it readable? What a concept!
  </p>
  
  <p>
    [3] You’ll see a huge red flash of text at startup that you can’t read, copy, nor save, and it goes away after 2 seconds, and suddenly your editor is slow a dog and you have to go plugin witch hunting.
  </p>
</div>