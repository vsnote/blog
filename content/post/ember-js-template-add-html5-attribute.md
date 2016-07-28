---
title: Ember.js 模板添加 HTML5 属性
author: 陈 三
layout: post
date: 2014-02-27T14:25:59+00:00
url: /ember-js-template-add-html5-attribute.html
views:
  - 543
categories:
  - 前端开发
tags:
  - ember.js

---
_Note：本文基于 Ember.js 1.4.0_

最近开发一个 Chrome 扩展，因为基于 Chrome 浏览器，所以就放心大胆地用各种新技术，比如[^11663.1]：

    <form>
      <label for=email>邮箱：</label>
      <input type=email required=required title=请输入邮箱地址 name=email placeholder=请输入邮箱地址>
      <input type=submit>
    </form>
    

`required` [^11663.2]是 HTML5 增加的元素属性，应用于表单中 input、select、textarea 元素，表示它们是必须项，用户需要填写才能提交。如果提交空内容，浏览器就会显示原生的错误消息，比如：请填写此字段。

在 Ember.js 下，上面的 Email 输入框代码会是这样写的[^11663.3]：

    {{view Ember.TextField name='email' valueBinding='email' type='email' placeholder='请输入邮箱地址' required='required' title='请输入邮箱地址'}}
    

检查 Ember.js 生成的 HTML 代码：

    <input id="ember218" class="ember-view ember-text-field" placeholder="请输入邮箱地址" name="email" type="email">
    

可以看到，`required` 与 `title` 两个属性被抛掉，这是因为 Ember.TextField [原生支持的 HTML 属性][1]有限。但 HTML5 里，像 `data-*` 这样的属性是经常出现的，`required` 也很常见。不能因为 Ember.js 原生不支持这样的属性就不用。

Ember.js 提供了一个非常简单的 reopen 方法[^11663.4]，直接扩展 Ember.TextField 类的实例方法和实例属性：

    Ember.TextField.reopen({
      attributeBindings: ['required', 'title']
    });
    

再检查 Ember.js 生成的 HTML 代码：

    <input id="ember219" class="ember-view ember-text-field" placeholder="请输入邮箱地址" name="email" required="required" title="请输入邮箱地址" type="email">
    

已经成功地给 Ember.js 模板加入 HTML5 属性了。

[^11663.1]:    
    [demo &#8211; html5 输入框][2]

[^11663.2]:    
    [required][3]

[^11663.3]:    
    [demo &#8211; ember.js view][4]

[^11663.4]:    
    [reopen 方法][5]

 [1]: http://emberjs.com/api/classes/Ember.Handlebars.helpers.html#toc_use-as-text-field
 [2]: http://jsbin.com/teducawu
 [3]: http://www.w3.org/wiki/HTML5_form_additions#required
 [4]: http://jsbin.com/buluyoka
 [5]: http://emberjs.com/guides/object-model/reopening-classes-and-instances/