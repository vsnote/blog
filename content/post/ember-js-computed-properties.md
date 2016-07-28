---
title: Ember.js 计算的属性
author: 陈 三
layout: post
date: 2014-03-14T23:57:59+00:00
url: /ember-js-computed-properties.html
views:
  - 580
categories:
  - 前端开发
tags:
  - ember.js

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 计算的属性</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 宏指令</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#Handlebars"><span class="toc_number toc_depth_1">3</span> Handlebars 助手</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    <i>Note：本文基于 Ember.js 1.4.0</i>
  </p>
  
  <p>
    在 Ember.js 里，模型对象的属性多数很简洁，可以把它理解为数据库里的字段。比如一个定义 person 对象<fnref target="11865.1" />的类：
  </p>
  
  <pre><code>App.Person = Ember.Object.extend({
  id: null,
  firstName: null,
  lastName: null,
  age: null,
  gender: null
});
</code></pre>
  
  <p>
    在 handlebars 模板里使用：
  </p>
  
  <pre><code>我的名字叫{{firstName}}{{lastName}}，{{gender}}性，今年{{age}}岁。
</code></pre>
  
  <p>
    假定我还想根据 age 的值来划分「幼年」、「少年」、「青年」、「壮年」、「老年」又如何？
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">计算的属性</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Ember.js 提供的<strong>计算的属性</strong>可以很方便地解决这种问题，只需要给 Person 类增加一个属性 &#8211; 区别是，这个属性不是静态的，而是动态的一个函数，函数中返回值：
  </p>
  
  <pre><code>App.Person = Ember.Object.extend({
  id: null,
  firstName: null,
  lastName: null,
  age: null,
  gender: null,
  ageClass: function() { // &lt;- 这就是我们要定义的计算属性，在函数体中可以做逻辑判断
    var age = this.get('age');
    switch (true) {
      case age &gt; 0 && age &lt; 6:
        return '幼年';
        break;
      case age &gt;= 6 && age &lt; 18:
        return '少年';
        break;
      case age &gt;= 18 && age &lt; 30:
        return '青年';
        break;
      case age &gt;= 30 && age &lt; 60:
        return '壮年';
        break;
      case age &gt;= 60:
        return '老年';
        break;
  }.property('age') // &lt;- 这个是计算的属性与普通属性的一个区别
});
</code></pre>
  
  <p>
    注意函数后紧跟着的 <code>property</code>，它声明该计算的属性依赖其他属性。age 值如果有变化，它的值会自动更新。
  </p>
  
  <p>
    创建对象实例时，我们不需要给计算的属性传参数，
  </p>
  
  <pre><code>App.Person.create({
  id: 1,
  firstName: '三',
  lastName: '陈',
  age: 18,
  gender: '男'
});
</code></pre>
  
  <p>
    Ember.js 会自动生成 <code>ageClass</code>，可直接在前端模板上使用：
  </p>
  
  <pre><code>我的名字叫{{firstName}}{{lastName}}，{{gender}}性，今年{{age}}岁，据称还属于{{ageClass}}。
</code></pre>
  
  <p>
    渲染后的内容为：
  </p>
  
  <blockquote>
    <p>
      我的名字叫三陈，男性，今年18岁，据称还属于青年。
    </p>
  </blockquote>
  
  <h2 class="storycontent-h2">
    <span id="i-2">宏指令</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    除开上面的用法，Ember.js 还提供宏<fnref target="11865.3" />指令<fnref target="11865.4" />，用于一些简单的真假判断，以及复杂的过滤(filter)、映射(map)等。
  </p>
  
  <p>
    仍以上面的模型为例子，比如我要在前端显示所有年纪小于25的人，第一感觉模板代码是这样写的：
  </p>
  
  <pre><code>{{#if age &lt; 25}}
...
{{/if}}
</code></pre>
  
  <p>
    但这是错的，Handlebars.js 不允许在 if 里做逻辑判断。我们可以考虑增加一个计算的属性，但这次是由计算的属性宏指令来构成函数体的：
  </p>
  
  <pre><code>App.Person = Ember.Object.extend({
  id: null,
  firstName: null,
  lastName: null,
  age: null,
  gender: null,
  isYoung: Ember.computed.lt('age', 25) // &lt;- 如果 age 小于25则 isYoung 值为 true
});
</code></pre>
  
  <p>
    然后模板这样写：
  </p>
  
  <pre><code>{{#if isYoung}}
...
{{/if}}
</code></pre>
  
  <p>
    在我们使用宏指令时，并不需要添加 <code>property()</code> 这样的方法，代码会更干净，更清楚。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="Handlebars">Handlebars 助手</span><a title="标题链接地址" class="u-floatRight hidden" id="heyHandlebars" href="#Handlebars"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    类似的问题，除了以上两种方法，我们还可以用 Handlebars 助手<fnref target="11865.2" />，
  </p>
  
  <pre><code>Ember.Handlebars.helper('isYoung', function(age) { // 定义模板助手
  return age &lt; 25 ? true : false;
});
</code></pre>
  
  <p>
    然后模板文件里这样写：
  </p>
  
  <pre><code>{{#if isYoung age}}
...
{{/if}}
</code></pre>
  
  <footnotes>
    <fn name="11865.1">
      <p>
        <a href="http://www.zfanw.com/blog/ember-js-model-without-ember-data.html">Ember.js 不用 Ember Data 如何创建模型</a>
      </p>
    </fn>
    
    <fn name="11865.3">
      <p>
        <a href="http://eviltrout.com/2013/07/07/computed-property-macros.html">Computed Property Macros &#8211; Evil Trout&#8217;s Blog</a>
      </p>
    </fn>
    
    <fn name="11865.4">
      <p>
        <a href="http://emberjs.com/api/classes/Ember.html">请查看 api 中 computed. 开头的方法</a>
      </p>
    </fn>
    
    <fn name="11865.2">
      <p>
        <a href="http://emberjs.com/guides/templates/writing-helpers/">Ember.js &#8211; Templates: Writing Helpers</a>
      </p>
    </fn>
  </footnotes>
</div>