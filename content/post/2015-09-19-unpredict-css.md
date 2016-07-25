---
title: 失控的 CSS
author: 陈 三
layout: post
date: 2015-09-19T01:36:05+00:00
excerpt: 从全局 CSS 到模块化 CSS
url: /unpredict-css.html
views:
  - 703
categories:
  - 前端开发
tags:
  - css

---
我觉得很多人对 CSS 太过轻视，以至于完全不知道，全局 CSS 的危险。

举个例子，A 君在 CSS 中加了一个规则如下：

    strong { font-weight: 700; font-size: 17px; }
    

B 君别有一个 strong，想扩展这个样式，于是，B 君可能这样写：

    .widget strong { color: red; }
    

C 君可能也有个模块类名叫 `.widget`，里面恰恰有个 strong 也想用这个样式，既然别人写好了，就用它吧。

时间过了半个月，D 君接手这个项目，他想重构下 CSS 代码，

  1. 他不敢动 `strong` 样式，因为他不知道，动了会发生什么
  2. 他不敢动 `.widget strong`，原因同上

全局的 CSS，没人敢删，唯一敢让人拍胸脯的，只能是不断地提高 [css specificity][1]，于是规则越来越多，也越来越长。

再后来，A 君改了 `strong` 的样式，B 君的样式坏了，C 君的也一样。

我们的 CSS 规则，变得神秘莫测。

## 解药

许多人觉得，SASS/SCSS、LESS、Stylus 这类 CSS 预处理器能解决全局 CSS 冲突问题，但是，只要它们生成的 css 类名还是 .xx-xx-xx 这样，上面提及的问题就只能减少，无法消灭，而况， CSS 预处理器本来是在解决 CSS 复用、继承等问题，至于迁移或减小了 CSS 样式冲突的风险，更像是意外所得。

同样的问题，在 JavaScript 领域同样遭遇。

一开始，大家都把变量名写在顶级作用域中：

    function a () {}
    function b () {}
    function c () {}
    

但名称总是有限，冲突注定会出现，于是大家开始加命名空间：

    var com = {}
    var com.utils = {}
    var com.utils.a = function () {}
    var com.utils.b = function () {}
    var com.utils.c = function () {}
    

当然，这么写非常累人，于是又有各种变体。

再之后我们有 [CommonJS][2] 尝试定义 JavaScript 模块，但它更多是针对服务器端，于是又出现了 [AMD][3]，专门针对浏览器环境，并且有各种辅助工具如 RequireJS 等。

再后来，我们就迎来了 [ES6(ES2005) 模块][4]。

回顾 JavaScript 的模块化进程，我们就会发现，CSS 的模块化还停留在命名空间的阶段，哪怕是 [BEM][5] 这类命名约定。所以 JavaScript 在那个阶段会碰上的问题，CSS 一样会碰上，Sass 等预处理器，最多，只是让 CSS 拥有了 JavaScript 的那些可复用、可继承的特性罢了，并没有解决 CSS 真正模块化的问题。

那么既然 JavaScript 已经走到 es6 模块化的阶段，CSS 为什么不能利用它的好处呢？这就是 [css modules][6] 所尝试的。

它确切地[解决了 CSS 命名冲突的问题][7]，让 CSS 同样变得可以预测。这样，你想删除某段模块化 CSS 代码时，可以放心删除，不用害怕可能破坏别人的样式。

**一段可以放心删除的 CSS**，我觉得这应该列入写 CSS 的标准。

 [1]: https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity
 [2]: http://wiki.commonjs.org/wiki/CommonJS
 [3]: http://requirejs.org/docs/whyamd.html
 [4]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import
 [5]: https://en.bem.info/method/naming-convention/
 [6]: https://github.com/css-modules/css-modules
 [7]: http://glenmaddern.com/articles/css-modules