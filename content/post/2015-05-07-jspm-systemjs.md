---
title: 'jspm & SystemJS 教程'
author: 陈 三
layout: post
date: 2015-05-07T12:55:32+00:00
excerpt: '使用 jspm & SystemJS'
url: /jspm-systemjs.html
views:
  - 3180
categories:
  - 前端开发
tags:
  - bower
  - gulp.js
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
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 包管理器</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 加载器</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#jspm"><span class="toc_number toc_depth_1">3</span> jspm</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    我的经验，前端开发上要解决的问题能简单分为两个阶段：
  </p>
  
  <ol>
    <li>
      开发阶段
    </li>
    <li>
      部署阶段
    </li>
  </ol>
  
  <p>
    其中开发阶段要解决：
  </p>
  
  <ol>
    <li>
      第三方包安装、使用、依赖关系的维护
    </li>
    <li>
      自有代码的依赖关系维护及使用
    </li>
  </ol>
  
  <p>
    先来聊聊开发阶段的解决方案。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">包管理器</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    最初在 jQuery 站点上，文档可能是这样写的：
  </p>
  
  <ol>
    <li>
      下载 jquery.min.js 文件
    </li>
    <li>
      保存到 js 目录
    </li>
    <li>
      在 HTML 文件中使用 <code>script</code> 标签引用 jquery
    </li>
  </ol>
  
  <p>
    因为 jQuery 不依赖其它库，所以相对来说，上面的操作还算简单。
  </p>
  
  <p>
    但如果碰上有依赖关系的，比如 Bootstrap 依赖于 jQuery，我们可能就需要分开下载 Bootstrap 与 jQuery。好在这一类第三方库通常都在下载文件中打包好依赖了。但这样又有一个问题，如果另一个库也同样打包一个 jQuery，并且版本与 Bootstrap 里打包的不一致呢。可以想像，这样的情况并不少见，我们的开发目录最终容易失控 &#8211; 添加包很容易，删除就难了。另外，手工来做这件事，效率太低。
  </p>
  
  <p>
    包管理器的意义就在这里。它封装了细节，自动化处理我们的需求。我们只需要提问题，它们提供答案：
  </p>
  
  <ol>
    <li>
      我要使用 jQuery &#8211; 好，<code>bower install jquery</code>
    </li>
    <li>
      我要使用 Bootstrap &#8211; 好， <code>bower install bootstrap</code>，顺便会把依赖 jQuery 一起安装了
    </li>
    <li>
      我想了想，还是删除 Bootstrap 吧 &#8211; 好， <code>bower uninstall bootstrap</code>
    </li>
  </ol>
  
  <p>
    包管理器会维护一个依赖清单，个中关系一目了然。
  </p>
  
  <p>
    当然，以上只是用 <a href="http://bower.io/" title="bower 官网">bower</a> 举例，市面上同类产品还非常多，比如 <a href="http://duojs.org/" title="doujs 官网">duojs</a>，本文的主角 <a href="http://jspm.io/" title="jspm 官网">jspm</a> 也是一个，甚至 npm 都算。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">加载器</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    包管理器解决了我们管理各种模块的需求。接下来，我们要利用这些模块来开发，那么就会碰上如何使用这些模块的问题了。
  </p>
  
  <p>
    目前 ES6 模块的标准还没在浏览器中得到完全落实，过渡期间我们有许多规范或不规范的模块：
  </p>
  
  <ol>
    <li>
      <a href="http://www.commonjs.org/" title="commonjs 官网">CommonJS</a>
    </li>
    <li>
      <a href="https://github.com/amdjs/amdjs-api/wiki/AMD" title="托管在 github 上的 AMD 说明">AMD</a>
    </li>
    <li>
      <a href="http://wiki.ecmascript.org/doku.php?id=harmony:modules" title="ecmacript 上的 modules 文档">ES6 Modules</a>
    </li>
    <li>
      命名空间方式定义
    </li>
    <li>
      其它
    </li>
  </ol>
  
  <p>
    如果只使用单一规范，比如针对 AMD，我们可能会用 <a href="http://requirejs.org/" title="requirejs 官网">RequireJS</a>；ES6 的模块，我们可能会用到 <a href="https://github.com/ModuleLoader/es6-module-loader" title="es6-module-loader 的 github 库">ES6 Module Loader Polyfill</a>；CommonJS 规范的模块，我们可能用 <a href="https://github.com/systemjs/systemjs" title="systemJS 的 github 库">SystemJS</a> &#8211; 它同样可用于加载 AMD/ES6 模块。
  </p>
  
  <h3>
    CSS 加载器？？
  </h3>
  
  <p>
    上面提及的加载器，通常是针对 JavaScript 模块的，CSS 并没有严格意义的模块，那它怎么管理？我们的包管理器当然会连着包的 CSS 文件一同管理。那我们该如何使用这些模块中的 CSS 呢？举 SystemJS 来说，我们可以通过它的插件执行 <code>import</code> 命令动态插入 CSS。打包的时候，SystemJS 默认会把整个 CSS 文件打包入 JS 文件中。当然，我们也可以借助 bower 与 gulp.js 及 <a href="https://github.com/taptapship/wiredep" title="wiredep 插件">gulp.js 的 wiredep 插件</a> 这样的组合实现在页面上「主动」插入 <code>link</code> 标签 &#8211; 但这需要搭配 gulp.js 等工具。
  </p>
  
  <p>
    走完开发阶段，我们来看看部署阶段要解决的几个明显问题：
  </p>
  
  <ol>
    <li>
      CSS 文件合并、压缩等
    </li>
    <li>
      JavaScript 文件合并、压缩、混淆等
    </li>
  </ol>
  
  <p>
    不过，还是先正式介绍 jspm 与 SystemJS 的用法。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="jspm">jspm</span><a title="标题链接地址" class="u-floatRight hidden" id="heyjspm" href="#jspm"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    如前所说的，jspm 是一个浏览器端包管理器。
  </p>
  
  <h3>
    安装 jspm
  </h3>
  
  <pre><code>npm install jspm -g
