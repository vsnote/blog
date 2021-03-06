---
title: 使用 Privoxy 屏蔽网页广告
author: 陈 三
layout: post
date: 2013-02-23T03:53:08+00:00
url: /block-webpage-ad-with-privoxy.html
views:
  - 3866
dsq_thread_id:
  - 1099970768
categories:
  - Firefox
tags:
  - Privoxy

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_Privoxy"><span class="toc_number toc_depth_1">1</span> 安装 Privoxy</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_Privoxy-2"><span class="toc_number toc_depth_1">2</span> 启动 Privoxy</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">3</span> 配置浏览器</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_Privoxy-3"><span class="toc_number toc_depth_1">4</span> 测试 Privoxy</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">5</span> 屏蔽图片广告</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-3"><span class="toc_number toc_depth_1">6</span> 屏蔽文字广告</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_gif"><span class="toc_number toc_depth_1">7</span> 定住 gif 动画</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-4"><span class="toc_number toc_depth_1">8</span> 补充</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-5"><span class="toc_number toc_depth_1">9</span> 更新</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    很多浏览器扩展可以屏蔽网页广告，比如 <a href="https://addons.mozilla.org/en-US/firefox/addon/adblock-plus/">Firefox 下的 Adblock Plus</a>，Google Chrome 下同样有 <a href="https://chrome.google.com/webstore/detail/adblock-plus/cfhdojbkjhnklbpkdaibdccddilifddb?hl=en">Adblock Plus</a>；在 Firefox 下，甚至可以通过 <a href="https://addons.mozilla.org/en-US/firefox/addon/greasemonkey/">GreaseMonkey</a> 或 <a href="https://addons.mozilla.org/en-US/firefox/addon/scriptish/">Scriptish</a> 来编写 JavaScript 脚本移除广告。
  </p>
  
  <p>
    如果只使用一个浏览器，则装插件来屏蔽广告可能没什么问题，而且即装即用，省事。但如果用多个浏览器，每个浏览器都得装一遍就非常麻烦。
  </p>
  
  <p>
    <a href="http://www.privoxy.org/">Privoxy</a> 可以解决这种问题。
  </p>
  
  <p>
    在我们的电脑上，它扮演的是中间<strong>代理服务器</strong>的角色。浏览器通过它向远程服务器发出请求，远程服务器返回文件后经过 Privoxy 过滤后再发送回浏览器。
  </p>
  
  <p>
    因为它的网站上文档太<strong>不入门</strong>了，所以写一篇介绍下<strong>怎么使用 Privoxy</strong>。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Privoxy">安装 Privoxy</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Privoxy" href="#_Privoxy"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Privoxy 提供了多个平台的支持，比如 Windows、Linux、Macintosh 等。
  </p>
  
  <p>
    Ubuntu 下可以通过如下命令安装：
  </p>
  
  <pre><code>sudo apt-get install privoxy
</code></pre>
  
  <p>
    Mac OS 上可以通过 brew 安装：
  </p>
  
  <pre><code>brew install privoxy
