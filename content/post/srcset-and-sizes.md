---
title: Srcset 和 sizes
author: 陈 三
layout: post
date: 2014-10-06T06:10:52+00:00
url: /srcset-and-sizes.html
enclosure:
  - |
    |
        http://ericportis.com/assets/2014-03-24-srcset-sizes/oops/oops-720.mp4
        343290
        video/mp4
        
  - |
    |
        http://ericportis.com/assets/2014-03-24-srcset-sizes/oops/oops-720.ogv
        460718
        video/ogg
        
views:
  - 2838
categories:
  - 前端开发
tags:
  - 响应式图片
  - 译文

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 第一部分：媒体查询有什么问题？</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#srcset_sizes"><span class="toc_number toc_depth_1">2</span> 第二部分：srcset + sizes = 太棒了！</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">3</span> 扩展阅读</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    <strong>译注</strong>：本文译自 <a href="http://ericportis.com/posts/2014/srcset-sizes/">Srcset and sizes</a>，原文使用 <a href="http://creativecommons.org/licenses/by/3.0/">CC BY 3.0</a> 许可。感谢作者额外提供一套灰色背景图片。
  </p>
  
  <p>
    <em>陈三的补充：如果你只是想了解 srcset 与 sizes，可以直接跳到第二部分，或扩展阅读的链接，第一部分作者只是在论证，在响应式图片里如果使用媒体查询会有什么样的困难。</em>
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">第一部分：媒体查询有什么问题？</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    且说你是在 <a href="http://1997.webhistory.org/www.lists/www-talk.1993q1/0182.html">1993.2.23</a> 到 <a href="http://alistapart.com/article/responsive-web-design/">2010.5.25</a> 期间制作网页。图片真是太简单了！无非就是：
  </p>
  
  <ul>
    <li>
      看看你的定宽布局
    </li>
    <li>
      量一量，要塞入你手上这张图片，究竟每个用户屏幕上固定需要多少个像素
    </li>
    <li>
      打开 Photoshop
    </li>
    <li>
      根据量好的尺寸保存图片
    </li>
    <li>
      在 <code>&lt;img&gt;</code> 标签中引用
    </li>
    <li>
      给自己倒一杯啤酒(或是打开一罐豌豆罐头)，庆祝任务完成
    </li>
  </ul>
  
  <p>
    <a href="https://www.zfanw.com/blog/wp-content/uploads/2014/10/measuring-hole.png" rel="attachment wp-att-13999"><img src="https://www.zfanw.com/blog/wp-content/uploads/2014/10/measuring-hole.png" alt="测量图片所占的空间大小" width="2118" class="alignnone size-full wp-image-13999" srcset="https://www.zfanw.com/blog/wp-content/uploads/2014/10/measuring-hole.png 2118w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/measuring-hole-300x202.png 300w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/measuring-hole-1024x690.png 1024w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/measuring-hole-100x67.png 100w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/measuring-hole-768x517.png 768w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/measuring-hole-520x350.png 520w" sizes="(max-width: 2118px) 100vw, 2118px" /></a>
  </p>
  
  <p>
    <a href="https://www.zfanw.com/blog/wp-content/uploads/2014/10/measuring-image.png" rel="attachment wp-att-13998"><img src="https://www.zfanw.com/blog/wp-content/uploads/2014/10/measuring-image.png" alt="计算图片大小" width="2448" class="alignnone size-full wp-image-13998" srcset="https://www.zfanw.com/blog/wp-content/uploads/2014/10/measuring-image.png 2448w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/measuring-image-300x203.png 300w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/measuring-image-1024x694.png 1024w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/measuring-image-100x67.png 100w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/measuring-image-768x520.png 768w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/measuring-image-520x352.png 520w" sizes="(max-width: 2448px) 100vw, 2448px" /></a>
  </p>
  
  <p>
    <a href="https://www.zfanw.com/blog/wp-content/uploads/2014/10/hammering.png" rel="attachment wp-att-14001"><img src="https://www.zfanw.com/blog/wp-content/uploads/2014/10/hammering.png" alt="把图片放入页面中" width="2232" class="alignnone size-full wp-image-14001" srcset="https://www.zfanw.com/blog/wp-content/uploads/2014/10/hammering.png 2232w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/hammering-300x200.png 300w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/hammering-1024x683.png 1024w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/hammering-100x66.png 100w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/hammering-768x512.png 768w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/hammering-520x346.png 520w" sizes="(max-width: 2232px) 100vw, 2232px" /></a>
  </p>
  
  <p>
    <a href="https://www.zfanw.com/blog/wp-content/uploads/2014/10/yay-peas.png" rel="attachment wp-att-13994"><img src="https://www.zfanw.com/blog/wp-content/uploads/2014/10/yay-peas.png" alt="完工吃豆子" width="1613" class="alignnone size-full wp-image-13994" srcset="https://www.zfanw.com/blog/wp-content/uploads/2014/10/yay-peas.png 1613w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/yay-peas-150x150.png 150w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/yay-peas-297x300.png 297w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/yay-peas-1014x1024.png 1014w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/yay-peas-100x100.png 100w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/yay-peas-768x775.png 768w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/yay-peas-520x524.png 520w" sizes="(max-width: 1613px) 100vw, 1613px" /></a>
  </p>
  
  <p>
    在偶尔会有一些先知从荒原里走出，吐露<a href="http://alistapart.com/article/dao/">真相</a>，指出这个方法与生俱来的问题以前，这个方法已经服侍普通的 Web 设计者们二十年了。
  </p>
  
  <p>
    只是，时代正在改变。
  </p>
  
  <p>
    四年前，Ethan Marcotte 发表了一篇<a href="http://alistapart.com/article/responsive-web-design/">文章</a>；13 天后，Steve Jobs 发布一台<a href="http://en.wikipedia.org/wiki/IPhone_4">手机</a>；突然之间，<a href="http://unstoppablerobotninja.com/entry/fluid-images">弹性</a>和/或<a href="http://en.wikipedia.org/wiki/Retina_Display">高清屏</a>图片就成形了。随后，各种<a href="https://www.google.com/search?q=site:lists.whatwg.org+responsive+images">咬牙切齿</a>。
  </p><video style='max-width: 100%;' controls="controls"> <source type=video/mp4 src=http://ericportis.com/assets/2014-03-24-srcset-sizes/oops/oops-720.mp4> <source type=video/ogg src=http://ericportis.com/assets/2014-03-24-srcset-sizes/oops/oops-720.ogv> 您的浏览器不支持 
  
  <code>video</code>，请下载后用播放器打开。 </video> 
  
  <p>
    碰上响应式图片，我们的第一直觉，是试试我们在响应式布局上用到的工具：媒体查询。
  </p>
  
  <p>
    <a href="https://www.zfanw.com/blog/wp-content/uploads/2014/10/media-queries.png" rel="attachment wp-att-13997"><img src="https://www.zfanw.com/blog/wp-content/uploads/2014/10/media-queries.png" alt="响应式图片与媒体查询" width="2221" class="alignnone size-full wp-image-13997" srcset="https://www.zfanw.com/blog/wp-content/uploads/2014/10/media-queries.png 2221w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/media-queries-300x199.png 300w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/media-queries-1024x682.png 1024w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/media-queries-100x66.png 100w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/media-queries-768x511.png 768w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/media-queries-520x346.png 520w" sizes="(max-width: 2221px) 100vw, 2221px" /></a>
  </p>
  
  <p>
    浏览器无法知道它尚未加载的网站的一切。但它们对自身的渲染环境却总是了解：视口的尺寸，用户屏幕的分辨率，等等。媒体查询的思路是这样的：让 web 开发者根据特定环境做特定的事情。如果视口宽于 1000 像素，那么侧边栏就显示在左边。否则，将它推到主栏下方。如果用户的屏幕是高清屏，那就使用一张大图，否则使用小图。
  </p>
  
  <p>
    太简单啦。
  </p>
  
  <p>
    <a href="https://www.zfanw.com/blog/wp-content/uploads/2014/10/easypeas.png" rel="attachment wp-att-14004"><img src="https://www.zfanw.com/blog/wp-content/uploads/2014/10/easypeas.png" alt="小意思" width="2258" class="alignnone size-full wp-image-14004" srcset="https://www.zfanw.com/blog/wp-content/uploads/2014/10/easypeas.png 2258w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/easypeas-300x199.png 300w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/easypeas-1024x682.png 1024w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/easypeas-100x66.png 100w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/easypeas-768x511.png 768w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/easypeas-520x346.png 520w" sizes="(max-width: 2258px) 100vw, 2258px" /></a>
  </p>
  
  <p>
    但不幸的是，响应式图片的情况里，使用媒体查询通常是非常<a href="http://www.xanthir.com/b4Su0">糟糕</a>的。
  </p>
  
  <p>
    <a href="https://www.zfanw.com/blog/wp-content/uploads/2014/10/gulp.png" rel="attachment wp-att-14002"><img src="https://www.zfanw.com/blog/wp-content/uploads/2014/10/gulp.png" alt="糟糕咬到牙了" width="2244" class="alignnone size-full wp-image-14002" srcset="https://www.zfanw.com/blog/wp-content/uploads/2014/10/gulp.png 2244w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/gulp-300x200.png 300w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/gulp-1024x682.png 1024w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/gulp-100x66.png 100w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/gulp-768x511.png 768w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/gulp-520x346.png 520w" sizes="(max-width: 2244px) 100vw, 2244px" /></a>
  </p>
  
  <p>
    这值得花些时间解释。基于媒体查询的响应式图片选择之所以糟糕，是因为大部分响应式设计者是基于一个变量（视口宽度）来决定如何改变页面布局的，而对于响应式图片，我们实际上需要关心三个变量：
  </p>
  
  <ul>
    <li>
      布局中图片的渲染尺寸（CSS 像素尺寸）
    </li>
    <li>
      像素密度
    </li>
    <li>
      我们手头可支配的不同尺寸的图片
    </li>
  </ul>
  
  <p>
    &#8230;这些被微妙地简缩成媒体查询。
  </p>
  
  <p>
    一旦我们知道这三种东西，那么解法就简单了。从给定的资源里，挑出一张最小的，但是尺寸又要比<code>渲染尺寸</code> * <code>像素密度</code> 大。
  </p>
  
  <p>
    但是，很不幸，要确定<code>渲染尺寸</code>是一件非常困难的事。Web 开发者没法知道它。弹性图片会伸缩；在响应式布局中，一张图片的<code>渲染尺寸</code>什么可能性都有。还有一点可能也让人吃惊，就是浏览器在加载图片时，也不知道<code>渲染尺寸</code> &#8211; <code>渲染尺寸</code>依赖于页面 CSS，通常浏览器是在页面开始加载图片后很久才分析 CSS 的。
  </p>
  
  <p>
    运气好的是（看起来如此），给我们的源文件附加媒体查询可以绕过这问题，只是要把<code>渲染尺寸</code>分成两个：
  </p>
  
  <ul>
    <li>
      视口尺寸
    </li>
    <li>
      相对于视口，图片大小将如何变化
    </li>
  </ul>
  
  <p>
    &#8230;当然，还需要作者在完成<del>一些</del>许多<del>简单</del>复杂的计算后指定视口尺寸与像素密度。
  </p>
  
  <p>
    怎样的计算呢？让我们看一个例子。
  </p>
  
  <p>
    <a href="https://www.zfanw.com/blog/wp-content/uploads/2014/10/study-up.png" rel="attachment wp-att-13995"><img src="https://www.zfanw.com/blog/wp-content/uploads/2014/10/study-up.png" alt="计算响应式图片规则" width="2244" class="alignnone size-full wp-image-13995" srcset="https://www.zfanw.com/blog/wp-content/uploads/2014/10/study-up.png 2244w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/study-up-300x200.png 300w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/study-up-1024x682.png 1024w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/study-up-100x66.png 100w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/study-up-768x511.png 768w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/study-up-520x346.png 520w" sizes="(max-width: 2244px) 100vw, 2244px" /></a>
  </p>
  
  <p>
    （请注意，虽说我会尽量简化，但这个例子存在的理由，只是想告诉你，亲爱的读者们，基于媒体查询的计算过程是繁杂且易出错的。如果你很快就确认了这一点，请跳到第二部分。）
  </p>
  
  <p>
    假定你有一张图片的三个版本：
  </p>
  
  <ul>
    <li>
      <code>large.jpg</code> (1024 x 768)
    </li>
    <li>
      <code>medium.jpg</code> (640 x 480)
    </li>
    <li>
      <code>small.jpg</code> (320 x 240)
    </li>
  </ul>
  
  <p>
    然后在弹性网格 &#8211; 一种开始只一列，大视口中切换成三列的网格，比如<a href="http://ericportis.com/assets/2014-03-24-srcset-sizes/wolves/">这样</a>，你想要挑选一张图片并加载它。
  </p>
  
  <p>
    你想要支持 1x 和 2x 的<code>设备像素比</code>。
  </p>
  
  <p>
    怎样构造媒体查询？让我们从上开始。
  </p>
  
  <p>
    <code>large.jpg</code> 只有在绝对必要 &#8211; <code>small.jpg</code> 和 <code>medium.jpg</code> 都太小的时候才加载。更确切说，我们只需要如下情况加载 <code>large.jpg</code>：
  </p>
  
  <pre><code>渲染尺寸 x 像素密度 &gt; 尺寸仅次于它的文件长度
