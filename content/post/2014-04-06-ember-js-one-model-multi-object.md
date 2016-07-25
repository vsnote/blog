---
title: Ember.js 一个模型包含多种对象
author: 陈 三
layout: post
date: 2014-04-06T04:44:09+00:00
excerpt: Ember.js 里如何给一个模型添加多种对象。
url: /ember-js-one-model-multi-object.html
views:
  - 597
categories:
  - 前端开发
tags:
  - ember.js

---
_Note：本文基于 Ember.js 1.4.0_

如果看 Ember.js 教程[^12105.1]，可以发现，一个路由对应的模型里，对象是只有一种的，比如这样[^12105.2]：

    App.PersonRoute = Ember.Route.extend({
      model: function() {
        return App.Person.findAll();
      },
      setupController: function(controller, model) {
        controller.set('model', model);
      }
    });
    

应该说，这是 Ember.js 框架适用的情景。

但某些情况下，你希望 model 不仅仅是一种对象，而是多种对象集合，则可以有两种选择：

  1. 放弃 Ember.js，因为它已经不太适用这种较传统的页面
  2. 已经用了 Ember.js，骑虎难下

项目做到一半结果要放弃整个框架，只能说前期对 Ember.js 的适用情形了解不足。但走到这一步，要砍掉重来却不现实。

Ember.js 提供有 **Ember.RSVP.hash** 方法[^12105.3]，用法如下：

    App.PersonRoute = Ember.Route.extend({
      model: function() {
        return Ember.RSVP.hash({ // 这里 model 对象包含两种子对象 allPerson 与 task
          allPerson: App.Person.findAll(),
          task: $.get('http://www.zfanw.com/api/task')
        });
      },
      setupController: function(controller, model) {
        controller.set('model', model);
      }
    });
    

模板里使用调用 `model.allPerson` 与 `model.task` 即可。

[^12105.1]:    
    [Ember.js &#8211; Guides and Tutorials: Ember.js Guides][1]

[^12105.2]:    
    [Ember.js 不用 Ember Data 如何创建模型][2]

[^12105.3]:    
    [Ember.js &#8211; Ember.RSVP][3]

 [1]: http://emberjs.com/guides/
 [2]: http://www.zfanw.com/blog/ember-js-model-without-ember-data.html
 [3]: http://emberjs.com/api/classes/Ember.RSVP.html#method_hash