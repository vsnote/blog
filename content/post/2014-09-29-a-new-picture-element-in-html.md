---
title: Picture 元素的故事
author: 陈 三
layout: post
date: 2014-09-29T12:44:02+00:00
url: /a-new-picture-element-in-html.html
views:
  - 1476
categories:
  - 前端开发
tags:
  - html

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_Web"><span class="toc_number toc_depth_1">1</span> 响应式 Web 设计</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#Picture"><span class="toc_number toc_depth_1">2</span> Picture 元素的引入</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">3</span> 理想很丰满，现实如何</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">4</span> 未来</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    <em>前阵子，我看了 arstechnica 的一篇 <a href="http://arstechnica.com/information-technology/2014/09/how-a-new-html-element-will-make-the-web-faster/">picture 元素的文章</a>。这是一篇讲英雄故事的文章，几个英雄人物在紧要时刻出现，最终促成 picture 元素诞生、成长。我觉得故事很有意思，就想译成中文，然后贴到博客。当时，我的打算是，先翻译完，然后联系他们，请求授权让我贴出译文。等我翻译完，请求的邮件发出去，过了两三天，得到的回复是：抱歉，没办法。我有些失望，但也无可奈何。只是心里琢磨着，找个时间，踩着 arstechnica 的肩膀，自己整理一篇 &#8211; 这样说的话，好像有抄袭嫌疑，但我尽力避免。</em>
  </p>
  
  <p>
    Web 历史里，有很长一段时间，我们所谓的网站，就是给桌面浏览器准备的。但移动互联网兴起后，所有的网站都傻眼了。因为用户要在移动设备上浏览网站，只能不停地放大、<strong>移动</strong>页面，根本没有什么体验可言。
  </p>
  
  <p>
    针对新出现的移动设备，当时盛行的解决办法是，让服务器检查用户代理（user agent），如果确认请求来自移动设备，就重定向到一个类似 m.domain.com 的移动专用网址上。但这样的话，开发者经常就需要维护两个、甚至两个以上站点。另外，重定向还经常出现失败的情况，比如用户访问某一具体的页面，结果却被重定向到移动端站点的首页。
  </p>
  
  <p>
    好在这 m.domain.com 的做法没有大范围铺开。一个更好的解决办法马上要来了。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Web">响应式 Web 设计</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Web" href="#_Web"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    2010 年，Web 开发人员 Ethan Marcotte 写了篇文章，聊些他称为<a href="http://alistapart.com/article/responsive-web-design">响应式 Web 设计</a>的东西。
  </p>
  
  <p>
    Ethan 说，新设备不断涌现，我们不能一直被动，如果要给每一种新设备都开发一个专用站点，那么，某种程度上，这是个零和游戏。
  </p>
  
  <p>
    他建议拥抱 Web 天生的灵活性，让<a href="(http://d.alistapart.com/responsive-web-design/ex/ex-site-FINAL.html)">页面</a>基于设备特征自动适应。
  </p>
  
  <p>
    这样，在 Ethan Marcotte 的推动，响应式设计开始正式进入舞台。
  </p>
  
  <p>
    响应式 Web 设计在一开始，只有少数开发者用来开发个人站点，真正使之走上正轨，是在 <a href="http://filamentgroup.com/lab/introducing-the-new-responsive-designed-bostonglobecom.html">Marcotte 和 Filament Group、Upstatement</a> 的开发者重新设计<a href="http://www.bostonglobe.com/">波士顿全球报站点</a>，使之自适应以后。全球报站点在 2011 年 9 月的全新设计表明，响应式设计不是只能小打小闹，被开发者拿来自娱自乐的东西，它是拥抱未来的真正道路。
  </p>
  
  <p>
    <img src="http://filamentgroup.com/images/bostonglobe-feat-promo.jpg" alt="波士顿全球报在电脑、平板、手机上的全貌" />
  </p>
  
  <p>
    <em>波士顿全球报在电脑、平板、手机上的全貌（<a href="http://filamentgroup.com/lab/introducing-the-new-responsive-designed-bostonglobecom.html">图片来源</a>）</em>
  </p>
  
  <p>
    站在用户角度看，全球站的重新设计是成功的，但背后，Macotte 他们却碰上一些问题，特别是图像一块。Marcotte 最初的文章里，使用 CSS 对图片做缩放处理。这使得图片能自动适应屏幕大小，不破坏内容布局，但同时也意味着，移动设备经常要加载不必要的、多余的像素。
  </p>
  
  <p>
    哪怕是今天，你在移动设备上浏览的许多网站还是这样的情况。开发者们知道这是个问题。但问题远没有第一眼看上去那么简单。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="Picture">Picture 元素的引入</span><a title="标题链接地址" class="u-floatRight hidden" id="heyPicture" href="#Picture"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Picture 元素的故事源于波士顿全球报的重构者们，这其中包括 Mat Marquis。
  </p>
  
  <p>
    一开始，Mat 和其他开发人员想出解决图片问题的办法<fnref target="13804.1" />是，在页面 img 标记中使用移动端的图片，JavaScript 加载到客户端后，马上检测屏幕大小并写入 cookie，如果屏幕尺寸大于约定的 480px，则在 HTML head 中插入一个 <code>base</code> 元素，将页面所有静态资源引用包括 JavaScript、CSS 以及图片等重定向到服务器上一个虚构的目录。服务器检查 cookie 里的屏幕尺寸，配合 .htaccess 规则给所有需要置换的移动端图片返回一个 1 像素大小的占位 gif 图片。接着，在页面加载完成后，JavaScript 移除 <code>base</code> 代码，并将移动端图片置换成大图。
  </p>
  
  <p>
    但这里还有一个问题，就是在大屏幕设备上，用户需要加载两次图片：一次是 1 像素大小的占位 gif，一次是置换过的大图。
  </p>
  
  <p>
    不管怎么说，当时的条件下，这可能是他们所能想到的最好解决办法。
  </p>
  
  <p>
    只不过，大约在波士顿全球报上线前一个月左右时间，几大新式浏览器推出它们的「图片预加载」功能。这个功能允许浏览器在解读 HTML 过程中提前加载页面上的图片，而不管图片的位置及大小。
  </p>
  
  <p>
    这个功能的推出，让 Mat 他们的办法报废，一来重定向失效，用户可能在置换图片前看到移动端图片，而不是 1 像素大小的占位 gif；二来使用 JavaScript 置换图片，是在反抗浏览器的「图片预加载」功能。
  </p>
  
  <p>
    这样，绕了一圈，Mat 他们又回到最初的问题上。
  </p>
  
  <p>
    最后，波士顿全球报在上线时，也没能解决这个问题，用户在移动设备浏览的话，还是会下载大图片。
  </p>
  
  <p>
    当然，事情并没有结束。关于响应式图片的讨论仍在进行。
  </p>
  
  <p>
    Mat 他们后来意识到，要解决这个问题，必须进入<strong>标记语言</strong>层面。他们开始在 WHATWG 邮件列表上讨论。但<a href="http://lists.w3.org/Archives/Public/public-whatwg-archive/2012Feb/0194.html">有人建议</a>他们移师社区小组(Community Group)里讨论。于是 2012 年 2 月，参加讨论的人员在 Mat Marquis 主导下，成立<a href="http://www.w3.org/community/respimg/">响应式图片社区小组</a>，3 月的时候，他们大致<a href="http://www.w3.org/community/respimg/2012/03/07/14/">拟定 <code>picture</code> 元素</a>：
  </p>
  
  <pre><code>&lt;picture alt="Alt tag should accurately describe the image represented by all sources, though cropping and zooming may differ."&gt;
  &lt;source src="mobile.jpg" /&gt; &lt;!-- Matches by default. --&gt;
  &lt;source src="high-res.jpg" media="min-width: 800px" /&gt; &lt;!-- Overrides the previous source over 800px before any assets are fetched, resulting in a single request. --&gt;
  &lt;img src="mobile.jpg" /&gt; &lt;!-- Fallback content, in the event the &lt;picture&gt; tag is completely unsupported by the user’s browser. --&gt;