</code></pre>
  
  <p>
    我们的示例布局里，<code>渲染尺寸</code>只是<code>视口尺寸</code>的一个简单百分比。因此：
  </p>
  
  <pre><code>渲染尺寸 = 图片相对视口的比例 x 视口尺寸
</code></pre>
  
  <p>
    <code>尺寸仅次于它的文件</code>是 <code>medium.jpg</code>，所以：
  </p>
  
  <pre><code>尺寸仅次于它的文件长度 = 640px
</code></pre>
  
  <p>
    汇合一下，则我们得到以下的不等式：
  </p>
  
  <pre><code>图片相对视口的比例 x
视口尺寸 x
像素密度
&gt; 640px
</code></pre>
  
  <p>
    重排一下：
  </p>
  
  <pre><code>视口尺寸 &gt;
  640px ÷
  (图片相对视口的比例 x 像素密度)
</code></pre>
  
  <p>
    要构建媒体查询，我们需要求解每个可能的<code>图片相对视口的比例</code>和<code>像素密度</code>值下的<code>视口尺寸</code>。
  </p>
  
  <p>
    <code>图片相对视口的比例</code>有两个可能取值：到达断点(36em)前的 100<a href="http://www.w3.org/TR/css3-values/#viewport-relative-lengths">vw</a>及到达断点后的 33.3vw。
  </p>
  
  <p>
    至于<code>像素密度</code>&#8230;呃，<a href="http://en.wikipedia.org/wiki/List_of_displays_by_pixel_density">取值可能无数</a>，不过我们前面已经说过，只要支持<code>设备像素比</code> 1x 和 2x。
  </p>
  
  <p>
    两种<code>图片相对视口的比例</code> x 两种<code>设备像素比</code> = 四种需要我们考虑的情形。且一个一个地来看。
  </p>
  
  <h3>
    1x，断点前
  </h3>
  
  <p>
    因为我们的断点是 36em，所以很明显地：
  </p>
  
  <pre><code>视口尺寸 &lt; 36em
