---
title: Ember.js 不用 Ember Data 如何创建模型
author: 陈 三
layout: post
date: 2014-03-13T13:26:32+00:00
url: /ember-js-model-without-ember-data.html
views:
  - 558
categories:
  - 前端开发
tags:
  - ember.js

---
_Note：本文基于 Ember.js 1.4.0_

Ember.js 的文档中，Model(模型)部分[^11824.1]赫然是围绕 Ember Data [^11824.2]写的。这就让人产生一个疑问，如果不用 Ember Data 会怎样？毕竟我可能出于以下各种理由拒绝使用它：

  1. 不喜欢它
  2. 它还不稳定
  3. 后端开发的 RESTful [^11824.3]API 风格不够正，Ember Data 不适用
  4. 其他

当然，不用它并不会怎样，因为我们还有许多轻量的替代品[^11824.4]，要是这些也都不喜欢，我们还可以手写 [^11824.5]ajax 来创建 Ember.js 的模型部分[^11824.6]。

    window.App = Ember.Application.create(); // 创建 App 实例
    
    App.Router.map(function() {
      this.route('person');
    });
    
    App.Model = Ember.Object.extend({}); // 定义一个 Model 类，所有 Model 都继承自它
    
    App.Person = App.Model.extend({
      firstName: null,
      lastName: null,
      age: null,
      gender: null
    }); // 定义一个 Person 类
    
    // 假定取得所有 person 的 api 接口为 http://www.zfanw.com/api/person.php
    // 返回的数据结构是 {"people": [{"firstName": "Sam", "lastName": "Chen", "age": 18, "gender": "male"},{"firstName": "Jane", "lastName": "White", "age": 18, "gender": "female"}]}
    

接下来用 reopenClass [^11824.7]给 Person 类增加一个方法，这个方法用于返回所有的 Person 实例：

    App.Person.reopenClass({ 
      findAll: function() {
        return $.get('http://www.zfanw.com/api/person.php').then(
          function(response) {
            return response.people.map(function(person) { // map 是 JavaScript 的方法
              return App.Person.create(person);
            });
          }
        );
      }
    });
    

这样，在 Route 里我们就可以设置 Model 了：

    App.PersonRoute = Ember.Route.extend({
      model: function() {
        return App.Person.findAll();
      },
      setupController: function(controller, model) {
        controller.set('model', model);
        // 也可以写成 controller.set('content', model)
      }
    });
    

之后可以在 Handlebars.js 模板里使用模型数据了[^11824.8]：

    <table class=table>
    <thead>
      <tr>
        <th>姓名</th>
        <th>年龄</th>
        <th>性别</th>
      </tr>
    </thead>
    <tbody>
    {{#each}}
      <tr>
        <td>{{firstName}} {{lastName}}</td>
        <td>{{age}}</td>
        <td>{{gender}}</td>
      </tr>
    {{/each}}
    </tbody>
    </table>
    

[^11824.1]:    
    [Ember.js &#8211; Models: Introduction][1]

[^11824.2]:    
    [emberjs/data][2]

[^11824.3]:    
    [Representational state transfer &#8211; Wikipedia, the free encyclopedia][3]

[^11824.4]:    
    [Alternatives to Ember Data][4]

[^11824.5]:    
    [Ember without Ember Data &#8211; Evil Trout&#8217;s Blog][5]

[^11824.6]:    
    [Getting Started with Ember.js | Tom Brandt][6]

[^11824.7]:    
    [Ember.js &#8211; The Object Model: Reopening Classes and Instances][7]

[^11824.8]:    
    [本文代码在 Jsbin 上的 Demo][8]

 [1]: http://emberjs.com/guides/models/
 [2]: https://github.com/emberjs/data
 [3]: http://en.wikipedia.org/wiki/Representational_state_transfer
 [4]: http://blog.emberwatch.com/2013/06/19/alternatives-ember-data.html
 [5]: http://eviltrout.com/2013/03/23/ember-without-data.html
 [6]: http://twbrandt.github.io/2013/02/11/Ember-Quick_Start_Guide/
 [7]: http://emberjs.com/guides/object-model/reopening-classes-and-instances/
 [8]: http://jsbin.com/karopaxe/1