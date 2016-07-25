---
title: Require.js 教程
author: 陈 三
layout: post
date: 2014-01-18T22:49:34+00:00
excerpt: require.js 的用法
url: /require-js.html
views:
  - 5979
categories:
  - 前端开发
tags:
  - AMD
  - require.js

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 全局环境中的函数</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 命名空间组织函数</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#Requirejs"><span class="toc_number toc_depth_1">3</span> Require.js</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#Requirejs-2"><span class="toc_number toc_depth_1">4</span> Require.js 的好处</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-3"><span class="toc_number toc_depth_1">5</span> 全局变量的额外说明</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-4"><span class="toc_number toc_depth_1">6</span> 修订历史</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <h2 class="storycontent-h2">
    <span id="i">全局环境中的函数</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    我开始学 JavaScript 时，函数通常这么写：
  </p>
  
  <pre><code>function fun1() {
  // some code here
}

function fun2() {
  // some other code here
}
...
</code></pre>
  
  <p>
    对，函数写在全局环境里。项目如果较小，通常不会有<strong>命名冲突</strong>问题。
  </p>
  
  <p>
    但代码多了以后，函数名常常不够用。于是引入命名空间，按功能模块化代码。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">命名空间组织函数</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    在命名空间下，代码可能是这样写：
  </p>
  
  <pre><code>var com = com || {};
com.zfanw = com.zfanw || {};

// 模块一
com.zfanw.module1 = (function() {
  // some code here
  return {
    func1: func1,
    ...
  };
}());

// 模块二
com.zfanw.module2 = (function() {
  // some other code here
  return {
    func1: func1,
    ...
  };
}());
...
</code></pre>
  
  <p>
    至此，代码冲突的可能性已经很小，但又会有代码依赖、脚本文件管理、阻塞等问题。
  </p>
  
  <p>
    <a href="http://requirejs.org/" title="require.js 官网页面">Require.js</a> 可以帮忙解决这些问题。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="Requirejs">Require.js</span><a title="标题链接地址" class="u-floatRight hidden" id="heyRequirejs" href="#Requirejs"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    首先了解下 require.js 里<a href="http://requirejs.org/docs/api.html#define" title="require.js 模块是什么">模块的概念</a>：
  </p>
  
  <blockquote>
    <p>
      A module is different from a traditional script file in that it defines a well-scoped object that avoids polluting the global namespace. It can explicitly list its dependencies and get a handle on those dependencies without needing to refer to global objects, but instead receive the dependencies as arguments to the function that defines the module.
    </p>
  </blockquote>
  
  <p>
    简单说，有两点：
  </p>
  
  <ol>
    <li>
      模块作用域自成一体，不会污染全局空间
    </li>
    <li>
      模块明确依赖关系，依赖通过参数传递进入模块作用域，不需要引用全局变量
    </li>
  </ol>
  
  <h3>
    定义模块
  </h3>
  
  <p>
    与上面使用的命名空间方式不同，require.js 使用全局方法 <code>define</code> 定义模块，形式如下：
  </p>
  
  <pre><code>define(id?, dependencies?, factory); // ? 表示可选
</code></pre>
  
  <p>
    我且把模块分两种。
  </p>
  
  <h4>
    无依赖的模块
  </h4>
  
  <p>
    假如一个模块不依赖其他模块，那么定义起来很简单，比如模块 hello 保存在 hello.js 文件中：
  </p>
  
  <pre><code>define(function() {

  // some code here
  return {
    // some public api
  };
});
</code></pre>
  
  <h4>
    有依赖的模块
  </h4>
  
  <p>
    有依赖的模块要稍复杂，<code>define</code> 时，我们需罗列模块的依赖情况：
  </p>
  
  <pre><code>define(['jquery'], function($) { 
// 比如这个模块，代码依赖 jQuery，require.js 会先加载并执行 `jquery` 模块代码，
// 然后将依赖模块以 `$` 的参数形式传入回调函数中，回调函数将执行结果注册为模块

  // maybe some code here
  return {
    // public api
  };
});
</code></pre>
  
  <h4>
    模块名称
  </h4>
  
  <p>
    <code>define</code> 函数共有三个参数，第一个参数 id 定义模块名称，这个名称的格式即 <code>baseUrl</code> 的路径除去文件格式，比如 <code>baseUrl</code> 为 js 目录，一个模块放在 js/libs/hi.js 里，则模块名称：
  </p>
  
  <pre><code>define('libs/hi', ['jquery'], function($){......});