</code></pre>
  
  <p>
    Windows 平台可以下载 <a href="http://sourceforge.net/projects/ijbswa/files/Win32/">EXE</a> 文件安装。
  </p>
  
  <p>
    更多系统下的安装方法参见 <a href="http://www.privoxy.org/user-manual/installation.html">Privoxy 网站说明</a>。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Privoxy-2">启动 Privoxy</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Privoxy-2" href="#_Privoxy-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    同样的，Privoxy 网站上提供有各平台<a href="http://www.privoxy.org/user-manual/startup.html">启动</a>的说明。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">配置浏览器</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Privoxy 服务器在电脑上的 ip 是 127.0.0.1，端口默认为 8118。根据需要，将个别浏览器或系统的 HTTP 与 HTTPS 代理服务器地址设置为 127.0.0.1,端口设置为 8118。
  </p>
  
  <p>
    <a href="http://www.privoxy.org/user-manual/startup.html">Privoxy 上</a>同样有配图说明。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Privoxy-3">测试 Privoxy</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Privoxy-3" href="#_Privoxy-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Privoxy 提供 <a href="http://p.p/">http://p.p/</a> 来测试它的运行是否在当前浏览器下正常。
  </p>
  
  <p>
    如果该页面头部显示诸如：
  </p>
  
  <blockquote>
    <p>
      This is Privoxy 3.0.19 on localhost (127.0.0.1), port 8118, enabled&#8221;
    </p>
  </blockquote>
  
  <p>
    则说明 Privoxy 已经在正常使用中。
  </p>
  
  <p>
    在 Privoxy 提供的默认配置文件下，如果仅是浏览英文站，则大部分广告已经可以对付掉。至于中文的，则需要自行调配配置文件了。
  </p>
  
  <p>
    Privoxy 提供多个<a href="http://www.privoxy.org/user-manual/configuration.html#CONFOVERVIEW">配置文件</a>，比如
  </p>
  
  <ul>
    <li>
      match-all.action
    </li>
    <li>
      default.action
    </li>
  </ul>
  
  <p>
    但不要去动这些配置文件，因为升级时这些文件会被覆盖，而 user.action、user.filter 这类文件在升级不会被覆盖，我们的规则就写在这些 user.* 的配置文件里。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">屏蔽图片广告</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    先来说怎样用 Privoxy 来屏蔽图片。
  </p>
  
  <p>
    <strong style='color:red;'>说明（ 2015.09.30）：</strong>因为我的博客迁移到 https，所以以下涉及图片 url 的规则不再有效，这是因为 Privoxy <a href="http://www.privoxy.org/faq/misc.html#AEN909">仅能处理 https 协议的 url 的 host 部分</a>。
  </p>
  
  <p>
    举个最简单的例子，打开 user.action 文件，在文件末加入以下内容：
  </p>
  
  <pre><code>{+block}
www.zfanw.com/blog/wp-content/uploads/2013/02/0-300x169.png
</code></pre>
  
  <p>
    这是最直白的方法，<code>+block</code> 指示 Privoxy 屏蔽随后的内容，这个内容由一个 <a href="http://www.privoxy.org/user-manual/actions-file.html#AF-PATTERNS">URL 规则</a> 指定，这个 URL 规则的格式为 <code>&lt;domain&gt;&lt;port&gt;/&lt;path&gt;</code>，三个值均为可选，另外需要注意，domain 部分不需要写 &#8220;http://&#8221;，因为 Privoxy 已经默认这个协议。
  </p>
  
  <p>
    保存 user.action 配置文件后强制刷新<a href="http://www.zfanw.com/blog/we-picture-together-when-young.html">页面</a>可以看到，图片已经被一个丑陋的 Pattern 替换掉。
  </p>
  
  <p>
    页面中被屏蔽的图片需要一个东西来替代，这个可以通过 <code>+set-image-blocker</code> 设置：
  </p>
  
  <pre><code>{+block +set-image-blocker{pattern}}