</code></pre>
  
  <p>
    把<code>图片相对视口的比例</code> = 100vw 和<code>像素密度</code> = 1x 代入我们此前的不等式中：
  </p>
  
  <pre><code>视口尺寸 &gt;
  640px ÷ ( 100vw x 1x ) = 640px = 40em
</code></pre>
  
  <p>
    结合两个不等式，我们得到一个不可能的东西：
  </p>
  
  <pre><code>36em &gt; 视口尺寸 &gt; 40em
</code></pre>
  
  <p>
    所以我们可以不用考虑这种情况 &#8211; 即单列布局下，1x 的设备像素比不需要 <code>large.jpg</code>。
  </p>
  
  <h3>
    2x，断点前
  </h3>
  
  <p>
    再来：
  </p>
  
  <pre><code>视口尺寸 &lt; 36em
</code></pre>
  
  <p>
    但这回我们代入 2x：
  </p>
  
  <pre><code>视口尺寸 &gt;
  640px ÷ ( 100vw x 2x ) = 320px = 20em
</code></pre>
  
  <p>
    结合起来我们得到：
  </p>
  
  <pre><code>36em &gt; 视口尺寸 &gt; 20em
</code></pre>
  
  <p>
    于是视口尺寸在这个范围中时，2x 屏幕上我们要加载 <code>large.jpg</code>。
  </p>
  
  <h3>
    1x，断点后
  </h3>
  
  <p>
    现在我们要比断点宽了：
  </p>
  
  <pre><code>视口尺寸 &gt; 36em