</code></pre>
  
  <h3>
    初始化目录
  </h3>
  
  <p>
    在安装完 jspm 后，我们在命令行下就有一个 <code>jspm</code> 命令可用。
  </p>
  
  <p>
    创建一个目录，执行 <code>jspm init</code> 即可在该目录下初始化开发环境：
  </p>
  
  <pre><code>Package.json file does not exist, create it? [yes]: 
Would you like jspm to prefix the jspm package.json properties under jspm? [yes]: 
Enter server baseURL (public folder path) [.]: 
Enter jspm packages folder [./jspm_packages]: 
Enter config file path [./config.js]: 
Configuration file config.js doesn't exist, create it? [yes]:
Enter client baseURL (public folder URL) [/]: 
Which ES6 transpiler would you like to use, Traceur or Babel? [traceur]:
</code></pre>
  
  <p>
    如果你用过 <a href="http://yeoman.io/" title="yeoman 官网">yeoman</a> 一类工具，对这类提示应该非常熟悉。
  </p>
  
  <h3>
    安装第三方库
  </h3>
  
  <p>
    比如要安装 jQuery：
  </p>
  
  <pre><code>jspm install jquery
</code></pre>
  
  <p>
    这条命令会从 github:components/jquery 上读取下载。
  </p>
  
  <p>
    还可以从 npm 上下载安装：
  </p>
  
  <pre><code>jspm install npm:jquery
</code></pre>
  
  <h3>
    创建 HTML 文件
  </h3>
  
  <p>
    创建一个 index.html 文件如下：
  </p>
  
  <pre><code> &lt;!doctype html&gt;
  &lt;script src="jspm_packages/system.js"&gt;&lt;/script&gt;
  &lt;script src="config.js"&gt;&lt;/script&gt;
  &lt;script&gt;
    System.import('app');
  &lt;/script&gt;
</code></pre>
  
  <p>
    首先我们需要引用 <code>jspm_packages/system.js</code>，这个是 jspm 提供的万用加载器。之后是 <code>config.js</code> 文件，我们安装的各种包、依赖等信息都在这个文件中维护，之后我们用全局的 <code>System.import</code> 执行 index.html 同一目录下的 app.js 文件。
  </p>
  
  <p>
    在 app.js 文件中，我们使用 ES6 语法：
  </p>
  
  <pre><code>import $ from 'jquery';
