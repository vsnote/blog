---
title: webpack 使用教程
author: 陈 三
layout: post
date: 2015-08-28T13:19:03+00:00
excerpt: webpack 入门
url: /webpack-tutorial.html
views:
  - 10315
categories:
  - 前端开发
tags:
  - webpack

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_8211_webpack"><span class="toc_number toc_depth_1">1</span> 起手式 &#8211; 安装 webpack</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">2</span> 初始化项目</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#webpack"><span class="toc_number toc_depth_1">3</span> webpack 配置</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">4</span> 实时刷新</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-3"><span class="toc_number toc_depth_1">5</span> 第三方库</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-4"><span class="toc_number toc_depth_1">6</span> 模块化</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-5"><span class="toc_number toc_depth_1">7</span> 打包、构建</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    我最近大量使用 <a href="https://www.zfanw.com/blog/tag/jspm">jspm</a>，但因为它搭建的环境里，测试代码不好写，而项目又有写测试的计划，所以决定改用 <a href="http://webpack.github.io/">webpack</a>。
  </p>
  
  <p>
    我还记得我刚接触 webpack 时的心情：零零碎碎。
  </p>
  
  <p>
    就没个简单、现成、完整的方案？我是说，我真的不太关心 js 文件要配什么加载器。我只想快一点把开发环境搭起来好干活。总之，几经折腾，我嫌麻烦放弃了 webpack 这个方案。
  </p>
  
  <p>
    但今天回头去看，其实它并没那么复杂。
  </p>
  
  <p>
    那么，webpack 是什么？
  </p>
  
  <blockquote>
    <p>
      MODULE BUNDLER
    </p>
  </blockquote>
  
  <p>
    它是这么自称的，<strong>模块打包器</strong>。
  </p>
  
  <p>
    在 webpack 里，所有类型的文件都可以是模块，包含我们最常见的 JavaScript，以及 css 文件、图片、json 文件等等。通过 webpack 的各种加载器，我们可以更有效地管理这些文件。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_8211_webpack">起手式 &#8211; 安装 webpack</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_8211_webpack" href="#_8211_webpack"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    我们通过 <code>npm</code> 全局安装 webpack：
  </p>
  
  <pre><code>npm install webpack -g
</code></pre>
  
  <p>
    安装完成后，我们可以使用 <code>webpack</code> 命令，执行
  </p>
  
  <pre><code>webpack --help
</code></pre>
  
  <p>
    能够查看 webpack 提供的所有命令。
  </p>
  
  <p>
    <strong>不过，通常建议在项目目录中安装一份本地的 webpack：</strong>
  </p>
  
  <pre><code>npm install webpack --save-dev
</code></pre>
  
  <p>
    如果觉得 npm 安装太慢，可以尝试 npm 的替代工具 <a href="http://gugel.io/ied/">ied</a> &#8211; 我的使用经历，它的速度比 npm 快太多了。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">初始化项目</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    安装好 webpack 后，我们要怎么开始一个项目？
  </p>
  
  <p>
    如果你用过 grunt.js、gulpjs 一类工具，它们可以借助 <a href="https://github.com/yeoman/generator-webapp">yeoman 来初始化项目</a>。webpack 的情况不太一样，我们可以把它当作 node.js 项目来初始化。当然，借用一些模板会更省事，比如 <a href="https://github.com/gaearon/react-transform-boilerplate">react transform boilerplate</a>。
  </p>
  
  <p>
    但这里还是聊聊如何手动初始化一个 webpack 项目。
  </p>
  
  <ol>
    <li>
      <p>
        创建一个 package.json 文件，用于保存项目版本、依赖关系等
      </p>
      
      <pre><code>npm init
</code></pre>
    </li>
    
    <li>
      <p>
        在当前目录下安装 webpack
      </p>
      
      <pre><code>npm install webpack --save-dev
</code></pre>
    </li>
  </ol>
  
  <p>
    之后，我们的项目下有两个内容：
  </p>
  
  <ol>
    <li>
      package.json 文件
    </li>
    <li>
      node_modules 文件夹
    </li>
  </ol>
  
  <p>
    我们还需要一个 <code>index.html</code> 文件，示例如下：
  </p>
  
  <pre><code>&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
    &lt;meta charset="UTF-8"&gt;
    &lt;title&gt;webpack 教程&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;/body&gt;
