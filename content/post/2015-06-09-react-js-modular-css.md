---
title: 模块化 React.js CSS
author: 陈 三
layout: post
date: 2015-06-09T09:22:51+00:00
excerpt: 根据 BEM 的建议模块化 react.js 的 CSS，并使用 JSPM 打包、合并 CSS，绕过 react.js 内联样式带来的问题。
url: /react-js-modular-css.html
views:
  - 2090
categories:
  - 前端开发
tags:
  - css
  - jspm
  - react.js

---
[React.js][1] 的法国开发者 Christopher Chedeau [分享过一期 react css in js][2]，里面罗列他们如何解决 CSS 中的七个难题：

  1. CSS 天然的全局命名空间导致的命名冲突
  2. 依赖
  3. 无用代码清理
  4. 命名压缩，比如 `.button` -> `.ifd`
  5. 共享规则
  6. 不确定的解析
  7. 代码分离

React 最后解决这些问题的方法是用 JavaScript 写 CSS 规则，并[内联样式][3]。

但内联样式一样存在问题：

  1. `:hover`、`:active` 这些伪类无法使用
  2. 媒体查询无法使用
  3. 样式代码也会出现大量重复

诚然我们有[各种][4] [workarounds][5] 解决伪类、媒体查询等问题，但我有些担心它们的可用性、可维护性 &#8211; 说到底，它们只是 workaround。

还是回到 CSS 命名约定上。

Google 工程师 [Philip Walton][6] 一直推荐 BEM，因为 BEM 可以很好地解决我们的 CSS 模块化问题，在 BEM 的定义里，我们可以把模块样式写在[以模块名命名的 CSS 文件][7]中，注意，我们的操作系统不允许同一目录下存在同名 CSS 文件，于是我们就巧妙地绕过了 CSS 命名冲突的问题 &#8211; 我承认，项目庞大的话，后面可能出现「行者孙、孙行者、者行孙」这样的奇怪命名。把 BEM 的这个思路应用到 React 上，则我们解决了模块化问题，也不会碰上 React 内联样式里伪类、媒体查询无法使用的问题。

但是，如果把 CSS 文件分散到各个 CSS 文件中，我们就会碰上合并、打包 CSS 的问题。不过 BEM 是成套的，我们最常说及的只是它的命名约定，围绕命名约定，它还提供[整套的工具][8]。又或者，如果你跟我一样，也在使用 [jspm][9]，则它已经可以解决 CSS 的合并、打包问题。

比如我的一个业余项目，样式表结构如下：

[resp_image id=&#8217;16505&#8242; caption=&#8221; ]

在执行 `jspm bundle-sfx script/app --minify` 命令后，所有 CSS 文件就被打包到一个 build.css 中了。

当然，使用命名规范并不能解决前面罗列的全部问题。技术常常是一种取舍，世间并没有银子弹。

<div class='timeline'>
  <h2>
    修订历史
  </h2>
  
  <ol>
    <li>
      <span itemprop='dateModified'>2015.06.10 今天恰巧看到一篇<a href="http://keithjgrant.com/posts/against-css-in-js.html" title="打开文章链接">反对 React 的 CSS 用法的文章</a></li> </ol> </div>

 [1]: http://facebook.github.io/react/ "react.js 官网"
 [2]: https://speakerdeck.com/vjeux/react-css-in-js "演示稿"
 [3]: https://facebook.github.io/react/tips/inline-styles.html "react 官网的样式文档"
 [4]: http://projects.formidablelabs.com/radium/ "radium 用法"
 [5]: https://github.com/js-next/react-style "react-style 库"
 [6]: http://philipwalton.com/ "Philip Walton 个人站点"
 [7]: https://en.bem.info/method/filesystem/ "BEM 中文件系统的使用"
 [8]: https://en.bem.info/tools/bem/bem-tools/
 [9]: http://www.zfanw.com/blog/tag/jspm "本博客 jspm 相关内容"