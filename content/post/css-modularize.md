---
title: 模块化 CSS
author: 陈 三
layout: post
date: 2015-06-01T22:52:24+00:00
excerpt: 怎样模块化 CSS，减小全局样式的不良影响
url: /css-modularize.html
views:
  - 1310
categories:
  - 前端开发
tags:
  - css

---
CSS 是失控的。

我们无妨把 CSS 想象成一头野马，我们所有的 CSS 命名规范上的尝试，无论是 [SUITCSS][1] 还是 [BEM][2]、[SMACSS][3] 或是[其它][4]，都是打算给 CSS 套上缰绳，但我们只是往正确的方向走了一小步。命名规范只是一种约定，如果开发者有意或无意地忽视，哪怕只是代码中的一小部分，也会给以后埋下问题。

所以我们可以看到，在 JavaScript 模块化非常成熟、各类工具齐全的今天，前端界开始往 CSS 模块化方向努力。

我最早了解到的这方面努力是 [ember-component-css][5]，比如 `app/my-component/styles.css` 文件内容如下：

    & {
      padding: 2px;
    }
    .urgent {
      color: red;
    }
    

构建后的 CSS 如下：

    .my-component-a34fba {
      padding: 2px;
    }
    .my-component-a34fba .urgent {
      color: red;
    }
    

构建后的 CSS 作用域不再是全局，而是限定在**这个**组件中，我们把 CSS 关进模块化的笼子。我们不用担心它的作用会渗透到其他代码，我们现在对我们的代码作用范围非常有信心 &#8211; 它现在更像是狙击枪，而不是手榴弹。

接下来，我在用 [JSPM][6] 时也看到[模块化 CSS 的努力][7]。

然后是 webpack 的 [CSS Module mode][8]，开发这块功能的这位甚至宣布了[全局 CSS 的终结][9]。

从上面的简单介绍中可以看到，CSS 的模块化依赖于特定工具，比如 ember-cli、webpack、jspm，如果我们不用这类工具的话，就基本无法对 CSS 做模块化，这样移植性似乎差了点，而且因为没有标准规范，所以它们的实施也不尽相同。可是这年头，不用这类工具辅助的代码，恐怕代码在可维护性、可扩展方面都会很糟糕吧。

 [1]: https://suitcss.github.io/
 [2]: https://en.bem.info/
 [3]: https://smacss.com/
 [4]: http://www.zfanw.com/blog/css-worst-practice-complex-tag-selectors.html
 [5]: https://github.com/ebryn/ember-component-css
 [6]: http://www.zfanw.com/blog/jspm-systemjs.html
 [7]: https://github.com/systemjs/plugin-css/issues/30
 [8]: https://github.com/webpack/css-loader/#module-mode
 [9]: https://medium.com/seek-ui-engineering/the-end-of-global-css-90d2a4a06284