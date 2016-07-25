---
title: jspm 安装使用 Bootstrap 与 jQuery
author: 陈 三
layout: post
date: 2015-05-08T00:35:15+00:00
url: /jspm-bootstrap-jquery.html
views:
  - 1098
categories:
  - 前端开发
tags:
  - bootstrap
  - jQuery
  - jspm

---
你可能知道，bootstrap 依赖于 jQuery，并且，是依赖全局的 jQuery，即页面的 `window` 对象下应该有个 `window.jQuery` 或 `window.$` 属性。

我在上一篇 [jspm 与 SystemJS 用法][1] 中提到，jspm 默认安装 `github:components/jquery` 上定义的 jQuery<del>，这个<a href="https://github.com/components/jquery">库的维护并不及时</a>，譬如现在 jQuery 最新版本是 1.11.3 与 2.1.4，而 components/jquery 上仍是 1.11.2 与 2.1.3 版本</del>。

对于第三方库，某些版本虽然只是小更新，但也许修复的 [bug 比较要命][2]，所以我通常都喜欢用最新版本。

但如果在 jspm 里使用 npm 上的 jQuery，会导致 Bootstrap 无法加载 jQuery。

整个流程如下：

  1. 安装 npm 上的最新版本 jQuery
    
        jspm install npm:jquery
        

  2. 修改 config.js 中 bootstrap 的依赖
    
    打开 config.js，修改 bootstrap 部分如下：
    
        System.config({
          "map": {
             "jquery": "npm:jquery@2.1.4", // 这一行是 jspm install 时自动配置的
             "github:twbs/bootstrap@3.3.4": {
               "jquery": "npm:jquery@2.1.4" // 我们要改的是这一行，将 bootstrap 的 jquery 依赖指向 npm/jquery@2.1.4
              }
          }
        });
        
    
    这时，`import bootstrap from 'bootstrap'` 就会报如下的错误：
    
    [resp_image id=&#8217;16059&#8242; caption=&#8221; ]

这个错误的原因在于，Bootstrap 需要全局 `jQuery` 或 `$`，但是 jspm 从 npm 上安装的 jQuery 是 CommonJS 规范的，我们的 `window` 对象下并没有 `jQuery` 或 `$` 属性，结果就报错。

所以目前，如果要在 jspm 中用 Bootstrap，就只能用 github:components/jquery 上的 jQuery 了。

 [1]: http://www.zfanw.com/blog/jspm-systemjs.html
 [2]: http://blog.jquery.com/2015/04/28/jquery-1-11-3-and-2-1-4-released-ios-fail-safe-edition/