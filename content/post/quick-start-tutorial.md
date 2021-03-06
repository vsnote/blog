---
title: Vimperator 快速入门教程
author: 陈 三
layout: post
date: 2011-01-03T04:50:43+00:00
url: /quick-start-tutorial.html
Views:
  - 1
dsq_thread_id:
  - 458449010
categories:
  - vimperator
tags:
  - vimperator

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 模式化界面</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 找到帮助</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-3"><span class="toc_number toc_depth_1">3</span> 无鼠标化</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-4"><span class="toc_number toc_depth_1">4</span> 滚动</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-5"><span class="toc_number toc_depth_1">5</span> 历史与标签</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-6"><span class="toc_number toc_depth_1">6</span> 网页浏览贴士</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-7"><span class="toc_number toc_depth_1">7</span> 常见问题</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-8"><span class="toc_number toc_depth_1">8</span> 保存配置</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-9"><span class="toc_number toc_depth_1">9</span> 退出</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#Firefox"><span class="toc_number toc_depth_1">10</span> Firefox 哪儿去了</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-10"><span class="toc_number toc_depth_1">11</span> 把我弄出去</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-11"><span class="toc_number toc_depth_1">12</span> 修订历史</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    <strong>注</strong>：本文译自 vimperator 英文帮助文档。
  </p>
  
  <p>
    这是一个 <a href="http://vimperator.org/" title="vimperator 官网">Vimperator</a> 快速入门教程，帮助新用户迅速上手 Vimperator。但它没打算像完整参考书那样，解释方方面面的内容。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">模式化界面</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Vimperator 的强大，就像 Vim 那样，来自它的模式。浏览器所处模式不同，则键击的意义不同。Vimperator 有许多模式，其中最重要的两个是<strong>普通模式（Normal Mode）</strong>、<strong>命令行模式（Command-Line Mode）</strong>。
  </p>
  
  <p>
    Vimperator 启动时，默认进入<strong>普通模式</strong>，这也会是你使用最多的模式。
  </p>
  
  <p>
    Vimperator 另一个核心模式，<strong>命令行模式</strong>，可以在<strong>普通模式</strong>下键入一个冒号 <code>:</code> 进入。接下来你会经常看到冒号 <code>:</code> 打头的 Vimperator 命令，意味着冒号后面跟着的是命令。
  </p>
  
  <p>
    要从<strong>命令行模式</strong>返回<strong>普通模式</strong>，只要按 <kbd><Esc></kbd> 键就可以。大部分时候，按 <kbd><Esc></kbd> 键也可以让你从 Vimperator 的其他模式返回到<strong>普通模式</strong>。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">找到帮助</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Vim 是个当得起“伟大”二字的编辑器，但它不是浏览器。因此，即便是有经验的 Vim 用户可能也需要不时查阅 Vimperator 文档。Vimperator 的大部分特性都可以通过 <kbd>:help</kbd> 命令找到。例如，你可以键入下列命令来查看关于 <code>:help</code> 命令的帮助。
  </p>
  
  <pre><code>:help :help
</code></pre>
  
  <p>
    类似的，配置选项的帮助可以通过 <kbd>:help '选项名称'</kbd>找到。（注意选项名称外加单引号是跟 Vim 一样的。）如你所预料的，所有可用选项的资料都可以通过 <kbd>:help options</kbd> 来取得。
  </p>
  
  <p>
    另外你可以使用以下命令找出 <kbd>gt</kbd> 与 <kbd>gT</kbd> 映射的帮助：
  </p>
  
  <pre><code>:help gt
</code></pre>
  
  <pre><code>:help gT