www.zfanw.com/blog/wp-content/uploads/2013/02/0-300x169.png
</code></pre>
  
  <p>
    其中 <code>pattern</code> 为该命令的默认参数值，即是你所见的丑陋的 Pattern；另两个取值分别是 &#8220;blank&#8221; 与「图片地址」。
  </p>
  
  <p>
    &#8220;blank&#8221; 使用一个 1&#215;1 像素的白色 gif 文件填充被屏蔽的图片位置。
  </p>
  
  <p>
    而第三个取值，即「图片地址」，可以是本地，也可以是网络上：
  </p>
  
  <pre><code>{+block +handle-as-image +set-image-blocker{http://farm9.staticflickr.com/8298/7976223037_941a1ed84f_z.jpg}}
www.zfanw.com/blog/wp-content/uploads/2013/02/0-300x169.png
</code></pre>
  
  <p>
    当在 user.action 文件中写入上面的命令并保存后，强制刷新页面，你看到的将是一朵茶花，而不是原来的几个男性图片。是的，Privoxy 用你指定的图片替换被屏蔽的广告图片。
  </p>
  
  <p>
    规则写好后，你可能想检查它是否生效，Privoxy 提供一个网页工具 <a href="http://config.privoxy.org/show-url-info">http://config.privoxy.org/show-url-info</a>，可以用来查看规则是否对某 URL 生效，借此我们可以检查规则是不是写对，是不是能达到我们的目的。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-3">屏蔽文字广告</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-3" href="#i-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    在屏蔽图片广告时，Privoxy 用到的是 action，动作，指示在匹配相应的 URL 时执行动作。屏蔽文字广告则有所不同，需要用到 <a href="http://www.privoxy.org/user-manual/filter-file.html">filter</a>，如果你接触过 WordPress 的代码，则相信对这个概念很了解。简单地理解，就是对相应的内容进行处理后再输出。
  </p>
  
  <p>
    同样的，我们将把规则写在 user.filter 文件中。
  </p>
  
  <p>
    先拿 Privoxy 上的示例做个说明：
  </p>
  
  <pre><code>FILTER: foo Replace all "foo" with "bar"
s/foo/bar/g
</code></pre>
  
  <p>
    <code>FILTER</code> 是 Privoxy 关键词，表示过滤文本，另外还有两个关键词，这里不做介绍。foo 是这个 filter 的名称，「Replace all &#8220;foo&#8221; with &#8220;bar&#8221;」则是描述。<code>s/foo/bar/g</code> 则是替换命令，如果熟悉 Vim 或 Sed 则应该对这个命令非常清楚。
  </p>
  
  <p>
    定义名称为 foo 的过滤器后，我们需要在 user.action 中调用它：
  </p>
  
  <pre><code>{+filter{foo}}
.privoxy.org/user-manual/filter-file.html
</code></pre>
  
  <p>
    强制刷新该页面后，就会看到，页面内的所有 foo 都被换成 bar 了。
  </p>
  
  <p>
    然后进入实战，如何屏蔽百度的广告 &#8211; 这里，需要 HTML/CSS 知识来找出广告部分的代码。比如百度搜索结果前的推广有个 class 为 <code>ec_pp_f</code>，右侧推广链接的 id 为 <code>content_right</code>。
  </p>
  
  <p>
    首先定义一个 filter:
  </p>
  
  <pre><code>FILTER: block-baidu 屏蔽百度广告
s|&lt;/head&gt;|&lt;style type="text/css"&gt;table.ec_pp_f,\#content_right,.ec_pp_f+br,[class~=EC_mr15]{display:none;}&lt;/style&gt;&lt;/head&gt;|
</code></pre>
  
  <p>
    注意 # 前的 \，因为在 user.filter 文件中 # 开头的行表示注释，所以需要转义。至于 s 命令后使用 | 而非 / 是因为 HTML 标签中带有 /，为避免加转义符号，就另外找个字符分隔，Privoxy 的 default.filter 文件中是使用 @ 符号来分隔的，我这里用 |。
  </p>
  
  <p>
    之后在 user.action 文件中调用该 filter:
  </p>
  
  <pre><code>{+filter{block-baidu}}
.baidu.com
</code></pre>
  
  <p>
    刷新页面后就可以看到，百度的推广广告已经屏蔽掉了。
  </p>
  
  <p>
    在写规则时，需要小心，因为 Privoxy 对配置文件非常敏感，一旦写错，就会退出，所以，如果发现代理不正常了，请重启 Privoxy。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_gif">定住 gif 动画</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_gif" href="#_gif"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    如果你对 gif 动画不耐烦，则 Privoxy 提供方法来「定」住它不动。在 user.action 文件中加入如下：
  </p>
  
  <pre><code>{+deanimate-gifs{last}}
.tumblr.com
</code></pre>
  
  <p>
    <code>last</code> 表示定在最后一帧，还有个 <code>first</code> 表示定在最前一帧。
  </p>
  
  <p>
    这样，tumblr.com 网站上的 gif 动画就不会闪瞎眼了。不过据我测试，还是有些漏网之鱼。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-4">补充</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-4" href="#i-4"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    补充中是我添加到 user.action 与 user.filter 文件的内容，以后可能会进行更新。仅作参考。
  </p>
  
  <ol>
    <li>
      <a href="https://gist.github.com/chenxsan/5004046">user.action gist 文件</a>
    </li>
    <li>
      <a href="https://gist.github.com/chenxsan/5004032">user.filter gist 文件</a>
    </li>
  </ol>
  
  <h2 class="storycontent-h2">
    <span id="i-5">更新</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-5" href="#i-5"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    因为 gist 的更新非常不便，就在 github 上创建了<a href="https://github.com/chenxsan/Privoxy">一个库</a>，专门用来存放这两个配置文件。
  </p>
</div>