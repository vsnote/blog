---
title: Zed编辑器
author: 陈 三
layout: post
date: 2014-05-03T05:53:56+00:00
url: /editor-zed-app.html
views:
  - 1535
categories:
  - 未分类
tags:
  - Zed
  - 编辑器

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#Zed"><span class="toc_number toc_depth_1">1</span> Zed的界面</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#Zed-2"><span class="toc_number toc_depth_1">2</span> Zed支持的平台</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">3</span> 初次见面</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">4</span> 主题样式</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#Zed-3"><span class="toc_number toc_depth_1">5</span> 配置Zed</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-3"><span class="toc_number toc_depth_1">6</span> 文件操作</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-4"><span class="toc_number toc_depth_1">7</span> 命令</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-5"><span class="toc_number toc_depth_1">8</span> 多游标</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-6"><span class="toc_number toc_depth_1">9</span> 多面板</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-7"><span class="toc_number toc_depth_1">10</span> 自动更新</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    我用Vim<fnref target="12411.1" />，但不是Vim狂热分子。看到有人说Sublime Text<fnref target="12411.3" />不错，我会下载一个试试 &#8211; 确实有过人之处。LightTable<fnref target="12411.4" />说自己是下一代代码编辑器，我也会试试 &#8211; 十分新颖。Brackets<fnref target="12411.5" />专为Web开发打造，我是做前端开发的，听起来量身定制。Github十年磨一剑的姿态，出了Atom<fnref target="12411.6" />，号称为21世纪而造。可惜我没有Mac系统，否则也愿意试试。
  </p>
  
  <p>
    我个人对软件之名没有执念。
  </p>
  
  <p>
    Zed<fnref target="12411.7" />是我最近看到的一款编辑器，tagline写着「Rethinking Code Editing」。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="Zed">Zed的界面</span><a title="标题链接地址" class="u-floatRight hidden" id="heyZed" href="#Zed"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    看图(图片来自Zed网站)：
  </p>
  
  <p>
    <img src="http://zedapp.zed.netdna-cdn.com/wp-content/uploads/2014/02/zed-new.png" alt="Zed App" />
  </p>
  
  <p>
    看上去，这界面跟Sublime Text、Atom很像。
  </p>
  
  <p>
    但是，Zed的顶部没有菜单栏，也没有标签页，左侧也没有文件管理树。<strong>界面极简</strong>。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="Zed-2">Zed支持的平台</span><a title="标题链接地址" class="u-floatRight hidden" id="heyZed-2" href="#Zed-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Zed目前支持的平台有：
  </p>
  
  <ol>
    <li>
      Chrome浏览器 &#8211; Zed作为一个Chrome App存在
    </li>
    <li>
      Mac系统
    </li>
    <li>
      Windows系统
    </li>
    <li>
      Linux 32位系统
    </li>
    <li>
      Linux 64位系统
    </li>
  </ol>
  
  <p>
    安装过程非常简单，下载压缩包，解压即可使用。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">初次见面</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    初次打开Zed的界面如下：
  </p>
  
  <p>
    <img src="http://drp.io/files/5357c7274a734.png" alt="zed start" />
  </p>
  
  <p>
    这是Zed项目选择窗。
  </p>
  
  <p>
    如果你不曾打开过项目，则窗口中有三条菜单：
  </p>
  
  <ol>
    <li>
      Open Local Folder &#8211; 打开本地文件夹
    </li>
    <li>
      Configuration &#8211; 配置
    </li>
    <li>
      Manual &#8211; 手册
    </li>
  </ol>
  
  <p>
    如果你曾经开过项目，则Zed会把项目路径追加到Manual菜单下，通过移动箭头或鼠标点击选择项目。
  </p>
  
  <p>
    第一次打开项目文件夹，Zed会显示一个只读帮助文件，介绍一些快捷键的使用，比如：
  </p>
  
  <ul>
    <li>
      <kbd>ctrl-e</kbd> &#8211; 打开文件
    </li>
  </ul>
  
  <h2 class="storycontent-h2">
    <span id="i-2">主题样式</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Zed 默认的主题样式是暗黑色，但非常容易切换：
  </p>
  
  <ol>
    <li>
      <kbd>Ctrl-.</kbd> 调出顶部的命令栏(goto UI)
    </li>
    <li>
      输入<code>configurationthemexcode</code>，因为Zed支持命令模糊匹配，所以输入<code>themxo</code>也同样可以定位到命令。事实上，不管你输入什么，只要能唯一定位出命令，都是可以的
    </li>
    <li>
      按回车键，Zed界面的样式已经变成Xcode的
    </li>
  </ol>
  
  <p>
    但你可能好奇，样式更改是在哪里进行的？或说更改是怎么保存的？
  </p>
  
  <h2 class="storycontent-h2">
    <span id="Zed-3">配置Zed</span><a title="标题链接地址" class="u-floatRight hidden" id="heyZed-3" href="#Zed-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Zed有一个user.json文件，用于保存用户配置。譬如上面的主题样式更改，会自动保存到user.json文件中<code>preferences</code>属性里，如下：
  </p>
  
  <pre><code>{
    imports: [
        "/default.json"
    ],
    preferences: {
        theme: "xcode"
    },
    modes: {},
    keys: {},
    commands: {},
    handlers: {},
    themes: {},
    packages: [    ]
}
</code></pre>
  
  <p>
    user.json文件里，modes可以增加对文件格式的支持，keys可以增加按键组合或重新定义按键，commands可以定义新的命令。
  </p>
  
  <p>
    打开user.json文件要绕点路，你要在Zed项目选择窗里，选择<code>Configuration</code>菜单项，回车后会打开一个新Zed窗口，两栏，左侧显示README.md文件，右侧显示user.json文件。
  </p>
  
  <p>
    如果你正在编辑项目，突然想更改user.json，则可以先按<kbd>Ctrl-Shift-o</kbd>快速切换到Zed的项目选择窗 &#8211; 不过，你要保证项目选择窗口还开着。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-3">文件操作</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-3" href="#i-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <h3>
    打开文件
  </h3>
  
  <p>
    在你进入一个项目后，可以用<kbd>Ctrl-e</kbd>调出goto UI，然后输入要打开的文件名称。
  </p>
  
  <p>
    切换文件或新建文件，也同样使用<kbd>Ctrl-e</kbd>。因为认真的说，无论是切换文件还是新建文件，都是在打开一个文件 &#8211; 不管它存在或不存在。
  </p>
  
  <p>
    所以Zed把这几个文件操作方式合并。这是它的一个<strong>特性</strong>。Zed里，没有单独的<kbd>Ctrl-o</kbd>来打开对话框选择文件，也没有单独的<kbd>Ctrl-n</kbd>创建新文件 &#8211; 要创建文件，你只要输入一个不存在的文件名。
  </p>
  
  <h3>
    保存文件
  </h3>
  
  <p>
    在Zed中，打开A文件后，要打开B文件，因为只有一个窗口，所以B会替代A，占据当前窗口。在VIM中，如果A文件做修改，却还没有保存，会要求我们先保存A然后才能打开B。但Zed允许你直接打开B，不会有任何提示要求你先保存A。
  </p>
  
  <p>
    这是因为，它已经保存好了。默认情况下，没有键击，则2秒后Zed会自动保存文件。以下三种情况下，Zed也会<strong>自动保存</strong>文件：
  </p>
  
  <ol>
    <li>
      编辑器失去焦点
    </li>
    <li>
      切换文件
    </li>
    <li>
      关闭窗口
    </li>
  </ol>
  
  <p>
    但自动保存的功能可能会带来一些问题。
  </p>
  
  <p>
    譬如我用<code>gulp watch</code>命令监控coffeeScript文件的变化并自动编译，有时候用Zed打一半代码，又切换到其他窗口做点事情，再回来，因为自动保存好了，<code>gulp watch</code>捕捉到无法编译的问题，就自动退出，于是又得重开<code>gulp watch</code>命令。
  </p>
  
  <p>
    但Zed必须有自动保存的功能。如果没有，则我们切换文件时，Zed就要提醒我们：保存当前文件吗？又或者我们可以在新标签页中打开另一文件，但如上面所说，Zed没有标签页。
  </p>
  
  <p>
    当然，这种问题交给编辑器去解决，我觉得想法本身就有些问题，我们有<a href="hhttp://www.zfanw.com/blog/gulp-js-watch-error-handle.html">其他方法解决</a>。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-4">命令</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-4" href="#i-4"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Zed没有菜单栏，所以许多操作除了使用快捷键外，都需要通过命令完成。
  </p>
  
  <p>
    所有的命令都可以通过goto UI来调用。goto UI是Zed的一个命令入口，平时隐藏起来，但可以通过一些特殊按键唤出，比如<kbd>Ctrl-.</kbd>或<kbd>Ctrl-Shift-.</kbd>。
  </p>
  
  <p>
    当然，你也可以重新定义按键组合，比如在user.json中增加：
  </p>
  
  <pre><code>keys: {
        "Command:Enter Command": {
            win: "Ctrl-Shift-P"
        }
    }