</code></pre>
  
  <p>
    而且我们是在 1x 屏幕上的三列布局：
  </p>
  
  <pre><code>视口尺寸 &gt;
  640px ÷ ( 33.3vw × 1x ) = 1920px = 120em
</code></pre>
  
  <p>
    当视口大于 120em 时，它始终是大于 36em的，因此我们可以把 36em 丢掉不管。在 1x 屏幕上，我们要加载 <code>large.jpg</code>的条件：
  </p>
  
  <pre><code>视口尺寸 &gt; 120em
</code></pre>
  
  <p>
    Ok，最后一个。
  </p>
  
  <h3>
    2x，断点后
  </h3>
  
  <pre><code>视口尺寸 &gt; 36em
</code></pre>
  
  <p>
    &#8230;而且&#8230;
  </p>
  
  <pre><code>视口尺寸 &gt;
  640px ÷ ( 33.3vw × 2x ) = 960px = 60em
</code></pre>
  
  <p>
    &#8230;结论是，以下情况下在 2x 屏幕加载 <code>large.jpg</code>：
  </p>
  
  <pre><code>视口尺寸 &gt; 60em
</code></pre>
  
  <p>
    把所有的组合一起放入媒体查询：
  </p>
  
  <pre><code>( (min-device-pixel-ratio: 1.5) and (min-width: 20.001em) and (max-width: 35.999em) ) or
( (max-device-pixel-ratio: 1.5) and (min-width: 120.001em) ) or
( (min-device-pixel-ratio: 1.5) and (min-width: 60.001em) )
</code></pre>
  
  <p>
    <code>medium.jpg</code> 的计算过程就留给读者做练习。
  </p>
  
  <p>
    使用最初的 <code>&lt;picture&gt;</code> 提案来标记我们的图片，结果是：
  </p>
  
  <pre><code>&lt;picture&gt;

  &lt;source src="large.jpg"
          media="( (min-device-pixel-ratio: 1.5) and (min-width: 20.001em) and (max-width: 35.999em) ) or
                 ( (max-device-pixel-ratio: 1.5) and (min-width: 120.001em) ) or
                 ( (min-device-pixel-ratio: 1.5) and (min-width: 60.001em) )" /&gt;
  &lt;source src="medium.jpg"
          media="( (max-device-pixel-ratio: 1.5) and (min-width: 20.001em) and (max-width: 35.999em) ) or
                 ( (max-device-pixel-ratio: 1.5) and (min-width: 60.001em) ) or
                 ( (min-device-pixel-ratio: 1.5) and (min-width: 10.001em) )" /&gt;
  &lt;source src="small.jpg" /&gt;

  &lt;!-- fallback --&gt;
  &lt;img src="small.jpg" alt="A rad wolf" /&gt;

