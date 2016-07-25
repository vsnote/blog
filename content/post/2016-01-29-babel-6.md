---
title: babel 6 教程
author: 陈 三
layout: post
date: 2016-01-29T10:25:05+00:00
excerpt: babel 5. x 与 6.x 的变化及 babel 6.x 的用法
url: /babel-6.html
views:
  - 2255
categories:
  - 前端开发
tags:
  - babel
  - webpack

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#babel-cli"><span class="toc_number toc_depth_1">1</span> babel-cli</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#babel"><span class="toc_number toc_depth_1">2</span> babel 插件</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">3</span> 预置套餐</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#babel-polyfill"><span class="toc_number toc_depth_1">4</span> babel-polyfill</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#babel-runtime"><span class="toc_number toc_depth_1">5</span> babel-runtime</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#webpack_babel-loader"><span class="toc_number toc_depth_1">6</span> webpack 中定义 babel-loader</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#babel-register"><span class="toc_number toc_depth_1">7</span> babel-register</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">8</span> 扩展阅读</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    babel 5.x -> 6.x 的变化非常大，许多模块分离出去，只是一些文档还语焉不详，这里略作整理。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="babel-cli">babel-cli</span><a title="标题链接地址" class="u-floatRight hidden" id="heybabel-cli" href="#babel-cli"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    如果你用过 CoffeeScript，或 TypeScript，那你对它们的编译过程一定很熟悉，<a href="https://babeljs.io/docs/usage/cli/">babel-cli</a> 模块同样也是一个编译的作用。
  </p>
  
  <p>
    比如有一个 test.js 文件，内容如下：
  </p>
  
  <pre><code>let fun = () =&gt; console.log('babel')
</code></pre>
  
  <p>
    那么执行 <code>babel test.js</code>，会输出以下内容：
  </p>
  
  <pre><code>"use strict";

var fun = function fun() {
  return console.log('babel');
};
</code></pre>
  
  <p>
    除了 <code>babel</code> 命令外，babel-cli 包另有一个 <code>babel-node</code> 命令，它近似于 node，只不过它在运行代码前会预先编译 ES2015 的代码。
  </p>
  
  <p>
    不论是 <code>babel</code> 命令还是 <code>babel-node</code> 命令，我们都可以通过命令行参数修改它们的行为，还可以通过新建一个 <code>.babelrc</code> 文件来配置。
  </p>
  
  <p>
    但以上是 babel 5.x 的用法。
  </p>
  
  <p>
    如果在 babel 6 里，执行 <code>babel test.js</code>，只会输出原样的文本，因为 <code>babel</code> 不再包含任何 transform 功能，babel 6 里把它们作为插件（plugin）分割出去，需要我们自己定义，见下文说明。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="babel">babel 插件</span><a title="标题链接地址" class="u-floatRight hidden" id="heybabel" href="#babel"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    在 babel 6 里，要转换 ES2015 的代码，需要自己配置插件，比如上面的示例：
  </p>
  
  <pre><code>let fun = () =&gt; console.log('babel')
</code></pre>
  
  <p>
    我们执行 <code>babel test.js</code>，babel 不会对文件做任何转换。我们需要一个 <a href="http://babeljs.io/docs/plugins/transform-es2015-arrow-functions/">ES2015 arrow functions transform</a> 插件。
  </p>
  
  <ol>
    <li>
      <p>
        安装插件
      </p>
      
      <pre><code>npm install babel-plugin-transform-es2015-arrow-functions
</code></pre>
    </li>
    
    <li>
      <p>
        在目录下创建一个 .babelrc 文件，用于配置 babel，添加如下内容：
      </p>
      
      <pre><code>{
  "plugins": ["transform-es2015-arrow-functions"]
}
</code></pre>
    </li>
    
    <li>
      <p>
        再执行 <code>babel test.js</code>，我们得到如下转换结果：
      </p>
      
      <pre><code>let fun = function () {
  return console.log('babel');
};
</code></pre>
      
      <p>
        基本上 ES2015/ES7 的各种功能，babel 都提供了相应的插件用于转换，但如果我们要一个一个配置 &#8211; 那就太恼人了。所以 babel 还提供了一个方法：presets。
      </p>
    </li>
  </ol>
  
  <h2 class="storycontent-h2">
    <span id="i">预置套餐</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    我们不妨把 presets 理解为套餐，不同套餐有不同的插件组合，比如 <a href="http://babeljs.io/docs/plugins/preset-es2015/">ES2015 preset</a> 里打包了所有用于转换 ES2015 代码的插件，<a href="http://babeljs.io/docs/plugins/preset-react/">React preset</a> 则打包了转换 react.js jsx 语法的插件。它们的用法同上面一致：
  </p>
  
  <ol>
    <li>
      <p>
        安装 preset
      </p>
      
      <pre><code>npm install babel-preset-es2015