</code></pre>
  
  <p>
    最后，除了帮助系统本身外，<code>:usage</code> 也是有用的快速参考命令。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-3">无鼠标化</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-3" href="#i-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Vimperator 的高效，正如它的灵感来源、传奇编辑器 Vim 一样，在于用户的手指保持在键盘上即可完成大部分工作。当然，在某些领域里鼠标要比键盘擅长，比如 GUI 设计或某些游戏，但 Vimperator 假定了浏览器不必要变成它们之一。不过 Vimperator 还是完全支持鼠标的，如果你更乐于动动这啮齿动物。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-4">滚动</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-4" href="#i-4"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    简单的击键就可滚动浏览器窗口
  </p>
  
  <ul>
    <li>
      <kbd>j</kbd>、<kbd>k</kbd>&#8212;逐行上下滚动窗口
    </li>
    <li>
      <kbd>h</kbd>、<kbd>l</kbd>&#8212;左右滚动窗口
    </li>
    <li>
      <kbd><Space></kbd>、<kbd><C-f></kbd>、<kbd><C-b></kbd>&#8212;逐屏上下滚动
    </li>
    <li>
      <kbd><C-d></kbd>、<kbd><C-u></kbd>&#8212;上下滚动半页
    </li>
  </ul>
  
  <p>
    <kbd><Up></kbd>、<kbd><Down></kbd>、<kbd><PgUp></kbd>、<kbd><PgDn></kbd> 也你所预期一样工作。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-5">历史与标签</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-5" href="#i-5"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    历史导航（如后退，前进）功能类似于滚动。
  </p>
  
  <ul>
    <li>
      <kbd><C-o></kbd>、<kbd><C-i></kbd> &#8211; 在当前（窗口/标签）的历史中后退/前进
    </li>
  </ul>
  
  <p>
    使用键击在标签页间切换与 Vim 标签页间切换相仿。
  </p>
  
  <ul>
    <li>
      <kbd>gt</kbd>、<kbd><C-n></kbd>&#8212;下一个标签页
    </li>
    <li>
      <kbd>gT</kbd>、<kbd><C-p></kbd>&#8212;上一个标签页
    </li>
    <li>
      <kbd>g0</kbd>（注意，g 后面是个数字而非字母）、<kbd>g$</kbd>&#8212;第一个/最后一个标签页
    </li>
    <li>
      <kbd>d</kbd>&#8212;关闭当前标签页（删除 buffer）
    </li>
  </ul>
  
  <p>
    要在新标签页中打开网页，则命令行模式中输入 <code>:tabopen url</code>。要在当前标签页中打开一个网址，则使用 <code>:open</code>。普通模式下这两个命令被映射为 <kbd>t</kbd> 与 <kbd>o</kbd>，因此如下的两对命令结果是相当的:
  </p>
  
  <pre><code>:open my.webmail.com

omy.webmail.com
</code></pre>
  
  <pre><code>:tabopen vimperator.org

tvimperator.org
</code></pre>
  
  <h2 class="storycontent-h2">
    <span id="i-6">网页浏览贴士</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-6" href="#i-6"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    现在你已经可以在 Vimperator 里进行导航了。但等一下，你该如何打开一个网页中的链接？没了你带尾巴的朋友，你如何点击这些链接？
  </p>
  
  <p>
    答案是 “hint”。启用 “hint” 模式会在每一个 Vimperator 找到的链接旁显示一组数字。要点击这些链接，只需输入红色方框围住的数字即可。
  </p>
  
  <p>
    对于文字链接，则有另外的快捷方式，你可以键入某些链接文字，Vimperator 会搜寻所有它能找到的链接，并高亮显示符合的链接，当其唯一时，Vimperator 会自动打开链接，不需要任何额外的用户输入。
  </p>
  
  <p>
    无论你选择哪种方法来指定你的目标链接，一旦 Vimperator 高亮显示你要的链接，单击<kbd><Enter></kbd> 即打开链接。
  </p>
  
  <p>
    最常见的 hint 模式叫做 quick-hints。要打开<strong>快速提示</strong>，单击 <kbd>f</kbd> 或 <kbd>F</kbd>。小写的 f 键在当前标签页打开链接，大写的 F 则在新的标签页打开链接。
  </p>
  
  <p>
    测试一下吧。你可以试试这个链接，<a href="http://vimperator.org/" title="vimperator 主页">Vimperator 主页</a>。按 <kbd>f</kbd> 或 <kbd>F</kbd> 激活“快速提示”模式，高亮显示当前所有的可见链接。然后键入链接的文字。链接迅速被定位，Vimperator 自动打开它。一旦你完成测试，记得使用 <kbd><C-o></kbd>（后退）或者 <kbd>d</kbd> 回到这个帮助页 &#8211; 具体哪个取决于你按哪个键激活“<strong>快速提示</strong>”模式。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-7">常见问题</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-7" href="#i-7"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    假如你输入新的网址到一半，发现已经在前一个标签页中打开了，这时你的命令行看起来可能像这样:
  </p>
  
  <pre><code>:open my.partial.url/fooba