&lt;/picture&gt;
</code></pre>
  
  <p>
    让人头痛！
  </p>
  
  <p>
    另外，有一堆的标记不支持超过 2 的<code>设备像素比</code>，或是低于 1 的<code>设备像素比</code>，通常是不完美地支持这两者间的数值。如果我们要扩展<code>设备像素比</code>的支持，则要考虑的情景数量就会陡增。
  </p>
  
  <p>
    关于标记最糟糕的部分是，如果我们改变任何一个基础变量 &#8211; 源图片的尺寸，要支持的设备分辨率&#8230; 或者影响图片尺寸的布局的任一方面 &#8211; 我们需要重新做过所有的算术。
  </p>
  
  <p>
    <a href="https://www.zfanw.com/blog/wp-content/uploads/2014/10/barf.png" rel="attachment wp-att-14006"><img src="https://www.zfanw.com/blog/wp-content/uploads/2014/10/barf.png" alt="吐" width="2244" class="alignnone size-full wp-image-14006" srcset="https://www.zfanw.com/blog/wp-content/uploads/2014/10/barf.png 2244w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/barf-300x200.png 300w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/barf-1024x682.png 1024w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/barf-100x66.png 100w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/barf-768x511.png 768w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/barf-520x346.png 520w" sizes="(max-width: 2244px) 100vw, 2244px" /></a>
  </p>
  
  <p>
    快，还是早点跳到第二部分吧！
  </p>
  
  <h2 class="storycontent-h2">
    <span id="srcset_sizes">第二部分：<code>srcset</code> + <code>sizes</code> = 太棒了！</span><a title="标题链接地址" class="u-floatRight hidden" id="heysrcset_sizes" href="#srcset_sizes"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    那么，如果媒体查询不是正确的工具的话，现在怎么办？
  </p>
  
  <p>
    让我们先回到响应式图片的几个基本变量上，这一次，考虑下它们什么时候变，以及谁知道了什么。
  </p>
  
  <table>
    <tr>
      <th>
        变量
      </th>
      
      <th>
        作者在写代码时是否清楚？
      </th>
      
      <th>
        浏览器加载页面时是否清楚？
      </th>
    </tr>
    
    <tr>
      <td>
        视口尺寸
      </td>
      
      <td>
        no
      </td>
      
      <td>
        yes
      </td>
    </tr>
    
    <tr>
      <td>
        图片相对视口的比例
      </td>
      
      <td>
        yes
      </td>
      
      <td>
        no
      </td>
    </tr>
    
    <tr>
      <td>
        像素密度
      </td>
      
      <td>
        no
      </td>
      
      <td>
        yes
      </td>
    </tr>
    
    <tr>
      <td>
        源文件尺寸
      </td>
      
      <td>
        yes
      </td>
      
      <td>
        no
      </td>
    </tr>
  </table>
  
  <p>
    注意了！一列 yes 时，另一列总是 no：作者与浏览器所了解的不一样，它们是互补的。我们是钥匙主人，它们是看门人；把我们的力量结合起来，如此，如此。
  </p>
  
  <p>
    怎样联合起来？
  </p>
  
  <p>
    媒体查询就像一套紧急预案，“你看，”我们跟浏览器说，“我不清楚视口会有多大，但如果有这么大，那就用这个文件。如果还要大，用那个。如果屏幕是高清屏，那也用那个，但如果我切换到三列布局，那还是不要用那个&#8230;”我们是在给杂七八可能的文件贴标签，根据浏览器知道而我们写代码的无法知道的理由。
  </p>
  
  <p>
    如我们所见的，实际上，这有太多工作要做。
  </p>
  
  <p>
    那么，如果我们反过来呢？
  </p>
  
  <p>
    譬如不再提供给浏览器一些乱七八糟的预案，只是告诉它它所不知道的东西？也就是说，图片相对于视口将怎样变换大小，以及源文件的尺寸。如果我们有办法把这些知识分享给浏览器，那选择源的条件不都就有了吗？
  </p>
  
  <p>
    是的！实际上，这也是<a href="http://picture.responsiveimages.org/">最新的 <picture> 细则中</a> <code>size</code> 属性和 <code>srcset</code> 中的 <code>w</code> 描述符所做的事。再来看一张表：
  </p>
  
  <table>
    <tr>
      <th>
        变量
      </th>
      
      <th>
        作者在写代码时是否清楚？
      </th>
      
      <th>
        浏览器加载页面时是否清楚？
      </th>
    </tr>
    
    <tr>
      <td>
        视口尺寸
      </td>
      
      <td>
        no
      </td>
      
      <td>
        yes
      </td>
    </tr>
    
    <tr>
      <td>
        图片相对视口的比例
      </td>
      
      <td>
        yes
      </td>
      
      <td>
        <del>no</del>yes! 通过 <code>size</code>！
      </td>
    </tr>
    
    <tr>
      <td>
        像素密度
      </td>
      
      <td>
        no
      </td>
      
      <td>
        yes
      </td>
    </tr>
    
    <tr>
      <td>
        源文件尺寸
      </td>
      
      <td>
        yes
      </td>
      
      <td>
        <del>no</del>yes! 通过 <code>srcset</code>！
      </td>
    </tr>
  </table>
  
  <p>
    <a href="https://www.zfanw.com/blog/wp-content/uploads/2014/10/rainbow.png" rel="attachment wp-att-13993"><img src="https://www.zfanw.com/blog/wp-content/uploads/2014/10/rainbow.png" alt="彩虹" width="2208" class="alignnone size-full wp-image-13993" srcset="https://www.zfanw.com/blog/wp-content/uploads/2014/10/rainbow.png 2208w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/rainbow-300x200.png 300w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/rainbow-1024x682.png 1024w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/rainbow-100x66.png 100w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/rainbow-768x512.png 768w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/rainbow-520x346.png 520w" sizes="(max-width: 2208px) 100vw, 2208px" /></a>
  </p>
  
  <p>
    在我们深入以前，且先搞明白三件事。
  </p>
  
  <p>
    第一个，也是最重要的，目前(译注：原文写于 2014.3.24，译文的时间里 Chrome 34、Firefox 33 中已经实现)没有一个浏览器实现了它们，但前景看起来很不错，只是规范还没稳定。因此且慢使用。现在不能用，未来也只会出问题。
  </p>
  
  <p>
    第二：曾经有一个叫 <a href="http://lists.whatwg.org/htdig.cgi/whatwg-whatwg.org/2012-May/035855.html"><code>srcset</code></a> 的响应式图片提案。我们要讲的全新提案依赖的属性也叫 <code>srcset</code>。新旧 <code>srcset</code> 均在逗号分隔的资源 URLS 列表中使用 <code>w</code> 描述符，但新旧 <code>w</code> 所代表的意思完全不一样！旧的 <code>w</code> 是媒体查询的简写形式：它描述的宽度是指视口宽度。新 <code>w</code> 则表示文件的宽度。我们随后就会详细解释新的 <code>w</code>，但现在，且让我掏出《黑衣人》中的记忆消除棒，消除掉你所有关于 <code>srcset</code> 和 <code>w</code> 的知识。
  </p>
  
  <p>
    <a href="https://www.zfanw.com/blog/wp-content/uploads/2014/10/men-in-black.png" rel="attachment wp-att-13996"><img src="https://www.zfanw.com/blog/wp-content/uploads/2014/10/men-in-black.png" alt="黑衣人" width="2236" class="alignnone size-full wp-image-13996" srcset="https://www.zfanw.com/blog/wp-content/uploads/2014/10/men-in-black.png 2236w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/men-in-black-300x199.png 300w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/men-in-black-1024x682.png 1024w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/men-in-black-100x66.png 100w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/men-in-black-768x511.png 768w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/men-in-black-520x346.png 520w" sizes="(max-width: 2236px) 100vw, 2236px" /></a>
  </p>
  
  <p>
    都忘了？很好。
  </p>
  
  <p>
    第三点：如果你一路看下来，对之前的 <code>&lt;picture&gt;</code> 细则燃起过希望的话，那么你要知道，新的 <code>&lt;picture&gt;</code> 细则中，仍然允许你使用媒体查询切换源，也可以附加分辨率描述符给源 URLs。如果你是在做<a href="http://usecases.responsiveimages.org/#art-direction">艺术指导</a>或是<a href="http://usecases.responsiveimages.org/#device-pixel-ratio-based-selection">固定大小的分辨率切换</a>，那你绝对应该使用这些特性。但如果你只是想让你的图片伸缩，则别有新工具可用。
  </p>
  
  <p>
    Okay。我想我已经扫清障碍，做好准备。让我们处理下我们的<a href="http://ericportis.com/assets/2014-03-24-srcset-sizes/wolves/">案例</a>，这次使用 <code>srcset</code> 和 <code>size</code>。
  </p>
  
  <p>
    回顾一下，我们的图片有三个版本：
  </p>
  
  <ul>
    <li>
      <code>large.jpg</code> (1024 x 768)
    </li>
    <li>
      <code>medium.jpg</code> (640 x 480)
    </li>
    <li>
      <code>small.jpg</code> (320 x 240)
    </li>
  </ul>
  
  <p>
    还有一个 36em 的断点位置，我们的布局从一列切换到三列。
  </p>
  
  <p>
    下面是标记：
  </p>
  
  <pre><code>&lt;img src="small.jpg"
     srcset="large.jpg 1024w,
             medium.jpg 640w,
             small.jpg 320w"
     sizes="(min-width: 36em) 33.3vw,
            100vw"
     alt="A rad wolf" /&gt;
