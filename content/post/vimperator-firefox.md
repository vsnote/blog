---
title: Firefox 利器 – Vimperator
author: 陈 三
layout: post
date: 2011-03-16T15:33:30+00:00
url: /vimperator-firefox.html
Views:
  - 1
dsq_thread_id:
  - 458725519
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
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 打开常用网址</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 打开网页</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-3"><span class="toc_number toc_depth_1">3</span> 搜索</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-4"><span class="toc_number toc_depth_1">4</span> 浏览网页</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-5"><span class="toc_number toc_depth_1">5</span> 历史导航</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-6"><span class="toc_number toc_depth_1">6</span> 输入文字</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-7"><span class="toc_number toc_depth_1">7</span> 标签页管理</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-8"><span class="toc_number toc_depth_1">8</span> 保存配置</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_Firefox"><span class="toc_number toc_depth_1">9</span> 重启 Firefox</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_Firefox-2"><span class="toc_number toc_depth_1">10</span> 退出 Firefox</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-9"><span class="toc_number toc_depth_1">11</span> 修订历史</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    Vimperator 受启于 Vim，但这不代表，我们使用 Vimperator 前一定要会 Vim，大部分时候，Vimperator 只需简单的几个键，就可以完成绝大部分工作。
  </p>
  
  <ul>
    <li>
      命令部分均可按 <kbd>Tab</kbd> 键补齐。
    </li>
    <li>
      任何时候，想要放弃输入或退回普通模式，按 <kbd>Esc</kbd> 键。
    </li>
    <li>
      大写请配合 <kbd>shift</kbd> 键输入。
    </li>
    <li>
      普通模式下 <kbd>.</kbd> 可以重复上一个操作，比如使用 <kbd>d</kbd> 关闭当前页后，<kbd>.</kbd> 可继续关闭当前页。
    </li>
  </ul>
  
  <h2 class="storycontent-h2">
    <span id="i">打开常用网址</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    可以将常用网址添加为 quickmark，有两个办法：
  </p>
  
  <ol>
    <li>
      <p>
        添加当前网址
      </p>
      
      <p>
        假设当前页网址是 http://www.google.com，
      </p>
      
      <ol>
        <li>
          按 <kbd>shift+m</kbd> 键，可以看到底端命令栏出现大写的 <code>M</code>
        </li>
        <li>
          再按 a-z、A-Z、0-9 中的任一个，如 <kbd>g</kbd>，则命令行显示 <code>Added quick mark 'g':http://www.google.com</code> 表示成功添加 quickmark。
        </li>
      </ol>
      
      <p>
        此后可以使用 <kbd>gog</kbd> 在当前页打开 google，或 <kbd>gng</kbd> 在新标签页打开 google。
      </p>
    </li>
    
    <li>
      <p>
        添加多个网址
      </p>
      
      <ol>
        <li>
          <p>
            在命令行模式中执行
          </p>
          
          <p>
            <code>:qmark a www.google.com, www.zfanw.com, google Vimperator</code>
          </p>
        </li>
      </ol>
      
      <p>
        注意逗号后面是有个空格的。
      </p>
      
      <p>
        以后按 <kbd>goa</kbd> 或 <kbd>gna</kbd> 可以同时打开 google 首页、zfanw 首页，还会打开 google 搜索 vimperator。
      </p>
    </li>
  </ol>
  
  <p>
    <code>:qmarks</code>：显示所有已经添加的 quickmark
  </p>
  
  <p>
    <code>:delqmark g</code>：删除 g 这个 quickmark
  </p>
  
  <p>
    <code>:delqmark!</code>：删除所有 quickmark
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">打开网页</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    <kbd>o</kbd>：当前页打开
  </p>
  
  <p>
    <kbd>t</kbd>：新标签页中打开
  </p>
  
  <p>
    <kbd>w</kbd>：新窗口里打开
  </p>
  
  <p>
    <kbd>gh</kbd>：在当前页打开主页
  </p>
  
  <p>
    <kbd>gH</kbd>：在新标签页中打开主页
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-3">搜索</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-3" href="#i-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    <code>:dialog searchengines</code>：查看所有可用的搜索引擎，并可以进行排序、删除、更改关键字等，默认搜索引擎是 Google。
  </p>
  
  <p>
    <code>:google vimperator</code>：打开 google 搜索 vimperator
  </p>
  
  <p>
    <code>:wikipedia vimperator</code>：打开 wikipedia 中的 vimperator 条目
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-4">浏览网页</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-4" href="#i-4"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    <kbd>h</kbd>：左
  </p>
  
  <p>
    <kbd>l</kbd>：右
  </p>
  
  <p>
    <kbd>j</kbd>：下
  </p>
  
  <p>
    <kbd>k</kbd>：上
  </p>
  
  <p>
    <kbd>gg</kbd>：回到页首
  </p>
  
  <p>
    <kbd>G</kbd>：跳到页面底部
  </p>
  
  <p>
    <kbd>]]</kbd>：下一页
  </p>
  
  <p>
    <kbd>[[</kbd>：上一页
  </p>
  
  <p>
    <kbd>gf</kbd>：查看页面源文件，再次使用则切换回原页面
  </p>
  
  <p>
    <kbd>gu</kbd>：打开上一级页面，比如当前网址为 www.zfanw.com/blog，<kbd>gu</kbd> 打开 www.zfanw.com
  </p>
  
  <p>
    <kbd>zi</kbd>：放大页面字体
  </p>
  
  <p>
    <kbd>zo</kbd>：缩小页面字体
  </p>
  
  <p>
    <kbd>zz</kbd>：恢复页面默认字体
  </p>
  
  <p>
    Vimperator 提供 hints 模式，该模式下，页面内的所有可见链接被编号，按下编号即可打开链接，又或者输入链接内的文本，比如某链接文本是 shopping car，则可以直接键击 shopping car 打开链接，hints 有两个打开模式：
  </p>
  
  <ol>
    <li>
      <kbd>f</kbd>：在当前页打开链接
    </li>
    <li>
      <kbd>F</kbd>：在新标签页打开链接
    </li>
  </ol>
  
  <h2 class="storycontent-h2">
    <span id="i-5">历史导航</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-5" href="#i-5"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    当你在当前页中不断打开链接后，你可能想后退到前一个浏览页，又或者前进到后一个浏览页，就像在工具栏上单击前进、后退那样。
  </p>
  
  <p>
    在使用以下命令时，请注意 Vimperator 所处的模式，只有在普通模式（normal mode）里，下述命令才能起到预期作用。
  </p>
  
  <p>
    <kbd>ctrl-o</kbd>：后退
  </p>
  
  <p>
    <kbd>ctrl-i</kbd>：前进
  </p>
  
  <p>
    <kbd>H</kbd>：后退，与普通模式下 <kbd>ctrl-o</kbd> 作用相同
  </p>
  
  <p>
    <kbd>L</kbd>：前进，与普通模式下 <kbd>ctrl-i</kbd> 作用相同
  </p>
  
  <p>
    <code>:[count]back[!]</code>：后退，<code>:3back</code> 表示后退 3 次，<code>:back!</code> 表示后退到最早一个历史页
  </p>
  
  <p>
    <code>:[count]forward</code>：前进，<code>:3forward</code> 表示前进 3 次，<code>:forward!</code> 表示前进到最后一个历史页
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-6">输入文字</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-6" href="#i-6"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    如果页面内有文本输入的地方，则 <kbd>gi</kbd> 命令可快速定位，使其处于插入模式。
  </p>
  
  <p>
    若页面内有多个可输入文字的地方，如一个注册用户的页面，有用户名、邮箱、密码、确认密码四个，则 <kbd>1gi</kbd> 定位到用户名框，<kbd>2gi</kbd> 定位到邮箱框。
  </p>
  
  <p>
    有时<kbd>gi</kbd>命令不行，则可以用 hints 模式来定位输入框。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-7">标签页管理</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-7" href="#i-7"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    <kbd>ctrl-p</kbd>：前一个标签页（p 指 previous）
  </p>
  
  <p>
    <kbd>ctrl-n</kbd>：后一个标签页（n 指 next）
  </p>
  
  <p>
    <kbd>gt</kbd>：后一个标签页，与 ctrl-n 命令同
  </p>
  
  <p>
    <kbd>gT</kbd>：前一个标签页，与 ctrl-p 命令同
  </p>
  
  <p>
    <kbd>g0</kbd>、<kbd>g^</kbd>：第一个标签页（0为数字而非字母）
  </p>
  
  <p>
    <kbd>g$</kbd>：最后一个标签页
  </p>
  
  <p>
    <kbd>d</kbd>：关闭当前标签页，将右侧一个标签页激活为当前
  </p>
  
  <p>
    <kbd>D</kbd>：关闭当前标签页，将左侧一个标签页激活为当前
  </p>
  
  <p>
    <code>:tabonly</code>：关闭除当前标签页外的所有标签页
  </p>
  
  <p>
    <kbd>u</kbd>：如果你想恢复刚关闭的标签页，则可以按 u 来恢复，按多次 u 的话则可以依次恢复
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-8">保存配置</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-8" href="#i-8"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    假如你自定义 Vimperator 选项或键映射，希望下回仍然生效，
  </p>
  
  <pre><code>:mkvimperatorrc&lt;/code&gt;[!]
</code></pre>
  
  <p>
    命令保存设置到 vimperatorrc 配置文件。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Firefox">重启 Firefox</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Firefox" href="#_Firefox"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    <code>:restart</code>：Vimperator 的该命令可以重启 Firefox。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Firefox-2">退出 Firefox</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Firefox-2" href="#_Firefox-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Vimperator 提供了多种退出方式。
  </p>
  
  <table>
    <tr>
      <th>
        命令
      </th>
      
      <th>
        作用
      </th>
    </tr>
    
    <tr>
      <td>
        :quit
      </td>
      
      <td>
        关闭当前页
      </td>
    </tr>
    
    <tr>
      <td>
        :quitall
      </td>
      
      <td>
        关闭所有页，不保存会话
      </td>
    </tr>
    
    <tr>
      <td>
        :winclose
      </td>
      
      <td>
        关闭窗口
      </td>
    </tr>
    
    <tr>
      <td>
        :winonly
      </td>
      
      <td>
        关闭当前窗口外的所有窗口
      </td>
    </tr>
    
    <tr>
      <td>
        :xall
      </td>
      
      <td>
        关闭所有，保存会话
      </td>
    </tr>
    
    <tr>
      <td>
        :wall
      </td>
      
      <td>
        关闭所有，保存会话
      </td>
    </tr>
  </table>
  
  <p>
    <kbd>ZQ</kbd>：退出所有，会话不保存，与 :quitall 命令作用相同
  </p>
  
  <p>
    <kbd>ZZ</kbd>：退出所有，保存当前会话，与 :xall 命令作用相同
  </p>
  
  <div class='timeline'>
    <h2 class="storycontent-h2">
      <span id="i-9">修订历史</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-9" href="#i-9"><span class="" aria-hidden="true">#</span></a>
    </h2>
    
    <ol>
      <li>
        <span itemprop='dateModified'>2015-06-29</span>：重新整理
      </li>
    </ol>
  </div>
</div>