</code></pre>
  
  <p>
    这种定义形式的好处是，模块不可能冲突，因为操作系统不允许同一目录下存在同名文件。但也因此 require.js 建议我们不要设置模块名称，因为设置了 &#8216;libs/hi&#8217; 的模块名称后，模块就必须放在 js/libs 目录下的 hi.js 文件中，要是我们移动位置，模块名称要跟着改变。
  </p>
  
  <h3>
    使用模块
  </h3>
  
  <p>
    在定义好模块后，我们该怎么使用？Require.js 同样提供了一个全局函数 <code>require</code>（与 <code>requirejs</code> 等效）。
  </p>
  
  <p>
    <code>require</code> 函数加载依赖并执行回调：
  </p>
  
  <pre><code>require(['jquery'], function($) { 

// 代码加载 jquery 依赖，然后执行回调代码
  console.log($);
});
</code></pre>
  
  <p>
    举一个简单例子。我有一个文件夹，文件结构如下：
  </p>
  
  <ul>
    <li>
      index.html
    </li>
    <li>
      js/ <ul>
        <li>
          main.js
        </li>
        <li>
          require.js
        </li>
        <li>
          jquery.js
        </li>
      </ul>
    </li>
  </ul>
  
  <p>
    这里 jquery.js 已经注册为 AMD 模块，则 HTML 文件里这样引用 require.js：
  </p>
  
  <pre><code>&lt;script src="js/require.js" data-main="js/main"&gt;&lt;/script&gt;
</code></pre>
  
  <p>
    require.js 会检查 <code>data-main</code> 属性值，这里是 <code>js/main</code>，根据设定，它会加载 js 目录下的 main.js 文件。
  </p>
  
  <p>
    main.js 文件里，我只做一件事，用 jQuery 方法取得当前窗口的宽度：
  </p>
  
  <pre><code>require(['jquery'], function($) {
    var w = $(window).width();
    console.log(w);
});
</code></pre>
  
  <p>
    是的，执行代码就这么简单。
  </p>
  
  <h3>
    非 AMD 规范的模块
  </h3>
  
  <p>
    但事情远没有我们想像中美好，AMD 只是一种社区规范，并非标准，而且在它出来以前，已经有各种各样的流行库存在，更不用说我们自己早期写的代码，所以我们一定会遇上非 AMD 规范的模块。
  </p>
  
  <p>
    为了让 require.js 能够加载它们，并且自动识别、载入依赖，我们有两种选择：
  </p>
  
  <ol>
    <li>
      自己动手，使用 <code>define</code> 重写代码
    </li>
    <li>
      使用 Require.js 提供的配置选项 shim
    </li>
  </ol>
  
  <p>
    比如我手上一个项目，因为某种原因，还在用 jQuery 1.4.1 版本，而 jQuery 从 1.7 版本开始才注册为 AMD 模块，我要在 require.js 中使用 jQuery 1.4.1 的话，就需要先做 shim：
  </p>
  
  <pre><code>require.config({
    shim: {
        'jquery-1.4.1': { // &lt;= 这个是相对于 main.js 的路径
            exports: 'jQuery' // &lt;= 这个值需要稍加注意，稍后会提及
        },
        'libs/jquery-throttle-debounce.min': { // &lt;= jQuery 插件
            deps: ['jquery-1.4.1'] //无需 exports，因为我们只是在增强 jQuery 功能
        }
    },
});
require(['jquery-1.4.1', 'libs/jquery-throttle-debounce.min'], function($){
    console.log($.debounce);
});
</code></pre>
  
  <p>
    写完 shim，发现 <code>jquery-1.4.1</code>、<code>libs/jquery-throttle-debounce.min</code> 这样的名称太长。这里我们又有两种选择：
  </p>
  
  <ol>
    <li>
      修改 js 文件名
    </li>
    <li>
      <p>
        使用 require.js 提供的配置项 <code>paths</code> 给模块 ID 指定对应的真实文件路径
      </p>
      
      <pre><code>require.config({
paths: {
    'jquery': 'jquery-1.4.1', // &lt;= 模块 jquery 指向 js/jquery-1.4.1.js 文件
    'debounce': 'libs/jquery-throttle-debounce.min'
},
shim: {
    'jquery': {
        exports: '$'
    },
    'debounce': {
        deps: ['jquery'] 
    }
}
});
require(['jquery', 'debounce'], function($){
console.log($.debounce);
});
</code></pre>
    </li>
  </ol>
  
  <p>
    这样，引用起来就方便很多了。
  </p>
  
  <p>
    另外，需要注意 shim 中的 <code>exports</code> 项。我们如果把 exports 值改成非全局变量名，就会导致传入回调的对象变成 undefined，举个例子：
  </p>
  
  <pre><code>require.config({
    paths: {
        'jquery': 'jquery-1.4.1', 
    },
    shim: {
        'jquery': {
            exports: 'hellojQuery' // 这里我把 exports 值设置为 jQuery/$ 以外的值
        }
    }
});
require(['jquery'], function($){
    console.log($);// 这里，会显示 undefined
});
</code></pre>
  
  <p>
    其他模块在做 shim 时同理，比如 underscore 需要 exports 为 <code>_</code>。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="Requirejs-2">Require.js 的好处</span><a title="标题链接地址" class="u-floatRight hidden" id="heyRequirejs-2" href="#Requirejs-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    说了这么多，Require.js 到底解决了我们什么问题？
  </p>
  
  <ol>
    <li>
      <p>
        并行加载
      </p>
      
      <p>
        我们知道，<code>&lt;script&gt;&lt;/script&gt;</code> 标签会阻塞页面 DOM 树的构建，比如加载 a.js，页面需要等它加载完成并执行结束后才能继续构建 DOM 树。而 require.js 的模块允许<strong>并行下载</strong>，没有依赖关系的模块还可以并行执行，大大加快页面访问速度。
      </p>
    </li>
    
    <li>
      <p>
        不愁依赖
      </p>
      
      <p>
        在我们定义模块的时候，我们就已经决定好模块的依赖 &#8211; c 依赖 b，b 又依赖 a。当我想用 c 模块的功能时，我只要在 require函数的依赖里指定 c：
      </p>
      
      <pre><code>require(['c'], function(c) {...});
