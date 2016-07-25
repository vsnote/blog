---
title: React.js 服务端渲染
author: 陈 三
layout: post
date: 2016-02-05T14:01:43+00:00
url: /react-js-server-render.html
views:
  - 1184
categories:
  - 前端开发
tags:
  - react.js
  - webpack

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#renderToString"><span class="toc_number toc_depth_1">1</span> renderToString</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">2</span> 准备工作</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">3</span> 按部就班</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_bundlejs"><span class="toc_number toc_depth_1">4</span> 构建 bundle.js</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    是否多此一举？
  </p>
  
  <p>
    毕竟，从服务端渲染走到客户端渲染这一步，前端界可花了不少时间。
  </p>
  
  <p>
    如果你对服务端渲染的必要性心存疑虑，不妨先看看<a href="http://alistapart.com/article/interaction-is-an-enhancement">这一篇</a>文章。
  </p>
  
  <p>
    但我还是在这儿简单介绍下，为什么这些客户端渲染的框架们要踏入服务端渲染的领域。
  </p>
  
  <p>
    在客户端渲染时，我们的页面通常很简洁，比如，你可能见过这样的 HTML 文件：
  </p>
  
  <pre><code>&lt;!doctype html&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;这是陈三&lt;/title&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;script src='http://code.jquery.com/jquery-2.1.4.min.js'&gt;&lt;/script&gt;
    &lt;script src='http://example.com/test.bundle.js'&gt;&lt;/script&gt;
  &lt;/body&gt;
&lt;/html&gt;
</code></pre>
  
  <p>
    陈三在打开这个页面后，浏览器会加载：
  </p>
  
  <ol>
    <li>
      jquery-2.1.4.min.js
    </li>
    <li>
      test.bundle.js
    </li>
  </ol>
  
  <p>
    在这两个文件加载完成并执行以前，陈三只能看到一片空白。等了十来秒后，页面还没有动静，陈三找来专业人士，哦，jquery-2.1.4.min.js 文件不知道怎么回事，加载失败，导致 test.bundle.js 无法构建 HTML 代码。
  </p>
  
  <p>
    实际上：
  </p>
  
  <ol>
    <li>
      任何 js 代码问题都可能导致陈三看不到页面
    </li>
    <li>
      搜索引擎可能无法索引这样的页面（对，<a href="https://googlewebmastercentral.blogspot.com/2015/10/deprecating-our-ajax-crawling-scheme.html">Google 可以做到</a>，但不是所有搜索引擎都是 Google）
    </li>
  </ol>
  
  <p>
    那么，我们可以做得更好吗？
  </p>
  
  <p>
    这正是 Ember.js、Angular.js 等努力的方向。这一篇，则是介绍 react.js 在这方面的情况。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="renderToString">renderToString</span><a title="标题链接地址" class="u-floatRight hidden" id="heyrenderToString" href="#renderToString"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    react 官网文档在服务端渲染上<a href="https://facebook.github.io/react/docs/top-level-api.html#reactdomserver">着墨不多</a>：
  </p>
  
  <blockquote>
    <p>
      Render a ReactElement to its initial HTML. This should only be used on the server. React will return an HTML string. You can use this method to generate HTML on the server and send the markup down on the initial request for faster page loads and to allow search engines to crawl your pages for SEO purposes.
    </p>
    
    <p>
      If you call ReactDOM.render() on a node that already has this server-rendered markup, React will preserve it and only attach event handlers, allowing you to have a very performant first-load experience.
    </p>
  </blockquote>
  
  <p>
    简单说，<code>renderToString</code> 方法在服务器上先渲染出组件的 HTML 结构，客户端上 react 在执行到 <code>render()</code> 方法时，会检查是否有服务端渲染过的代码，如果有，则仅仅往上添加事件处理器。我们不妨这样认为，原来在客户端要执行的 js 代码被拆成两个部分：
  </p>
  
  <ol>
    <li>
      渲染 HTML 结构
    </li>
    <li>
      往 HTML 结构上附加事件处理器
    </li>
  </ol>
  
  <p>
    前者在服务端上完成，后者在客户端上完成。
  </p>
  
  <p>
    那么，我们要怎么入手 react.js 服务端渲染？react.js 初期开发者 Pete Hunt 给了些<a href="https://github.com/petehunt/react-howto#learning-server-rendering">建议</a>：
  </p>
  
  <blockquote>
    <p>
      Server rendering still requires a lot of tooling to get right. Since it transparently supports React components written without server rendering in mind, you should build your app first and worry about server rendering later. You won&#8217;t need to rewrite all of your components to support it.
    </p>
  </blockquote>
  
  <p>
    要做服务端渲染，我们要干的事还很多，但通常可以先构建 app，再来关心服务端渲染。我们并不会需要全部重写所有的组件。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">准备工作</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    我们要先解决以下问题：
  </p>
  
  <ol>
    <li>
      <p>
        server 端用什么框架？
      </p>
      
      <p>
        对前端开发来说，基于 node.js 的框架通常更易于上手，所以这里选用了 <a href="http://expressjs.com/">expressjs</a>。
      </p>
    </li>
    
    <li>
      <p>
        要构建出前端使用的 js 文件，要用什么工具？
      </p>
      
      <p>
        不论是 requirejs 还是 browserify 或 jspm 都可以用，这里使用 webpack。
      </p>
    </li>
    
    <li>
      <p>
        react.js 在后端 render 时，如果要用 jsx 语法，要怎么解决？
      </p>
      
      <p>
        使用 <a href="https://www.zfanw.com/blog/babel-6.html#babel-register">babel-register</a>。
      </p>
    </li>
    
    <li>
      <p>
        如果我想用 es2015 语法后 express.js 程序，要怎么做？
      </p>
      
      <p>
        同第 3 点。
      </p>
    </li>
  </ol>
  
  <p>
    接下来就是安装 react、react-dom、babel，并且配置 babel，<a href="https://github.com/chenxsan/react-server-render/tree/810b2cd13ccdc9d59784e97f1937efe949de21ff">点击查看项目代码</a>。
  </p>
  
  <p>
    好了，我们可以开始写代码了。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">按部就班</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    首先，我们添加一个 Home 组件，代码如下：
  </p>
  
  <pre><code>import React from 'react'