</code></pre>
    </li>
    
    <li>
      <p>
        配置 .babelrc 文件
      </p>
      
      <pre><code>{
  "presets": ["es2015"]
}
</code></pre>
    </li>
    
    <li>
      <p>
        再执行 <code>babel test.js</code>，我们会得到与 babel 5.x 一样的转换结果：
      </p>
      
      <pre><code>'use strict';
var fun = function fun() {
  return console.log('babel');
};
</code></pre>
    </li>
  </ol>
  
  <h2 class="storycontent-h2">
    <span id="babel-polyfill">babel-polyfill</span><a title="标题链接地址" class="u-floatRight hidden" id="heybabel-polyfill" href="#babel-polyfill"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    babel 虽然可以转换各种 ES2015 语法及 jsx，但浏览器未提供原生支持的许多功能还是需要 polyfill，比如 Promise。
  </p>
  
  <p>
    我们只要在代码中引入 babel-polyfill 就可以模拟出一个 ES2015 的环境，用法如下：
  </p>
  
  <ol>
    <li>
      <p>
        安装 <code>babel-polyfill</code>
      </p>
      
      <pre><code>npm install babel-polyfill --save
</code></pre>
    </li>
    
    <li>
      <p>
        在入口文件中引用：
      </p>
      
      <pre><code>import babel-polyfill
</code></pre>
    </li>
  </ol>
  
  <h2 class="storycontent-h2">
    <span id="babel-runtime">babel-runtime</span><a title="标题链接地址" class="u-floatRight hidden" id="heybabel-runtime" href="#babel-runtime"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    与 babel-polyfill 一样，babel-runtime 的作用也是模拟 ES2015 环境。只不过，babel-polyfill 是针对全局环境的，引入它，我们的浏览器就好像具备了规范里定义的完整的特性 &#8211; 虽然原生并未实现。
  </p>
  
  <p>
    babel-runtime 更像是分散的 polyfill 模块，我们可以在自己的模块里单独引入，比如 <code>require(‘babel-runtime/core-js/promise’)</code> ，它们不会在全局环境添加未实现的方法，只是，这样手动引用每个 polyfill 会非常低效。我们借助 <a href="http://babeljs.io/docs/plugins/transform-runtime/">Runtime transform</a> 插件来自动化处理这一切。
  </p>
  
  <p>
    至于要用 babel-polyfill 还是 babel-runtime，则需要根据具体需求。举个例子，如果一个库里引用了 babel-polyfill，别人的库也引用了 babel-polyfill，我们很可能会跑两个 babel-polyfill 实例，这里，使用 babel-runtime 会更合适。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="webpack_babel-loader">webpack 中定义 babel-loader</span><a title="标题链接地址" class="u-floatRight hidden" id="heywebpack_babel-loader" href="#webpack_babel-loader"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    在 <code>webpack.config.js</code> 里这样定义：
  </p>
  
  <pre><code>module: {
  loaders:  [
    {
      test: /\.js/,
      loader: 'babel?presets[]=es2015,presets[]=react,plugins[]=transform-runtime'
    }
  ]
}
</code></pre>
  
  <h2 class="storycontent-h2">
    <span id="babel-register">babel-register</span><a title="标题链接地址" class="u-floatRight hidden" id="heybabel-register" href="#babel-register"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    <a href="https://babeljs.io/docs/usage/require/">babel-register</a> 是放在 node 里使用的。它的作用是替代 node 的 <code>require</code> 命令，与 node 自身的 <code>require</code> 不同，它可以加载 es2015、jsx 等类型文件。
  </p>
  
  <p>
    用法如下：
  </p>
  
  <pre><code>require('babel-register')({presets: ['es2015', 'react']})
require('./app')
</code></pre>
  
  <p>
    这样我们在 app 文件中就可以使用 es2015 与 jsx 语法了。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">扩展阅读</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <a href="https://medium.com/@jcse/clearing-up-the-babel-6-ecosystem-c7678a314bf3#a7d5">Clearing up the Babel 6 Ecosystem</a>
    </li>
  </ol>
</div>