</code></pre>
  
  <p>
    你可能注意到，虽然这段标记取自 <a href="http://picture.responsiveimages.org/"><code>picture</code> 细则</a>，但我们却没见到 <code>picture</code> 元素。<code>srcset</code> 和 <code>size</code> 属性是应用到 <code>&lt;img&gt;</code> 的，对于类似这个的简单的非艺术指导，非类型切换的案例，你可以也应该使用我们的老朋友 <code>&lt;img&gt;</code> 的实例来标记你的响应式图片。
  </p>
  
  <p>
    一样的旧 <code>&lt;img&gt;</code>，全新的属性；让我们一个个看过去。
  </p>
  
  <pre><code>src="small.jpg"
</code></pre>
  
  <p>
    这个一点都不新鲜嘛。正是我们的回落(fallback) <code>src</code>，功能照旧，在浏览器不识 <code>srcset</code> & <code>size</code> 的时候加载该图片。
  </p>
  
  <p>
    下一个！
  </p>
  
  <pre><code>srcset="large.jpg 1024w,
        medium.jpg 640w,
        small.jpg 320w"
</code></pre>
  
  <p>
    这个也是不说自明的。<code>srcset</code> 接受一个逗号分隔的 URLs 列表，指向当前图片的所有版本；每个图片的宽度由 <code>w</code> 描述符确定。因此，如果你”保存为 Web&#8230;“时图片为 1024&#215;768，那么就在 <code>srcset</code> 中将其标记为 <code>1024w</code>。简单。
  </p>
  
  <p>
    <a href="https://www.zfanw.com/blog/wp-content/uploads/2014/10/declarative.png" rel="attachment wp-att-14005"><img src="https://www.zfanw.com/blog/wp-content/uploads/2014/10/declarative.png" alt="表述性" width="2236" class="alignnone size-full wp-image-14005" srcset="https://www.zfanw.com/blog/wp-content/uploads/2014/10/declarative.png 2236w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/declarative-300x199.png 300w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/declarative-1024x682.png 1024w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/declarative-100x66.png 100w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/declarative-768x511.png 768w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/declarative-520x346.png 520w" sizes="(max-width: 2236px) 100vw, 2236px" /></a>
  </p>
  
  <p>
    你可能注意到，这里我们只指定了宽度。为什么不一起指定高度？我们的布局中，图片是由宽度限定的，它们的宽度通常由 CSS 明确指定，但高度不是。大部分的响应式图片也是由宽度限定的，因此细则中为了简单就只处理宽度。
  </p>
  
  <p>
    展望未来，我们有<a href="https://github.com/ResponsiveImagesCG/picture-element/issues/85">理</a><a href="https://github.com/ResponsiveImagesCG/picture-element/issues/86">由</a>(我看来，非常棒的理由)使用 <code>h</code> 描述符来描述文件的高度，只是，还不到时候。
  </p>
  
  <p>
    让我再强调一遍，你可以在 <code>srcset</code> 源中使用 <code>1x</code>/<code>2x</code> 这样的分辨率描述符替换 <code>w</code> 描述符，但不要在 <code>srcset</code> 中混合使用它们。真的。
  </p>
  
  <p>
    <a href="https://www.zfanw.com/blog/wp-content/uploads/2014/10/lightning.png" rel="attachment wp-att-14000"><img src="https://www.zfanw.com/blog/wp-content/uploads/2014/10/lightning.png" alt="x 和 w 不要混用" width="2237" class="alignnone size-full wp-image-14000" srcset="https://www.zfanw.com/blog/wp-content/uploads/2014/10/lightning.png 2237w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/lightning-300x200.png 300w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/lightning-1024x682.png 1024w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/lightning-100x66.png 100w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/lightning-768x512.png 768w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/lightning-520x346.png 520w" sizes="(max-width: 2237px) 100vw, 2237px" /></a>
  </p>
  
  <p>
    Okay，这就是 <code>srcset</code> 和 <code>w</code> 了。
  </p>
  
  <p>
    最后，浏览器在知道如何选择一个源文件前还需要知道图片在布局中的渲染尺寸。对于这个，我们有 <code>sizes</code>。从例子中看：
  </p>
  
  <pre><code>sizes="(min-width: 36em) 33.3vw,
       100vw"