export default class Home extends React.Component {
  render () {
    return (&lt;div&gt;
              hello from 陈三。
            &lt;/div&gt;)
  }
}
</code></pre>
  
  <p>
    这个组件目前只是渲染一段 div。
  </p>
  
  <p>
    接下来是在 app.js 文件中引用它并渲染成 HTML：
  </p>
  
  <pre><code>import express from 'express'
import React from 'react'
import ReactDOM from 'react-dom/server'
import Home from './components/Home'
let app = express()
app.get('/', (req, res) =&gt; {
  res.send(ReactDOM.renderToString(React.createFactory(Home)()))
})
app.listen(3000, () =&gt; {
  console.log('listen on 3000')
})

</code></pre>
  
  <p>
    这里用到的两个方法：
  </p>
  
  <ol>
    <li>
      <a href="https://facebook.github.io/react/docs/top-level-api.html#reactdomserver.rendertostring">renderToString</a> &#8211; 将组件渲染成字符串。
    </li>
    <li>
      <a href="https://facebook.github.io/react/docs/top-level-api.html#react.createfactory">createFactory</a> &#8211; 生成一个组件工厂方法，用于生成组件。之所以用它，是因为 renderToString 接受的参数是 ReactElement element，所以我们不能使用 jsx 的形式 <code>&lt;Home /&gt;</code>。
    </li>
  </ol>
  
  <p>
    执行 <code>node index.js</code> 命令，可以在 http://localhost:3000 网址看到：
  </p>
  
  <blockquote>
    <p>
      hello from 陈三。
    </p>
  </blockquote>
  
  <p>
    点击<a href="https://github.com/chenxsan/react-server-render/tree/82ab7be8078743c31fa2e92cf62d0ffd9af69ad6">查看这一步的项目代码</a>。
  </p>
  
  <p>
    目前为止，我们还没给组件添加任何交互行为，比如点击一下，<strong>字体颜色变化</strong>。下面我们就来尝试给 Home 组件添加这一交互。
  </p>
  
  <p>
    我们将 Home 组件改造如下：
  </p>
  
  <pre><code>import React from 'react'