</code></pre>
      
      <p>
        至于 c 依赖的模块，c 依赖的模块的依赖模块&#8230; 等等，require.js 会帮我们打理。
      </p>
      
      <p>
        而传统的 script 办法，我们必须明确指定所有依赖顺序：
      </p>
      
      <pre><code>&lt;script src="js/a.js"&gt;&lt;/script&gt;
&lt;script src="js/b.js"&gt;&lt;/script&gt;
&lt;script src="js/c.js"&gt;&lt;/script&gt;
</code></pre>
      
      <p>
        换句话说，传统的 script 方法里，我们极可能要靠记忆或者检查模块内容这种方式来确定依赖 &#8211; 效率太低，容易出错。
      </p>
    </li>
    
    <li>
      <p>
        减少全局冲突
      </p>
      
      <p>
        通过 define 的方式，我们大量减少全局变量，这样代码冲突的概率基本为零。
      </p>
    </li>
  </ol>
  
  <h2 class="storycontent-h2">
    <span id="i-3">全局变量的额外说明</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-3" href="#i-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    有一点需要说明，require.js 环境中并不是只有 <code>define</code> 和 <code>require</code> 两个全局变量。许多库都会向全局环境中暴露变量，以 jQuery 为例，1.7 版本后，它虽然注册自己为 AMD 模块，但同时也向全局环境中暴露 <code>jQuery</code> 与 <code>$</code>。所以下面的代码中，虽然我们没有向回调函数传入一份引用，jQuery/$ 同样是存在的：
  </p>
  
  <pre><code>require(['jquery'], function(){ 
  console.log(jQuery); 
  console.log($);
});
</code></pre>
  
  <div class='timeline'>
    <h2 class="storycontent-h2">
      <span id="i-4">修订历史</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-4" href="#i-4"><span class="" aria-hidden="true">#</span></a>
    </h2>
    
    <ol>
      <li>
        <span itemprop='dateModified'>2015-06-21</span>：修改排版，删除不必要文字
      </li>
    </ol>
  </div>
</div>