&lt;/html&gt;
</code></pre>
  
  <p>
    现在，我们可以通过 <a href="https://github.com/tapio/live-server">live-server</a> 等访问到 index.html 页面。
  </p>
  
  <p>
    目前页面上还是一片空白，除了一个标题。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="webpack">webpack 配置</span><a title="标题链接地址" class="u-floatRight hidden" id="heywebpack" href="#webpack"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    在单页面应用里，项目通常会有一个入口（entry）文件，假设是 <code>main.js</code>，我们通过配置 webpack 来指明它的位置。
  </p>
  
  <p>
    首先，在项目根目录新建一个 <code>webpack.config.js</code>，这是 webpack 默认的配置文件名称，添加以下内容：
  </p>
  
  <pre><code>module.exports = {
  entry: './main.js'
};
</code></pre>
  
  <p>
    这时在项目根目录执行 <code>webpack</code>，会提示我们，
  </p>
  
  <blockquote>
    <p>
      Output filename not configured.
    </p>
  </blockquote>
  
  <p>
    因为我们只是设定了入口（entry），还没有设定一个输出文件的路径与名称。
  </p>
  
  <p>
    在 <code>webpack.config.js</code> 中添加一个 <code>output</code>：
  </p>
  
  <pre><code>module.exports = {
    entry: './main.js',
    output: {
        path: __dirname, // 输出文件的保存路径
        filename: 'bundle.js' // 输出文件的名称
    }
}
</code></pre>
  
  <p>
    现在在项目里执行 <code>webpack</code> 命令，我们的根目录下会多出一个 <code>bundle.js</code> 文件：
  </p>
  
  <p>
    <a href="//www.zfanw.com/blog/wp-content/uploads/2015/06/Screen-Shot-2015-06-05-at-20.53.08.png" rel="attachment wp-att-16394"><img src="//www.zfanw.com/blog/wp-content/uploads/2015/06/Screen-Shot-2015-06-05-at-20.53.08.png" alt="webpack build" width="766" class="alignnone size-full wp-image-16394" srcset="https://www.zfanw.com/blog/wp-content/uploads/2015/06/Screen-Shot-2015-06-05-at-20.53.08.png 766w, https://www.zfanw.com/blog/wp-content/uploads/2015/06/Screen-Shot-2015-06-05-at-20.53.08-300x82.png 300w, https://www.zfanw.com/blog/wp-content/uploads/2015/06/Screen-Shot-2015-06-05-at-20.53.08-100x27.png 100w, https://www.zfanw.com/blog/wp-content/uploads/2015/06/Screen-Shot-2015-06-05-at-20.53.08-520x143.png 520w" sizes="(max-width: 766px) 100vw, 766px" /></a>
  </p>
  
  <p>
    接下来，在 index.html 中引用 bundle.js 文件：
  </p>
  
  <pre><code>&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
    &lt;meta charset="UTF-8"&gt;
    &lt;title&gt;webpack 教程&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;script src="./bundle.js"&gt;&lt;/script&gt; &lt;!-- 在 index.html 文件中添加这一行代码 --&gt;
&lt;/body&gt;
&lt;/html&gt;
</code></pre>
  
  <p>
    大功告成。
  </p>
  
  <p>
    这是 webpack 与 browserify 一类工具的特点，它们在 HTML 文件中直接引用构建后的 js 文件，而不是源文件。
  </p>
  
  <p>
    当然，这可能会引发性能问题，毕竟，如果每一点文件修改都会导致整个 bundle.js 文件重新构建的话，碰上大一点的项目，有几千个源文件要编译，编译速度降下来是必然的。webpack 有它的解决办法，具体参见<a href="https://webpack.github.io/docs/build-performance.html">它的文档</a>。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">实时刷新</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    在 html 文件中引用 bundle.js 文件后，我们有几个问题需要解决。
  </p>
  
  <ol>
    <li>
      <p>
        <code>main.js</code> 或它所引用的模块的变化如何通知 webpack，重新生成 <code>bundle.js</code>？
      </p>
      
      <p>
        非常简单，在根目录下执行 <code>webpack --watch</code> 就可以监控目录下的文件变化并实时重新构建。
      </p>
    </li>
    
    <li>
      <p>
        上面只是实时构建，我们该如何把结果通知给浏览器页面，让 HTML 页面上的 bundle.js 内容保持最新？
      </p>
      
      <p>
        webpack 提供了 <a href="http://webpack.github.io/docs/webpack-dev-server.html">webpack-dev-server</a> 解决实时刷新页面的问题，同时解决实时构建的问题。
      </p>
    </li>
  </ol>
  
  <p>
    ​
  </p>
  
  <h3>
    安装 webpack-dev-server
  </h3>
  
  <ol>
    <li>
      <p>
        在全局环境中安装 webpack-dev-server：
      </p>
      
      <pre><code>npm install webpack-dev-server -g
</code></pre>
    </li>
    
    <li>
      <p>
        在项目根目录下执行命令：
      </p>
      
      <pre><code>$ webpack-dev-server
