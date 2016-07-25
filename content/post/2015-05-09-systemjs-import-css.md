---
title: SystemJS 加载 CSS
author: 陈 三
layout: post
date: 2015-05-09T01:25:42+00:00
excerpt: SystemJS 怎样动态加载 CSS 文件，需要哪些配置
url: /systemjs-import-css.html
views:
  - 1200
categories:
  - 前端开发
tags:
  - jspm
  - SystemJS

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_css"><span class="toc_number toc_depth_1">1</span> 重命名 css 目录名称</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_paths"><span class="toc_number toc_depth_1">2</span> 配置 paths</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_map_key"><span class="toc_number toc_depth_1">3</span> 修改 map 中定义的 key</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_CSS"><span class="toc_number toc_depth_1">4</span> 远程 CSS</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    <strong>说明</strong>：SystemJS & jspm 仍在开发中，所以各种接口可能会出现变化。
  </p>
  
  <p>
    上一篇曾经介绍过，<a href="http://www.zfanw.com/blog/jspm-systemjs.html#i-2">SystemJS 可以使用 css 插件加载 bootstrap 的 NPM 包中的 CSS 文件</a>。那么，如果是我们自己写的 CSS 文件，比如 css 目录下的 app.css 文件，SystemJS 里要怎么​加载？
  </p>
  
  <p>
    这里有个 SystemJS 的<a href="https://github.com/systemjs/plugin-css/issues/34">说不上是 bug 的 bug</a>。
  </p>
  
  <p>
    首先，css plugin 安装完后，在 config.js 里的 <code>map</code> 中是这样定义的：
  </p>
  
  <pre><code>"css": "github:systemjs/plugin-css@0.1.10",
</code></pre>
  
  <p>
    这里，<code>css</code> 是模块名称，可以在我们的代码中使用，<code>github:systemjs/plugin-css@0.1.10</code> 是目录，指向 <code>jspm_packages/github/systemjs/plugin-css@0.1.10</code>。
  </p>
  
  <p>
    如果我在 <code>index.html</code> 文件中这样加载 <code>app.css</code> 文件：
  </p>
  
  <pre><code>System.import('css/app.css!css');
</code></pre>
  
  <p>
    这个加载路径会指向 <code>http://localhost:3001/jspm_packages/github/systemjs/plugin-css@0.1.10/app.css</code>。Oooops，<code>import</code> 语句里的第一个 <code>css</code> 被解析为 <code>map</code> 中定义的路径了。
  </p>
  
  <p>
    目前来看，在开发者推出更佳解决办法前，只有用 workaround 了。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_css">重命名 <code>css</code> 目录名称</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_css" href="#_css"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    把 <code>css</code> 目录名改成其它，比如 <code>mycss</code>，记住，不要跟 <code>map</code> 里定义的任何模块名称冲突，否则又会出现上面的情况，然后在 <code>index.html</code> 中 <code>import</code>：
  </p>
  
  <pre><code>System.import('mycss/app.css!css');
</code></pre>
  
  <h2 class="storycontent-h2">
    <span id="_paths">配置 <code>paths</code></span><a title="标题链接地址" class="u-floatRight hidden" id="hey_paths" href="#_paths"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    我们可以在 <code>config.js</code> 文件中配置一个 <code>paths</code><fnref target="16048.1" />：
  </p>
  
  <pre><code>// 配置 CSS 文件路径
System.paths["mycss/*"] = "css/*.css";
</code></pre>
  
  <p>
    注意，在 config.js 中，模块定义的路径，都是相对于 <code>baseURL</code> 的。
  </p>
  
  <p>
    之后在 <code>index.html</code> 文件中加载：
  </p>
  
  <pre><code>System.import('mycss/app!css');
</code></pre>
  
  <p>
    <code>!css</code> 表示该文件通过 css 插件加载，SystemJS 可以通过文件扩展名自动判断使用哪个插件 &#8211; 但建议指定使用的插件名称。
  </p>
  
  <p>
    刷新页面，我们的 app.css 已经动态插入 <code>head</code> 部分了：
  </p>
  
  <p>
    [resp_image id=&#8217;16084&#8242; caption=&#8221; ]
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_map_key">修改 <code>map</code> 中定义的 key</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_map_key" href="#_map_key"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    这一个方法，拿 <code>config.js</code> 里的 <code>map</code> 开刀。
  </p>
  
  <p>
    把如下代码：
  </p>
  
  <pre><code>"css": "github:systemjs/plugin-css@0.1.10",
</code></pre>
  
  <p>
    改成:
  </p>
  
  <pre><code>"style": "github:systemjs/plugin-css@0.1.10",
</code></pre>
  
  <p>
    然后在 <code>index.html</code> 中加载：
  </p>
  
  <pre><code>System.import('css/app.css!style');
</code></pre>
  
  <p>
    上面三种折衷办法中，最推荐第一个。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_CSS">远程 CSS</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_CSS" href="#_CSS"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    除了加载自有 CSS，我们还会加载 CDN 上的外部 CSS。
  </p>
  
  <p>
    同样的，我们可以在 config.js 中预先定义一个 <code>paths</code>：
  </p>
  
  <pre><code>System.paths["purecss"] = "http://yui.yahooapis.com/pure/0.6.0/pure-min.css";
</code></pre>
  
  <p>
    然后就可以在 <code>index.html</code> 文件中 <code>import</code> 了：
  </p>
  
  <pre><code>System.import('purecss!css)';
</code></pre>
  
  <p>
    不过需要注意，从 CDN 上加载的文件，目前在跑 <code>jspm bundle</code> 时会报错。
  </p>
  
  <footnotes>
    <fn name="16048.1">
      <p>
        <a href="https://github.com/systemjs/systemjs/wiki/Configuration-Options#paths-unstable">SystemJS 路径配置项</a>
      </p>
    </fn>
  </footnotes>
</div>