$(function() {
  console.log($);
});
</code></pre>
  
  <p>
    假定我们要在 index.html 中使用 Bootstrap，那么先通过 <code>jspm</code> 安装：
  </p>
  
  <pre><code>jspm install bootstrap
</code></pre>
  
  <p>
    然后把 app.js 文件修改如下：
  </p>
  
  <pre><code>import bootstrap from 'bootstrap';

$(function() {
    console.log($);
});
</code></pre>
  
  <p>
    我们并没有 <code>import</code> jQuery，这是因为 jspm 维护有 bootstrap 的依赖，会自动加载 jQuery，不需要我们再手动 <code>import</code>。
  </p>
  
  <p>
    <code>import bootstrap from 'bootstrap'</code> 一行是加载了 Bootstrap 的 js 模块。那么，Bootstrap 的 CSS 部分如何加载呢？我们需要用到 <a href="https://github.com/jspm/jspm-cli/wiki/Plugins#css" title="plugin css 说明">jspm 的 CSS 插件</a>。
  </p>
  
  <p>
    首先，安装 jspm 的 css 插件：
  </p>
  
  <pre><code>jspm install css
</code></pre>
  
  <p>
    然后在 app.js 中添加一行：
  </p>
  
  <pre><code>import 'bootstrap/css/bootstrap.css!';
</code></pre>
  
  <p>
    <strong>!</strong> 表示这会经过插件处理。
  </p>
  
  <p>
    这时如果在本地服务器上打开 index.html 文件，借助浏览器的开发者工具查看：
  </p>
  
  <p>
    [resp_image id=&#8217;16028&#8242; caption=&#8221; ]
  </p>
  
  <p>
    Wow，请求有点多 &#8211; 但这只是开发阶段。
  </p>
  
  <h3>
    打包 JavaScript
  </h3>
  
  <p>
    我们终于说到 JavaScript 的打包了。
  </p>
  
  <p>
    jspm 里，js 文件的打包非常简单，举上面的例子说，如果我们只有一个 js 入口的话，则执行：
  </p>
  
  <pre><code>jspm bundle-sfx app build.js --minify
</code></pre>
  
  <p>
    就可以将所有需要的 js 文件包括 CSS 文件打包到一个 build.js 文件中。
  </p>
  
  <p>
    之后修改 index.html 文件中 script 部分如下：
  </p>
  
  <pre><code>&lt;!--    &lt;script src="jspm_packages/system.js"&gt;&lt;/script&gt;
    &lt;script src="config.js"&gt;&lt;/script&gt;
    &lt;script&gt;
        System.import('app');
    &lt;/script&gt;--&gt;
    &lt;script src="build.js"&gt;&lt;/script&gt;
</code></pre>
  
  <p>
    这时打开 index.html 页面，就只剩下 index.html 与 build.js 两个请求了。
  </p>
  
  <h3>
    打包 CSS
  </h3>
  
  <p>
    在上在一个步骤中，我们把 CSS 文件连着一起打包进了 js 中，这可能并不是多数人想要的结果。
  </p>
  
  <p>
    我们可以通过定义 <a href="https://github.com/jspm/jspm-cli/wiki/Plugins#css-builds" title="jspm config.js 构建配置">config.js 文件</a>改变这种行为。
  </p>
  
  <p>
    打开 config.js 文件，添加 <code>seperateCSS: true</code>：
  </p>
  
  <pre><code>System.config({
  "baseURL": "/",
  "separateCSS": true
});
</code></pre>
  
  <p>
    再次执行 <code>jspm bundle-sfx app build.js --minify</code>，会在 index.html 同级目录下生成一个 build.js 与 build.css，在 index.html 中引用 build.css 文件即可。
  </p>
  
  <p>
    对比 gulp.js 或 grunt.js 等工具，jspm 给我的体验非常好，解决了开发阶段、部署阶段的几个重要难题，目前只有 ember-cli 这样的环境能给我同样的感受。
  </p>
</div>