&lt;/picture&gt;
</code></pre>
  
  <p>
    这个新元素的语法参考了 <code>video</code> 元素，是对 <code>img</code> 标签的一层封装，假如浏览器不支持它，则会回落到 img，不会给旧浏览器造成问题。而支持 picture 的浏览器可以根据规则，自动选择一张最合适的图片。最重要的，浏览器的「图片预加载」功能对其一样适用。
  </p>
  
  <p>
    与此同时，他们也了解到，早在 2007 年，同样的元素就有出现在 W3C 的公开邮件列表中，之后类似的主题也多次在 WHATWG 跟 W3C 的讨论列表中出现，只是每次都没有结果。
  </p>
  
  <p>
    那么这一次，随着响应式 web 设计的兴起，是否会有不一样的结果呢？
  </p>
  
  <p>
    2012 年 <a href="http://www.w3.org/community/respimg/2012/05/11/respimg-proposal/">5 月 11 号</a>，Mat 发现一个苹果员工于 5 月 10 号提交一份使用 img 标签 <code>set</code> 属性的响应式图片<a href="http://lists.w3.org/Archives/Public/public-whatwg-archive/2012May/0138.html">语法</a>到 WHATWG，这份语法只是解决 RICG 罗列的所有用例中的几个；更进一步，Mat 发现大部分 WHATWG 成员对 RICG 以及他们讨论的 picture 元素基本<a href="http://krijnhoetmer.nl/irc-logs/whatwg/20120510#l-747">一无所知</a> &#8211; 社区小组与 HTML 工作小组的联系根本不是 Mat 他们想像的那种关系。Mat 把这件事发到社区小组内讨论，但紧接着，在 5 月 15 号，Ian Hickson <a href="http://lists.w3.org/Archives/Public/public-whatwg-archive/2012May/0247.html">宣布</a>将 <code>set</code> 加入标准草案。RICG 社区一片哗然，Twitter 上讨论纷纷。
  </p>
  
  <p>
    一边是 WHATWG 声称浏览器厂商更支持 <code>set</code>，一边是开发者社区强烈支持 <code>picture</code>。
  </p>
  
  <p>
    甚至后来，HTML 的另一个工作小组 W3C 都出来掺一脚：
  </p>
  
  <blockquote class="twitter-tweet" lang="en">
    <p>
      <a href="https://twitter.com/scottjehl">@scottjehl</a> <a href="https://twitter.com/eddiemachado">@eddiemachado</a> <a href="https://twitter.com/hashtag/tkadlec?src=hash">#tkadlec</a> we are looking at this situation&#8230;please stay tuned (in meetings this week)
    </p>&mdash; W3C (@w3c) 
    
    <a href="https://twitter.com/w3c/status/202379977944084481">May 15, 2012</a>
  </blockquote>
  
  <p>
    好在双方后来开始妥协，愿意彼此合作。
  </p>
  
  <p>
    最终，修订过的 Picture 元素被纳入 HTML 标准，Web 羸了。大家都很高兴。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">理想很丰满，现实如何</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    picture 诚然是被纳入标准了，但如果浏览器厂商没有实现它，那 picture 也只是个美好的愿望。
  </p>
  
  <p>
    虽然 Firefox、Chrome 都表示愿意在未来实现 picture，但对二者来说，要优先考虑 Picture 的话，那可能还得几年。
  </p>
  
  <p>
    介绍下 Yoav Weiss。Yoav 是个跨越 Web 开发与浏览器开发两个世界的人。一方面，他是 RICG 参与者，熟悉响应式图片的问题及解决办法，另一方面，他还是 Blink & Webkit 的贡献者。
  </p>
  
  <p>
    在和 Blink 团队沟通过后，Yoav 开始着手相关的基础架构。起初他是在业余时间里做这件事，但他的业余时间实在不多，于是考虑转为全职做这件事。Mat Marquis 他们发起了一个<a href="https://www.indiegogo.com/projects/picture-element-implementation-in-blink#home">众筹活动</a>。出人意料的是，活动不仅成功达到目标，还远远超过目标。这样 Yoav 就有足够的精力在 Blink 上实现 picture 元素，并且把它移植到 Webkit，使得基于 Webkit 的浏览器也能使用 picture 元素。与此同时，RICG 的另一个贡献者 Caceres 开始在 Mozilla 工作，帮助推动 Firefox <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=870022">实现 Picture</a>。
  </p>
  
  <p>
    截止今天，Picture 元素已经在 Chrome 38 以上版本实现并推出，Firefox 33 版本后可以通过 flag 开启，IE 也在考虑支持，Webkit 则也已经实现 picture 规范的子集 srcset。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">未来</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    这是一个 Web 开发者们共同努力，让 Web 变得更加美好的故事。整个过程看起来有点像烂俗肥皂剧，但不得不承认，我们的 Web 就是这么来的。只是这一次，RICG 的努力，为我们打开一个全新的局面，那就是，Web 开发者可以、也应该努力参与 Web 标准的制定过程，因为他们自己更知道自己需要什么。
  </p>
  
  <footnotes>
    <fn name="13804.1">
      <p>
        <a href="http://alistapart.com/article/responsive-images-how-they-almost-worked-and-what-we-need">Responsive Images: How they Almost Worked and What We Need · An A List Apart Article</a>
      </p>
    </fn>
  </footnotes>
</div>