export default class Home extends React.Component {
  constructor (props) {
    super(props)
    this.clickToChangeColor = this.clickToChangeColor.bind(this)
    this.state = {
      color: '#' + (Math.random() * 0xFFFFFF &lt;&lt; 0).toString(16)
    }
  }
  clickToChangeColor (e) {
    this.setState({
      color: '#' + (Math.random() * 0xFFFFFF &lt;&lt; 0).toString(16)
    })
  }
  render () {
    return (&lt;div onClick={this.clickToChangeColor} style={{color: this.state.color}}&gt;
              hello from 陈三。
            &lt;/div&gt;)
  }
}

</code></pre>
  
  <p>
    现在点击 div 块，字体颜色并不会出现任何变化，因为，目前为止，我们只是在后端渲染了 HTML 结构，事件绑定等工作，要在前端上完成。
  </p>
  
  <p>
    但现在，我们还只是简单的生成一个页面，只有一个 <code>div</code> 块，没有 <code>html</code> 标签，没有 <code>meta</code> 标签，也没有引用任何脚本。
  </p>
  
  <p>
    我们需要一个完整的页面，这里，使用 <a href="http://expressjs.com/en/guide/using-template-engines.html">jade 模板引擎</a>来生成页面。
  </p>
  
  <p>
    我们在 views 目录下增加一个 <code>index.jade</code> 模板：
  </p>
  
  <pre><code>doctype html
html
    head
        title='react 服务端渲染'
        meta(charset='utf-8')
    body
        #root!= react
        script(src='/bundle.js')
</code></pre>
  
  <p>
    app.js 内容修改成：
  </p>
  
  <pre><code>import express from 'express'
import React from 'react'
import ReactDOM from 'react-dom/server'
import Home from './components/Home'
let app = express()
app.use(express.static('public'))
app.set('views', './views')
app.set('view engine', 'jade')
let html = ReactDOM.renderToString(React.createFactory(Home)())
app.get('/', (req, res) =&gt; {
  res.render('index', {react: html})
})
app.listen(3000, () =&gt; {
  console.log('listen on 3000')
})
</code></pre>
  
  <p>
    目前为止，我们还没有一个叫 <code>bundle.js</code> 的文件，它将由 webpack 来构建。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_bundlejs">构建 bundle.js</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_bundlejs" href="#_bundlejs"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    如果对 webpack 的构建不熟悉，可以先看看 <a href="https://www.zfanw.com/blog/webpack-tutorial.html">我写的 webpack 教程</a>。这里跳过安装 webpack、babel 等步骤。
  </p>
  
  <p>
    上面说到的 app.js 是服务端的入口文件，前端上同样需要一个入口，且把它叫 client.js：
  </p>
  
  <pre><code>import Home from './components/Home'
import ReactDOM from 'react-dom'
import React from 'react'
ReactDOM.render(&lt;Home /&gt;, document.getElementById('root'))
</code></pre>
  
  <p>
    另外，我们再定义一个 webpack.config.js 文件：
  </p>
  
  <pre><code>var path = require('path')
module.exports = {
  entry: './src/client',
  output: {
    filename: 'bundle.js',
    path: path.join(__dirname, 'public')
  },
  module: {
    loaders: [
      {test: /\.js$/,
        loaders: ['babel?presets[]=react,presets[]=es2015'],
        include: [path.join(__dirname, 'src')]
      }
    ]
  }
}
</code></pre>
  
  <p>
    在项目根目录下执行 <code>webpack</code>，我们就会得到 <code>public/bundle.js</code>，刷新我们的主页，点击 div 就能看到文字的颜色在改变了。
  </p>
  
  <p>
    就这样，我们完成了一趟轻松、简单的 react.js 服务端渲染之旅。
  </p>
  
  <p>
    如果对完整的代码有兴趣，请点击 <a href="https://github.com/chenxsan/react-server-render">github 上的 react-server-render 仓库</a>，还可以点击<a href="https://www.zfanw.com/react/server-render/">示例</a>查看最终效果。
  </p>
</div>