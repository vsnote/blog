---
title: Ember.js 里 model 与 content 属性的区别
author: 陈 三
layout: post
date: 2014-04-08T22:37:43+00:00
excerpt: Ember.js 路由中为什么存在 content 与 model 两种设置控制器的方法，它们有什么区别。
url: /ember-js-difference-between-model-and-content.html
views:
  - 529
categories:
  - 前端开发
tags:
  - ember.js

---
_Note：本文基于 Ember.js 1.4.0_

Ember.js 里，路由(route)通过 **setupController** 方法设置控制器(controller)属性：

    App.ApplicationRoute = Ember.Route.extend({
      model: function() {
        return {'user': '陈三', 'blog': 'http://www.zfanw.com/blog/'};
      },
      setupController: function(controller, model) {
        controller.set('model', model); // <- 这里，我们把 model 内容指派给控制器的 model 属性
      }
    });
    

前端模板里，可以直接引用对象的属性：

    <script type="text/x-handlebars">
      用户{{user}}的博客地址是{{blog}}
    </script>
    

页面的渲染结果为[^12159.1]：

> 用户陈三的博客地址是http://www.zfanw.com/blog/

但如果用 Ember.js Inspector [^12159.2]检查 ApplicationController 的属性，如下图：

<img src="http://www.zfanw.com/blog/wp-content/uploads/2014/04/emberjs-inspector-result.png" alt="ember.js 检查器" width="477" height="144" class="alignnone size-full wp-image-12169" srcset="https://www.zfanw.com/blog/wp-content/uploads/2014/04/emberjs-inspector-result.png 477w, https://www.zfanw.com/blog/wp-content/uploads/2014/04/emberjs-inspector-result-300x90.png 300w, https://www.zfanw.com/blog/wp-content/uploads/2014/04/emberjs-inspector-result-150x45.png 150w, https://www.zfanw.com/blog/wp-content/uploads/2014/04/emberjs-inspector-result-100x30.png 100w" sizes="(max-width: 477px) 100vw, 477px" />

我们并没有看到一个叫 `model` 的属性，相反，有一个 `content` 的属性包含着我们指派给 `model` 的内容。

如果在 setupController 里把 `model` 换成 `content` 如何？

    App.ApplicationRoute = Ember.Route.extend({
      model: function() {
        return {'user': '陈三', 'blog': 'http://www.zfanw.com/blog/'};
      },
      setupController: function(controller, model) {
        controller.set('content', model); // <- 这回，我们把 model 内容指派给控制器的 content 属性
      }
    });
    

实践证明，`content` 与 `model` 属性是等效的。

更准确的说，`model` 只是 `content` 通过 `Ember.computed.alias` [^12159.3]设置的一个别名[^12159.4]：

> model: Ember.computed.alias(&#8216;content&#8217;),

至于为什么要设置这样一个别名，可以看 Github 上的一个讨论[^12159.5]。

[^12159.1]:    
    [本篇代码的 demo][1]

[^12159.2]:    
    [ember 检查器][2]

[^12159.3]:    
    [Ember.computed.alias 方法][3]

[^12159.4]:    
    [ember.js 控制器源代码][4]

[^12159.5]:    
    [The way we set a controller&#8217;s content and model is a bit baroque · Issue #2007 · emberjs/ember.js][5]

 [1]: http://jsbin.com/poxaw
 [2]: https://github.com/emberjs/ember-inspector
 [3]: http://emberjs.com/api/#method_computed_alias
 [4]: https://github.com/emberjs/ember.js/blob/d60c6c059bfb4ccf69d4a2eb98563ef2519d5f60/packages/ember-runtime/lib/controllers/controller.js#L63
 [5]: https://github.com/emberjs/ember.js/issues/2007