</code></pre>
      
      <p>
        这样，我们就可以在默认的 <code>http://localhost:8080</code> 网址上打开我们的 index.html。
      </p>
    </li>
  </ol>
  
  <p>
    此时，我们可能认为事情是按以下顺序发生的，
  </p>
  
  <ol>
    <li>
      js 文件修改
    </li>
    <li>
      webpack-dev-server 监控到变化
    </li>
    <li>
      webpack 在内存中重新构建 bundle.js
    </li>
    <li>
      webpack-dev-server 保证页面引用的 bundle.js 文件与内存中一致
    </li>
  </ol>
  
  <p>
    但不幸的是，我们「自以为是」了。<code>http://localhost:8080/index.html</code> 对 js 文件的变化无动于衷。
  </p>
  
  <p>
    webpack-dev-server 提供了<a href="http://webpack.github.io/docs/webpack-dev-server.html#automatic-refresh">两种模式</a>用于自动刷新页面：
  </p>
  
  <ol>
    <li>
      <p>
        iframe 模式
      </p>
      
      <p>
        我们不访问 <code>http://localhost:8080</code>，而是访问 <code>http://localhost:8080/webpack-dev-server/index.html</code>
      </p>
    </li>
    
    <li>
      <p>
        inline 模式
      </p>
      
      <p>
        在命令行中指定该模式，<code>webpack-dev-server --inline</code>。这样 <code>http://localhost:8080/index.html</code> 页面就会在 js 文件变化后自动刷新了。
      </p>
    </li>
  </ol>
  
  <p>
    以上说的两个页面自动刷新的模式都是指刷新整个页面，相当于点击了浏览器的<strong>刷新</strong>按钮。
  </p>
  
  <p>
    webpack-dev-server 还提供了一种 <a href="https://webpack.github.io/docs/hot-module-replacement.html"><code>--hot</code> 模式</a>，属于较高阶的应用。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-3">第三方库</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-3" href="#i-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    webpack 并不是包管理器，所以如果我们要使用第三方库，需要借助 npm。比如，在项目里安装 <code>jQuery</code>：
  </p>
  
  <pre><code>npm install jquery --save
</code></pre>
  
  <p>
    这样我们在当前项目目录下安装了 jquery，并将它写入 package.json 里的依赖里。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-4">模块化</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-4" href="#i-4"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <h3>
    模块化 JavaScript
  </h3>
  
  <p>
    如果我想用 ES6 的方式引入某个 es6 模块，比如：
  </p>
  
  <pre><code>import $ from 'whatever';
</code></pre>
  
  <p>
    怎么办？浏览器目前还不提供原生支持，webpack 原生也仅支持 CommonJS 的那种写法，但借助 <a href="http://babeljs.io/docs/setup/#webpack">babel-loader</a> ，我们可以加载 es6 模块：
  </p>
  
  <ol>
    <li>
      <p>
        安装 babel-loader
      </p>
      
      <pre><code>npm install babel-loader babel-core babel-preset-es2015 --save-dev
</code></pre>
    </li>
    
    <li>
      <p>
        配置 webpack.config.js
      </p>
      
      <p>
        在 <code>module.exports</code> 值中添加 <code>module</code>：
      </p>
      
      <pre><code>module.exports = {
entry: {
    app: ['./main.js']
},
output: {
    filename: 'bundle.js'
},
module: {
    loaders: [{
        test: /\.js$/,
        loaders: ['babel?presets[]=es2015'],
        exclude: /node_modules/
    }]
}
}
</code></pre>
      
      <p>
        这样我们就可以在我们的 js 文件中使用 ES6 语法，babel-loader 负责翻译。
      </p>
    </li>
  </ol>
  
  <p>
    上面的方法，是在 webpack.config.js 文件中给某一类型文件定义加载器，我们还可以在代码中直接指定：
  </p>
  
  <pre><code>import $ from 'babel!whatever'
</code></pre>
  
  <p>
    当然，前一种方法会更优雅。
  </p>
  
  <h3>
    CSS 加载器
  </h3>
  
  <p>
    我们可以按传统方法使用 CSS，即在 HTML 文件中添加：
  </p>
  
  <pre><code>&lt;link rel="stylesheet" href="style/app.css"&gt;
