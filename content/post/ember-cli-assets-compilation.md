---
title: ember-cli 静态资源压缩
author: 陈 三
layout: post
date: 2015-04-20T14:22:08+00:00
url: /ember-cli-assets-compilation.html
views:
  - 731
categories:
  - 前端开发
tags:
  - ember.js

---
ember-cli 文档中的 [assets compilation 一节中][1]提到静态资源如 CSS/JS 等的混淆压缩，让我们在 Brocfile.js 文件中加如下代码：

    minifyCSS: {
      enabled: false
    },
    minifyJS: {
      enabled: false
    }
    

语焉不详，我第一回看见，不知道这段代码究竟往哪里加。

当然，我们可以看 ember-app.js 文件的代码注释：

    
    /**
      EmberApp is the main class Ember CLI uses to manage the Brocolli trees
      for your application. It is very tightly integrated with Brocolli and has
      an `toTree()` method you can use to get the entire tree for your application.
    
      Available init options:
        - es3Safe, defaults to `true`,
        - storeConfigInMeta, defaults to `true`,
        - autoRun, defaults to `true`,
        - outputPaths, defaults to `{}`,
        - minifyCSS, defaults to `{enabled: !!isProduction,options: { relativeTo: 'app/styles' }},
        - minifyJS, defaults to `{enabled: !!isProduction},
        - loader, defaults to this.bowerDirectory + '/loader.js/loader.js',
        - sourcemaps, defaults to `{}`,
        - trees, defaults to `{},`
        - jshintrc, defaults to `{},`
        - vendorFiles, defaults to `{}`
    
      @class EmberApp
      @constructor
      @param {Object} options Configuration options
    */
    

打开 Brocfile.js 文件，默认有一行：

    var app = new EmberApp();
    

我们给 `new EmberApp` 传递参数即可：

    var app = new EmberApp({
      minifyCSS: {
        enabled: true
      },
      minifyJS: {
        enabled: false
      }
    });

 [1]: http://www.ember-cli.com/#asset-compilation