</code></pre>
  
  <p>
    你可以按 <kbd><Esc></kbd> 退出命令行。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-8">保存配置</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-8" href="#i-8"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    一旦你根据自己意愿配置好选项、映射与命令，你可能希望下次打开 Vimperator 时它们仍然可用。延续 Vim 的风格，这可以通过保存 Vimperatorrc 配置文件达到目的。
  </p>
  
  <p>
    要保存你当下的设置并允许它们在下次打开 Vimperator 时自动加载，执行 <code>:mkv[imperatorrc]</code> 命令。
  </p>
  
  <p>
    这会在 $HOME 文件夹下生成 .vimperatorrc 文件，里面包含了你的设置。它只是个简单的文本文件，就像 vimrc 文件，你可以随意编辑来满足你的偏好。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-9">退出</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-9" href="#i-9"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Vimperator 支持 Vim 所有的经典退出方式。
  </p>
  
  <ul>
    <li>
      <code>:xall</code>&#8212;退出并为下次保存当前会话，默认行为。
    </li>
    <li>
      <code>:qall</code>&#8212;退出，不保存会话。
    </li>
    <li>
      <kbd>ZZ</kbd> &#8211; 普通模式下 <code>:xall</code> 的映射键值。
    </li>
    <li>
      <kbd>ZQ</kbd> &#8211; 普通模式下 <code>:qall</code> 的映射键值。
    </li>
  </ul>
  
  <h2 class="storycontent-h2">
    <span id="Firefox">Firefox 哪儿去了</span><a title="标题链接地址" class="u-floatRight hidden" id="heyFirefox" href="#Firefox"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    你现在可能相当茫然。请不要担心，这仍然是在 Firefox 下。以下是 Vimperator 提供的一些办法，它们允许 Firefox 继续抛头露面。
  </p>
  
  <ul>
    <li>
      <code>:dialog</code>&#8212;要访问 Firefox 的众多对话框窗口，你可以使用 <code>:dialog</code> 命令。
    </li>
    <li>
      <code>:bmarks</code>&#8212;Vimperator 提供了一个全新的书签界面，但它们从根子说仍然是 Firefox 的标准标签。<code>:bmark</code> 添加新书签，<code>:bmarks</code> 列出所有书签。
    </li>
    <li>
      <code>:history</code>&#8212;这个命令列出一整个彩色的可滚动、可点击的 Vimperator 的历史浏览列表。
    </li>
    <li>
      <code>:emenu</code>&#8212;通过命令行访问 Firefox 菜单。
    </li>
  </ul>
  
  <p>
    现在请随意练习。假如你使用 <code>:tabopen</code> 命令，记得使用映射 <kbd>gt</kbd>、<kbd>gT</kbd> 返回。如果使用 <code>:open</code> 命令，使用后退键击（如<kbd>H</kbd>）退回。假如你绝望地发现自己不知所在，请键入 <code>:help</code> 然后点击教程链接返回。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-10">把我弄出去</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-10" href="#i-10"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    或者你试过了，然后决定删除它。
  </p>
  
  <p>
    Vimperator 风格的方法是使用命令 <code>:addons</code>。键入命令打开 Firefox 附加组件窗口，然后你可以如平常的卸载方式选中 vimperator 然后卸载。
  </p>
  
  <p>
    当然，你也可以通过旧式方法，键入 <code>:set toolbars=menu</code> 显示菜单栏，然后从工具菜单中选择附加组件。
  </p><div class=timeline> 
  
  <h2 class="storycontent-h2">
    <span id="i-11">修订历史</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-11" href="#i-11"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <span itemprop='dateModified'>2015-06-12</span>：更新过时的信息
    </li>
  </ol>
</div></div>