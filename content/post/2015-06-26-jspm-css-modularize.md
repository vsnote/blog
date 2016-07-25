---
title: JSPM 模块化 CSS
author: 陈 三
layout: post
date: 2015-06-26T12:35:17+00:00
excerpt: JSPM 的全新 CSS 加载器允许我们模块化 CSS
url: /jspm-css-modularize.html
views:
  - 1243
categories:
  - 前端开发
tags:
  - css
  - jspm

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_jspm-loader-css"><span class="toc_number toc_depth_1">1</span> 安装 jspm-loader-css</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_CSS"><span class="toc_number toc_depth_1">2</span> 模块 CSS 规则</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_CSS-2"><span class="toc_number toc_depth_1">3</span> 使用 CSS 模块</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    之前我写过两篇模块化 CSS 的内容：
  </p>
  
  <ol>
    <li>
      <a href="http://www.zfanw.com/blog/css-modularize.html" title="模块化 CSS">当下前端界在模块化 CSS 上的种种尝试</a>
    </li>
    <li>
      <a href="http://www.zfanw.com/blog/react-js-modular-css.html" title="react.js 模块化 css">React.js 中内联 CSS 的问题</a>
    </li>
  </ol>
  
  <p>
    其中提到 <a href="https://github.com/systemjs/plugin-css/issues/30" title="github systemjs plugin-css">jspm 在模块化 CSS 上的尝试</a>。
  </p>
  
  <p>
    现在，jspm 贡献者已经完成<a href="https://github.com/geelen/jspm-loader-css">这一功能</a>，只待整合进 jspm。
  </p>
  
  <p>
    来看看，jspm 里，要怎么使用这个功能。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_jspm-loader-css">安装 jspm-loader-css</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_jspm-loader-css" href="#_jspm-loader-css"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    在命令行下运行命令：
  </p>
  
  <pre><code>jspm install css=npm:jspm-loader-css
</code></pre>
  
  <p>
    jspm 默认使用的 CSS 加载器是 <a href="https://github.com/systemjs/plugin-css">plugin-css</a>，上一条命令让 jspm-loader-css 取代 plugin-css，安装完成后，config.js 文件中 <code>System.config</code> 里的 <code>map</code> 下 <code>css</code> 条目变成：
  </p>
  
  <pre><code>"css": "npm:jspm-loader-css@0.1.4"
</code></pre>
  
  <h2 class="storycontent-h2">
    <span id="_CSS">模块 CSS 规则</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_CSS" href="#_CSS"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    假设模块保存在 Components/book 目录下，
  </p>
  
  <pre><code>- Components
  - book
    + book.js
    + book.css
</code></pre>
  
  <p>
    在 book.css 文件中，我们这样定义 CSS 模块：
  </p>
  
  <pre><code>:local(.book) { color: red; }
</code></pre>
  
  <p>
    <code>:local()</code> 指定该样式类为局域样式。
  </p>
  
  <p>
    当然，旧的写法仍然支持：
  </p>
  
  <pre><code>.test { color: red; }
</code></pre>
  
  <p>
    这条规则表示 <code>.test</code> 在全局环境中均可以使用。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_CSS-2">使用 CSS 模块</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_CSS-2" href="#_CSS-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    在 book.js 文件中：
  </p>
  
  <pre><code>import styles from './book.css!css';
import React from 'react';

export default class extends React.Component {
    render() {
        return (
            &lt;li className={styles.book}&gt;

            &lt;/li&gt;
            );
    }
};
</code></pre>
  
  <p>
    这是一个 React.js 项目文件。
  </p>
  
  <p>
    查看生成的页面，生成的 <code>li</code> 的 class 类名是 <code>_Components_book_book__book</code>。
  </p>
  
  <p>
    如果嫌 CSS 中总写 <code>:local</code> 麻烦，则可以使用另一个 CSS 加载器 <a href="https://github.com/geelen/jspm-loader-css-modules">jspm-loader-css-module</a>，这个加载器默认所有的 CSS 类名是局域的，而非全局，使用它就不需要写 <code>:local</code>。
  </p>
  
  <p>
    <strong>最值得提及的一点是</strong>，jspm-loader-css 默认启用 autoprefixer，实际上，因为 jspm-loader-css 依赖 <a href="https://github.com/css-modules/css-modules-loader-core">css-modules/css-modules-loader-core</a>，而后者又是基于 <a href="https://github.com/postcss/postcss" title="postcss 库">postcss</a>，所以 postcss 的插件，我们都可以使用，<a href="https://github.com/geelen/jspm-loader-css#customize-your-own-loader" title="jspm-loader-css 配置 postcss 插件">具体用法见文档说明</a>。
  </p>
</div>