</code></pre>
  
  <p>
    goto UI支持模糊匹配，所以我们不需要记住完整的命令，只大概知道几个单词或者字母就可以。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-5">多游标</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-5" href="#i-5"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    虽说它的功能跟查找/替换相近，但多游标似乎成了现下编辑器的标配。Sublime Text里有，Adobe Brackets在Sprint 38版本中也加入该功能，Zed同样提供多游标。
  </p>
  
  <p>
    首先，将光标置于要编辑的文本中(当然你也可以先选中文本)，然后，
  </p>
  
  <ol>
    <li>
      按<kbd>Ctrl-Alt-Right</kbd>，Zed会选中随后的同一文本；
    </li>
    <li>
      或者也可以按<kbd>Ctrl-Alt-Left</kbd>选择此前的同一文本；
    </li>
    <li>
      <kbd>Ctrl-Alt-F</kbd>则选中所有相同文本。
    </li>
  </ol>
  
  <p>
    在选择好多处文本后，按上、下、左、右方向键就可以移动多处光标的位置，也就可以同时编辑多处文本。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-6">多面板</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-6" href="#i-6"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    虽然Zed没有标签页功能，但它也提供了一个多面板功能。
  </p>
  
  <ol>
    <li>
      <kbd>Ctrl-2</kbd> &#8211; 将窗口分割为左右两个面板
    </li>
    <li>
      <kbd>Ctrl-3</kbd> &#8211; 将窗口分割为三个等宽面板
    </li>
    <li>
      <kbd>Ctrl-1</kbd> &#8211; 恢复原状
    </li>
    <li>
      <kbd>Ctrl-0</kbd> &#8211; 多面板间切换焦点
    </li>
  </ol>
  
  <p>
    如果你编辑的是Markdown文件或是CoffeeScript文件，按<kbd>Ctrl-p</kbd>可以在右侧面板实时预览编译效果，非常便利。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-7">自动更新</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-7" href="#i-7"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Zed的作者目前全职开发Zed，所以编辑器的更改会很频繁，不过Zed具备自动更新功能，所以不需要我们频繁跟踪进度。只需要在软件提醒更新时，重启Zed就好。
  </p>
  
  <footnotes>
    <fn name="12411.1">
      <p>
        <a href="http://www.vim.org/">welcome home : vim online</a>
      </p>
    </fn>
    
    <fn name="12411.3">
      <p>
        <a href="http://www.sublimetext.com/">Sublime Text: The text editor you&#8217;ll fall in love with</a>
      </p>
    </fn>
    
    <fn name="12411.4">
      <p>
        <a href="http://www.lighttable.com/">Light Table</a>
      </p>
    </fn>
    
    <fn name="12411.5">
      <p>
        <a href="http://brackets.io/">Brackets &#8211; The Free, Open Source Code Editor for the Web</a>
      </p>
    </fn>
    
    <fn name="12411.6">
      <p>
        <a href="https://atom.io/">Atom</a>
      </p>
    </fn>
    
    <fn name="12411.7">
      <p>
        <a href="http://zedapp.org/">Zed | Zed — Rethinking Code Editing</a>
      </p>
    </fn>
  </footnotes>
</div>