</code></pre>
  
  <p>
    格式是这样的：
  </p>
  
  <pre><code>sizes="[media query] [length], [media query] [length] ... etc"
</code></pre>
  
  <p>
    我们让媒体查询与长度成对出现。浏览器检查每个媒体查询，直到碰上匹配的，就使用配对的那个长度作为源文件选择难题的最后一个因素：图片相对于视口的渲染比例。
  </p>
  
  <p>
    “那是什么？”你说，“媒体查询？我以为你说过它们非常糟糕？！”
  </p>
  
  <p>
    我确实说过，在选择源上，它们是非常糟糕的一种机制。但这里媒体查询所做的并不一样，它们只是让浏览器提前一点(也是非常关键的)时间知道它将要在页面 CSS 碰到的断点情况。记不记得，我们第一个例子中的各种查询，根本与页面的唯一断点(36em)毫无关系？我是说，60em，20em，10em &#8211; 它们到处都是。<code>sizes</code> 中的断点必须准确反应你的页面断点。媒体查询后的长度表示的是，媒体查询判断为真时，图片在布局中的长度。
  </p>
  
  <p>
    于是，浏览器就有了所有必要的信息，来做第一部分中我们这又拖、又懒、还易出错的人类需要做的那种种计算。于是我们就得以轻松，然后如上帝所愿去吃豆子。
  </p>
  
  <p>
    而且！还记得不我们的媒体查询示例只覆盖 1x & 2x 的屏幕？这个标记却可以在任何<code>设备像素比</code>上使用。不用再猜测它可能或不太可能支持哪些分辨率了。2016 年 4.8625x 的智能手表出来时，<code>srcset</code> & <code>sizes</code> 也已覆盖。
  </p>
  
  <p>
    再者！这个办法也给了浏览器一些空间。指定给源的媒体查询或为真或为假，如果为真，则浏览器必须加载相应的源文件。<code>sizes</code> 和 <code>srcset</code> 没那么死板。规范允许浏览器当带宽或慢或贵的时候加载较小的源文件。
  </p>
  
  <p>
    “嗯，所有这些无疑地听起来很棒，”你说，缓缓地点着头，开始理解描述性的而非条件方法的好处。“可是等等，什么是长度？”
  </p>
  
  <p>
    <a href="http://www.w3.org/TR/css3-values/#lengths">长度可以千奇百怪！</a>一个长度可以是绝对的（比如 <code>99px</code>，<code>16em</code>）或是相对的（<code>33.3vw</code>，就像我们的例子中）。你可能会注意到，不跟我们的例子一样，许多布局会结合使用绝对和相对单位。这也是<a href="http://caniuse.com/calc">意外地支持性特别好</a>的 <a href="http://dev.w3.org/csswg/css-values/#calc-notation">calc() 函数</a>的用处。比如说我要给我们的<a href="http://ericportis.com/assets/2014-03-24-srcset-sizes/wolves/wolfroll.html">三列布局增加一 12em 的侧边栏</a>。我们这样调整我们的 sizes 属性：
  </p>
  
  <pre><code>sizes="(min-width: 36em) calc(.333 * (100vw - 12em)),
       100vw"
