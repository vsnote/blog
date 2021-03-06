---
title: Compass 与 CSS 贴图定位
author: 陈 三
layout: post
date: 2013-10-04T14:01:29+00:00
excerpt: 利用 Compass 提高制作 Sprite 的效率
url: /compass-sprite.html
views:
  - 741
categories:
  - 前端开发
tags:
  - compass
  - css
  - sprite

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_Ruby"><span class="toc_number toc_depth_1">1</span> 安装 Ruby</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_compass"><span class="toc_number toc_depth_1">2</span> 安装 compass</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_compass-2"><span class="toc_number toc_depth_1">3</span> 配置 compass</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_scss"><span class="toc_number toc_depth_1">4</span> 书写 scss 文件</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    在我的前端开发工作里，CSS 贴图定位占用的时间不少。首先要切出小图片，然后放置到 sprite 大图里，确定 x、y 位置，最后写到 CSS 规则里：
  </p>
  
  <pre><code>body {
    background:url(../img/sprite.png) no-repeat -100px 0;
}
</code></pre>
  
  <p>
    Photoshop 提供的确定 x、y 位置的方法并不高效，而况我还要在 CSS 文件里手写 x、y 值，完全是低效的体力劳动。后期如果还对 Sprite 做修改，那更让人头大。
  </p>
  
  <p>
    Compass 提供了一个相对高效的<a href="http://compass-style.org/help/tutorials/spriting/">贴图定位方法</a>，我们要做的，只是切出小图，给它们命名，然后统一保存到某文件夹下，配置好 Compass，然后写 sass 文件，再运行命令：
  </p>
  
  <pre><code>compass watch
</code></pre>
  
  <p>
    接着，Compass 自动生成贴图定位的类，我们在 HTML 代码中添加相应类名就好了。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Ruby">安装 Ruby</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Ruby" href="#_Ruby"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    compass 是一个 Ruby 包，所以我们需要事先安装 <a href="https://www.ruby-lang.org/en/">Ruby</a>。最新版本的 Ruby 里已经包含 RubyGems，不需要另外安装。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_compass">安装 compass</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_compass" href="#_compass"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    打开命令行工具：
  </p>
  
  <pre><code>gem install compass
</code></pre>
  
  <p>
    这个命令会同时安装 Compass 与 Sass。我们可以通过 <code>compass version</code> 命令查看安装情况。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_compass-2">配置 compass</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_compass-2" href="#_compass-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    根据项目情况，全新创建的，还是已有项目，我们会有不同的<a href="http://compass-style.org/install/">配置命令</a>。
  </p>
  
  <p>
    比如我要在一个已有项目中配置：
  </p>
  
  <pre><code>compass create --css-dir "css" --javascripts-dir "js" --images-dir "img"
</code></pre>
  
  <p>
    Compass 会自动生成一个 sass 文件夹。
  </p>
  
  <p>
    在运行 <code>compass watch</code> 命令后，sass 文件夹下的 .scss 文件会自动编译到 css 文件夹下。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_scss">书写 scss 文件</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_scss" href="#_scss"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    假定要应用贴图定位的图片全部放在 img/icon/ 目录下，总共有三张：
  </p>
  
  <ol>
    <li>
      upload.png
    </li>
    <li>
      download.png
    </li>
    <li>
      pause.png
    </li>
  </ol>
  
  <p>
    则 sass 目录下，我们的 .scss 文件这样写：
  </p>
  
  <pre><code>@import "icon/*.png";
@include all-icon-sprites;
</code></pre>
  
  <p>
    <strong>注意</strong>：scss 文件中的 <strong>icon</strong> 是对应于 img 目录下的 <strong>icon</strong> 目录名称的。
  </p>
  
  <p>
    <code>compass watch</code> 命令在 css 目录下编译出的 css 文件如下：
  </p>
  
  <pre><code>/* line 58, icon/*.png */
.icon-sprite, .icon-download, .icon-pause, .icon-upload {
  background: url('/img/icon-seab081b7aa.png') no-repeat;
}

/* line 60, ../../../.rvm/gems/ruby-2.0.0-p247/gems/compass-0.12.2/frameworks/compass/stylesheets/compass/utilities/sprites/_base.scss */
.icon-download {
  background-position: 0 0;
}

/* line 60, ../../../.rvm/gems/ruby-2.0.0-p247/gems/compass-0.12.2/frameworks/compass/stylesheets/compass/utilities/sprites/_base.scss */
.icon-pause {
  background-position: 0 -256px;
}

/* line 60, ../../../.rvm/gems/ruby-2.0.0-p247/gems/compass-0.12.2/frameworks/compass/stylesheets/compass/utilities/sprites/_base.scss */
.icon-upload {
  background-position: 0 -512px;
}
</code></pre>
  
  <p>
    另外，img 目录下多出一个 icon-xxxxxxx.png 的图片，这是 compass 自动组合生成的，不需要我们操心。
  </p>
  
  <p>
    接下来，我们在 HTML 代码中引用上述类即可：
  </p>
  
  <pre><code>&lt;i class="icon-upload"&gt;&lt;/i&gt;
</code></pre>
  
  <p>
    如果我们要明确每个贴图的宽度、高度，只要在 scss 文件中的 <code>@include all-icon-sprites</code> 后加个 <code>true</code>：
  </p>
  
  <pre><code>@include all-icon-sprites(true);
</code></pre>
  
  <p>
    生成的 CSS 会变成如下：
  </p>
  
  <pre><code>/* line 58, icon/*.png */
.icon-sprite, .icon-download, .icon-pause, .icon-upload {
  background: url('/img/icon-seab081b7aa.png') no-repeat;
}

/* line 60, ../../../.rvm/gems/ruby-2.0.0-p247/gems/compass-0.12.2/frameworks/compass/stylesheets/compass/utilities/sprites/_base.scss */
.icon-download {
  background-position: 0 0;
  height: 256px;
  width: 256px;
}

/* line 60, ../../../.rvm/gems/ruby-2.0.0-p247/gems/compass-0.12.2/frameworks/compass/stylesheets/compass/utilities/sprites/_base.scss */
.icon-pause {
  background-position: 0 -256px;
  height: 256px;
  width: 256px;
}

/* line 60, ../../../.rvm/gems/ruby-2.0.0-p247/gems/compass-0.12.2/frameworks/compass/stylesheets/compass/utilities/sprites/_base.scss */
.icon-upload {
  background-position: 0 -512px;
  height: 256px;
  width: 256px;
}
</code></pre>
</div>