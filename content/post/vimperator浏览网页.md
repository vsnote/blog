---
title: Vimperator 浏览网页
author: 陈 三
layout: post
date: 2011-01-06T13:15:04+00:00
url: /vimperator浏览网页.html
isCJKLanguage: true
Views:
  - 1
dsq_thread_id:
  - 458747015
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
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 打开网页</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#countltC-xgt"><span class="toc_number toc_depth_1">2</span> [count]<C-x></a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#countltC-agt"><span class="toc_number toc_depth_1">3</span> [count]<C-a></a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">4</span> ~</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-3"><span class="toc_number toc_depth_1">5</span> 导航</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-4"><span class="toc_number toc_depth_1">6</span> 重新载入</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-5"><span class="toc_number toc_depth_1">7</span> 停止</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-6"><span class="toc_number toc_depth_1">8</span> 保存</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-7"><span class="toc_number toc_depth_1">9</span> 退出</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-8"><span class="toc_number toc_depth_1">10</span> 当前目录</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-9"><span class="toc_number toc_depth_1">11</span> 修订历史</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    Vimperator 为保证 Vim 用户流畅使用，几乎重写了所有 Firefox 击键。不过，某些情况下，你可能想把某个击键传给 Firefox，或者网页，则有两个办法：
  </p>
  
  <ol>
    <li>
      <p>
        <kbd>S-<Esc></kbd> 、<kbd><Insert></kbd>
      </p>
      
      <p>
        禁用 Vimperator 所有击键，包括 <kbd><Esc></kbd> 键，然后将击键传给下一个事件处理过程。在使用 JavaScript 驱动的表单（如 Gmail 的 RichEdit 表单域）时，又或一些 Google Reader 这样自带大量快捷键的 web app 时，这十分有用。要退出这个模式，再次按下 <kbd>S-<Esc></kbd>。
      </p>
    </li>
    
    <li>
      <p>
        <kbd>i</kbd>
      </p>
      
      <p>
        如果你只是需要传递某个击键给 javasciprt 表单又或其他扩展，请预先按下 <kbd>i</kbd>。如果要唤出被 Vimperator 隐藏的 Firefox 快捷键 <kbd><C-o></kbd>，这个方法同样适用。
      </p>
    </li>
  </ol>
  
  <h2 class="storycontent-h2">
    <span id="i">打开网页</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <h3>
    :o[pen] [arg1], [arg2], &#8230;
  </h3>
  
  <p>
    在当前标签页中打开一个或者多个 URL。多个 URL 可以用 URL 分隔符隔开（默认为“, ”，注意逗号后的一个空格是必需的）。第一个 URL 在当前标签页打开，其余的在新标签页打开。每个 token 按如下顺序解析：
  </p>
  
  <ol>
    <li>
      如果 token 是存在的相对或绝对文件名，则打开本地文件。 <ul>
        <li>
          <code>:open /etc/fstab</code> 打开系统表
        </li>
        <li>
          <code>:open ../other/foo.html</code> 打开你用户文件夹下的 /home/other/foo.html 文件
        </li>
      </ul>
    </li>
    
    <li>
      如果 token 看起来像搜索关键词且第一个单词是某个搜索引擎的名称，则打开该搜索引擎搜索并搜索关键词(<code>:open wikipedia linus torvalds</code> 打开维基百科中的 linus torvalds 词条。)搜索引擎的短名称由其名称猜测。假如你想自定义一名称，则可以从 <code>:dialog searchengines</code> 中更改。
    </li>
    <li>
      假如第一个单词并非搜索引擎，则打开默认搜索引擎搜索关键词（由 <code>'defsearch'</code> 选项确定）(<code>:open Linus torvalds</code> 打开 Google 搜索 linus torvalds)。
    </li>
    <li>
      其他情况下直接传递给 Firefox(<code>:open www.osnews.com,  www.slashdot.org</code> 在当前标签页打开 OSNews，在新标签页打开 Slashdot)。
    </li>
  </ol>
  
  <h3>
    :tabopen[!] [arg1],[arg2],&#8230;
  </h3>
  
  <p>
    和 <code>:open</code> 一样，不过是在新标签页打开第一个 URL。如果使用 [!]，则 tabopen 的 <code>'activate'</code> 选项的值被反转。
  </p>
  
  <h3>
    T
  </h3>
  
  <p>
    在浏览器底部显示 <code>:tabopen</code> 命令，并自动输入当前页 URL。如果你要基于当前页 URL 跳转其他网址，这十分好用。
  </p>
  
  <h3>
    :[count]tabdu[plicate][!]
  </h3>
  
  <p>
    复制当前标签页 [count] 次。tabopen 的 <code>'activate'</code> 值可以决定是否默认最后一个克隆标签页为活动页。当使用 [!] 时，tabopen 的值 <code>'activate'</code> 选项值被反转。
  </p>
  
  <h3>
    O
  </h3>
  
  <p>
    在浏览器底端显示 <code>:open</code> 命令，并自动输入当前页 URL。如果你要基于当前页 URL 再跳转其他网址，这十分有用。
  </p>
  
  <h3>
    :wino[pen] [!] [arg1],[arg2], &#8230;
  </h3>
  
  <p>
    同 <code>:tabopen</code> 命令相似，只不过是在新窗口中打开页面。
  </p>
  
  <h3>
    W
  </h3>
  
  <p>
    基于当前位置在新窗口打开一个或多个 URL。
  </p>
  
  <h3>
    p
  </h3>
  
  <p>
    基于当前 buffer 中剪贴板内容打开 URL。你也可以选择（对非 X11 用户来说是复制）一些非 URL 文本，<code>p</code> 命令会使用默认搜索引擎进行搜索。
  </p>
  
  <h3>
    P
  </h3>
  
  <p>
    类于 p，只是打开在新标签页。
  </p>
  
  <p>
    是否设置打开的新标签页为当前页取决于 <code>'activate'</code> 值。
  </p>
  
  <h3>
    gP
  </h3>
  
  <p>
    类于 P，只是反转了 &#8216;activate&#8217; 设置。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="countltC-xgt">[count]<C-x></span><a title="标题链接地址" class="u-floatRight hidden" id="heycountltC-xgt" href="#countltC-xgt"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    用于减小 url 中的最靠后一个数字值，默认减 1，也可以减去 [count] 值，负值不支持，因为这基本不怎么有用，所以数值最小只减到 0。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="countltC-agt">[count]<C-a></span><a title="标题链接地址" class="u-floatRight hidden" id="heycountltC-agt" href="#countltC-agt"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    用于增加 url 中的最靠后一个数字值，默认加 1，也可以加 [count] 值。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">~</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    打开用户 HOME 文件夹。其中你也可以使用 hints 模式，这也许会是地球上最快的文件浏览器。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-3">导航</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-3" href="#i-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <h3>
    :[count]ba[ck] [url]
  </h3>
  
  <p>
    在浏览器历史里后退 [count] 页，如果提供 [url]，则后退到第一个符合 url 值的页面。<code>:back!</code> 后退到浏览器历史最初页。
  </p>
  
  <h3>
    :[count]fo[rward] [url]
  </h3>
  
  <p>
    在浏览器历史里前进 [count] 页，如果提供 [url]，则前进到第一个符合 url 值的页面。<code>:forward!</code> 前进到浏览器历史最末页。
  </p>
  
  <h3>
    :ju[mps]
  </h3>
  
  <p>
    列出所有跳落点即标签页历史即会话历史。
  </p>
  
  <p>
    当前跳落位置用 > 标记。跳转序数决定 <code>:back</code> 与 <code>:forward</code> 的进退顺序。
  </p>
  
  <h3>
    gh
  </h3>
  
  <p>
    在当前标签页打开主页。
  </p>
  
  <h3>
    gH
  </h3>
  
  <p>
    在新标签页中打开主页。<code>'activate'</code> 值决定新标签页是否置为活动页面。
  </p>
  
  <h3>
    [count]gu
  </h3>
  
  <p>
    跃到 [count] 级父目录位置。
  </p>
  
  <p>
    在一个 url 上按 <kbd>gu</kbd> 会逐级提升 url。
  </p>
  
  <ul>
    <li>
      http://www.example.com/path/to/file.txt?query=value#anchor
    </li>
    <li>
      http://www.example.com/path/to/file.txt?query=value
    </li>
    <li>
      http://www.example.com/path/to/file.txt
    </li>
    <li>
      http://www.example.com/path/to/
    </li>
    <li>
      http://www.example.com/path/
    </li>
    <li>
      http://www.example.com/
    </li>
    <li>
      http://example.com/
    </li>
  </ul>
  
  <h3>
    gU
  </h3>
  
  <p>
    跳到网站的根目录。
  </p>
  
  <p>
    在 http://www.example.com/dir1/dir2/file.htm 地址上执行 <kbd>gU</kbd> 会打开 http://www.example.com/，在浏览本地文件夹时，则会跳到根文件夹。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-4">重新载入</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-4" href="#i-4"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <h3>
    r
  </h3>
  
  <p>
    强制重载当前页。
  </p>
  
  <h3>
    R
  </h3>
  
  <p>
    强制重载当前页，忽略本地缓存的内容。
  </p>
  
  <h3>
    :re[load] [!]
  </h3>
  
  <p>
    重载当前页，如果带 [!]，则跳过本地缓存内容。
  </p>
  
  <h3>
    :reloada[ll] [!]
  </h3>
  
  <p>
    强制重载所有页面，如果带 [!]，则跳过本地缓存内容。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-5">停止</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-5" href="#i-5"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <h3>
    <C-c>
  </h3>
  
  <p>
    停止加载当前网页。仅当没有选择任何文本时，若选择了文本，则命令拷贝文本到剪贴板。大部分时候这种情况不会出现，因为当页面尚在加载时，基本不会出现文本被选中的情形。
  </p>
  
  <h3>
    :st[op]
  </h3>
  
  <p>
    停止加载当前见面。
  </p>
  
  <h3>
    :stopa[ll]
  </h3>
  
  <p>
    停止加载所有网页。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-6">保存</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-6" href="#i-6"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <h3>
    :sav[eas] [!] [file]
  </h3>
  
  <p>
    保存当前页面到硬盘。若没有指定 [file] 参数，则保存为页面默认的文件名。末尾加 [!] 则覆盖已有文件。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-7">退出</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-7" href="#i-7"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <h3>
    :q[uit]
  </h3>
  
  <p>
    关闭当前标签页，如果这是窗口的最后一个标签页，则关闭窗口。如果这是最后一个窗口，则关闭 Vimperator。退出 Vimperator 时，会话不储存。
  </p>
  
  <h3>
    :quita[ll]
  </h3>
  
  <p>
    退出 Vimperator。无论有多少标签页、窗口打开着都关闭掉。会话不储存。
  </p>
  
  <h3>
    :winc[lose]
  </h3>
  
  <p>
    关闭窗口。
  </p>
  
  <h3>
    :winon[ly]
  </h3>
  
  <p>
    关闭除当前窗口外的所有其他窗口。
  </p>
  
  <h3>
    :wqa[ll]
  </h3>
  
  <p>
    不管开着多少标签页、窗口，都保存会话并退出。<code>:wq</code> 与 Vim 中的作用不同，Vim 中关闭一个标签页，Vimperator 则关闭窗口。
  </p>
  
  <h3>
    ZQ
  </h3>
  
  <p>
    退出，不保存会话。与 <code>:qall</code> 作用一样。
  </p>
  
  <h3>
    ZZ
  </h3>
  
  <p>
    退出 Vimperator，不管有多少标签页或窗口打开着，但会话会被保存，作用如 <code>:xall</code>。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-8">当前目录</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-8" href="#i-8"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <h3>
    :cd [-|path]
  </h3>
  
  <p>
    改变当前目录。<code>:cd -</code> 跳转到最后一次使用的目录。
  </p>
  
  <h3>
    :pw[d]
  </h3>
  
  <p>
    输出当前目录的名称。
  </p><div class=timeline> 
  
  <h2 class="storycontent-h2">
    <span id="i-9">修订历史</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-9" href="#i-9"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <span itemprop='dateModified'>2015-06-12</span>：调整内容
    </li>
  </ol>
</div></div>