</code></pre>
  
  <p>
    好了！
  </p>
  
  <p>
    “Okay，okay，”你深思着说，摸了摸下巴，对这知识的涌入感到疲倦（也觉得激动）。“最后还有一件事：那个孤零零的 <code>100vw</code> 是什么？你是不是忘了媒体查询？
  </p>
  
  <p>
    在规范里，没有和媒体查询一同出现的长度是一个”默认长度“。如果没有匹配到哪个媒体查询，就使用默认的。这意味着，一张巨大的全宽横幅图片，你的标记可以如下简单：
  </p>
  
  <pre><code>&lt;img src="small.jpg"
     srcset="large.jpg 1024w, medium.jpg 640w, small.jpg 320w"
     sizes="100vw"
     alt="A rad wolf" /&gt;
</code></pre>
  
  <p>
    简单。
  </p>
  
  <p>
    <a href="https://www.zfanw.com/blog/wp-content/uploads/2014/10/empty-can.png" rel="attachment wp-att-14003"><img src="https://www.zfanw.com/blog/wp-content/uploads/2014/10/empty-can.png" alt="一地豆子" width="4108" class="alignnone size-full wp-image-14003" srcset="https://www.zfanw.com/blog/wp-content/uploads/2014/10/empty-can.png 4108w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/empty-can-300x109.png 300w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/empty-can-1024x372.png 1024w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/empty-can-100x36.png 100w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/empty-can-768x279.png 768w, https://www.zfanw.com/blog/wp-content/uploads/2014/10/empty-can-520x189.png 520w" sizes="(max-width: 4108px) 100vw, 4108px" /></a>
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">扩展阅读</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <a href="http://www.smashingmagazine.com/2014/05/responsive-images-done-right-guide-picture-srcset/">Responsive Images Done Right: A Guide To <picture> And srcset – Smashing Magazine</a>
    </li>
  </ol>
</div>