</code></pre>
  
  <p>
    但 webpack 里，CSS 同样可以模块化，使用 <code>import</code> 导入。
  </p>
  
  <p>
    因此我们不再使用 <code>link</code> 标签来引用 CSS，而是通过 webpack 的 <a href="https://github.com/webpack/style-loader">style-loader</a> 及 <a href="https://github.com/webpack/css-loader">css-loader</a>。前者将 css 文件以 <code>&lt;style&gt;&lt;/style&gt;</code> 标签插入 <code>&lt;head&gt;</code> 头部，后者负责解读、加载 CSS 文件。
  </p>
  
  <ol>
    <li>
      <p>
        安装 CSS 相关的加载器
      </p>
      
      <pre><code>npm install style-loader css-loader --save-dev
</code></pre>
    </li>
    
    <li>
      <p>
        配置 webpack.config.js 文件
      </p>
      
      <pre><code>{
// ...
module: {
    loaders: [
        { test: /\.css$/, loaders: ['style', 'css'] }
    ]
}
}
</code></pre>
    </li>
    
    <li>
      <p>
        在 main.js 文件中引入 css
      </p>
      
      <pre><code>import'./style/app.css';
</code></pre>
    </li>
  </ol>
  
  <p>
    这样，在执行 <code>webpack</code> 后，我们的 CSS 文件就会被打包进 bundle.js 文件中，如果不想它们被打包进去，可以使用 <a href="https://github.com/webpack/extract-text-webpack-plugin">extract text 扩展</a>。
  </p>
  
  <ol>
    <li>
      重启 webpack-dev-server
    </li>
  </ol>
  
  <h3>
    模块化 CSS
  </h3>
  
  <p>
    上一步里，我们 <code>import</code> 到 JavaScript 文件中的 CSS 文件中的 CSS 在打包后是仍然是全局的，也就是说，我们只是换了种加载 CSS 的方式，在书写 CSS 的时候，还是需要注意使用<a href="https://en.bem.info/method/definitions/">命名规范，比如使用 BEM</a>，否则全局环境 CSS 类的冲突等问题不会消失。
  </p>
  
  <p>
    这里，webpack 做了一个<a href="https://medium.com/seek-ui-engineering/the-end-of-global-css-90d2a4a06284">模块化 CSS 的尝试</a>，真正意思上的「模块化」，即 CSS 类不会泄露到全局环境中，而只会定义在 UI 模块内 &#8211; 类似 react.js 这类模块，或者 <a href="http://www.w3.org/wiki/WebComponents/" title="w3c web components">web components</a>。
  </p>
  
  <h3>
    autoprefixer
  </h3>
  
  <p>
    我们在写 CSS 时，按 CSS 规范写，构建时利用 autoprefixer 可以输出 -webkit、-moz 这样的浏览器前缀，webpack 同样是通过 <a href="https://github.com/passy/autoprefixer-loader" title="github autoprefixer 加载器">loader 提供该功能</a>。
  </p>
  
  <ol>
    <li>
      <p>
        安装 autoprefixer-loader
      </p>
      
      <pre><code>npm install autoprefixer-loader --save-dev
</code></pre>
    </li>
    
    <li>
      <p>
        配置 webpack.config.js
      </p>
      
      <pre><code>loaders: [{
test: /\.css$/,
loader: 'style!css!autoprefixer?{browsers:["last 2 version", "&gt; 1%"]}',
//...
}]
</code></pre>
    </li>
    
    <li>
      <p>
        重启 webpack-dev-server
      </p>
      
      <p>
        假如我们在 CSS 中写了 <code>body { display: flex; }</code> 规则，再查看 <code>bundle.js</code> 文件的话，我们能看到类似如下的代码：
      </p>
      
      <pre><code>body {\n\tdisplay: -webkit-box;\n\tdisplay: -webkit-flex;\n\tdisplay: -ms-flexbox;\n\tdisplay: flex;\n}
</code></pre>
    </li>
  </ol>
  
  <h3>
    图片
  </h3>
  
  <p>
    图片同样可以是模块，但使用的是 <a href="https://github.com/webpack/file-loader">file loader</a> 或者 <a href="https://github.com/webpack/url-loader">url loader</a>，后者会根据定义的大小范围来判断是否使用 data url。
  </p>
  
  <pre><code>import loadingIMG from 'file!../img/loading.gif'

React.render(&lt;img src={loadingIMG} /&gt;, document.getElementById('app'));
</code></pre>
  
  <h2 class="storycontent-h2">
    <span id="i-5">打包、构建</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-5" href="#i-5"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    项目结束后，代码要压缩、混淆、合并等，只需要在命令行执行：
  </p>
  
  <pre><code>webpack
</code></pre>
  
  <p>
    即可，webpack 根据 webpack.config.js 文件中的配置路径、构建文件名生成相应的文件。通常，我们会额外定义一个专门用于生产环境的配置文件，比如 <strong>webpack.production.config.js</strong>，其中可以做许多代码优化。
  </p>
</div>