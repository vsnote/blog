---
title: 面试一个前端开发者
author: 陈 三
layout: post
date: 2014-01-04T07:47:38+00:00
url: /interviewing-a-front-end-developer.html
views:
  - 1083
categories:
  - 前端开发
tags:
  - 前端开发
  - 面试

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 第一部分：对象原型</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 第二部分：参数</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-3"><span class="toc_number toc_depth_1">3</span> 第三部分：上下文</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-4"><span class="toc_number toc_depth_1">4</span> 第四部分：遮罩库</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-5"><span class="toc_number toc_depth_1">5</span> 其他想法</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    声明：This post is translated from <a href="http://blog.sourcing.io/interview-questions">Alex MacCaw&#8217;s interesting sharing</a>, thank him for allowing my translating and blogging here.
  </p>
  
  <p>
    我在 Twitter、Stripe 的一部分工作包括面试前端工程师候选人。关于怎样面试，我们有很大的自由，我也因此开发出些不一样的问题集，颇有意思，所以我想分享下。
  </p>
  
  <p>
    在继续前，我想声明一下，招聘是件极度困难的事，要在45分钟内就决定某个人是产上合适同样是艰巨的任务。面试的问题在于，每个人都努力要被雇佣。任何一个通过我面试的人，可能跟我一样，想得很多，而这不见得是件好事。因此，迄今为止我的决定多少都有碰运气的成分。不过，我相信这个方法是个好的开始。
  </p>
  
  <p>
    最理想的，当然是候选人有一个非常完整的 <strong>GitHub</strong><fnref target="11191.a" /> 简历，那么我们就可以一同回顾下他们的开源项目。我通常会浏览他们的代码，围绕一些设计决策，问他们问题。如果他们表现突出，那么面试就会更多地考核他们是否能跟团队良好协作。否则，我会继续问代码问题。
  </p>
  
  <p>
    我的面试是非常实际的，全都关于代码。我不问抽象的、算法的问题 &#8211; 其他面试官如果愿意，可以选择问这些，不过我认为这些问题跟前端编程的关联性是存疑的。我的问题看起来可能很简单，不过每个集合都有所针对，考察 JavaScript 知识的某一特定方面。
  </p>
  
  <p>
    不需要白板。如果候选人带笔记本电脑，他们可以用自己的。否则他们可以用我的。他们可以使用他们喜欢的任何编辑器，通常我会在 Chrome 浏览器的控制台里直接测试他们的程序输出的结果。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">第一部分：对象原型</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    我们先从简单的开始。我让候选人定义一个 <code>spacify</code> 函数，函数接收一个字符串参数，然后返回一样的字符串，只是两个字符间均插入一个空格。例如：
  </p>
  
  <pre><code>spacify('hello world')//=&gt;'h e l l o  w o r l d'
</code></pre>
  
  <p>
    这个问题看起来可能非常简单，但后面你会发现，这是个不错的开始，尤其对那些只是通过电话面试、不曾考察的候选人来说 &#8211; 有些人声称了解 JavaScript，但实际上连个函数怎么写都不知道。
  </p>
  
  <p>
    正确答案如下。有些时候，候选人会用 <code>for</code> 循环，也是个可接受的答案。
  </p>
  
  <pre><code>function spacify(str) {
  return str.split('').join(' ');
}
</code></pre>
  
  <p>
    紧接的一个问题，是让候选人将 <code>spacify</code> 函数直接应用到 <code>String</code> 对象，比如：
  </p>
  
  <pre><code>'hello world'.spacify();
</code></pre>
  
  <p>
    问这个问题，能让我了解候选人对函数原型的基本掌握情况。通常，这会引向一个有趣的讨论，就是直接在原型上定义属性，尤其是 <code>Object</code> 上定义属性时带来的影响。最后的结果看起来如下：
  </p>
  
  <pre><code>String.prototype.spacify = function(){
  return this.split('').join(' ');
};
</code></pre>
  
  <p>
    这时，我一般还会让候选人解释函数表达式与函数声明的区别。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">第二部分：参数</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    接下来，我会问一些简单问题，专门考察他们对 <code>arguments</code> 对象的理解程度。我会先运行一个尚未定义的 <code>log</code> 函数。
  </p>
  
  <pre><code>log('hello world')
</code></pre>
  
  <p>
    然后让他们定义一个 <code>log</code> 函数，它会把字符串参数委托给 <code>console.log()</code>。正确答案就差不多是后面几行这样，不过聪明的候选人会跳过直接应用 <code>apply</code>。
  </p>
  
  <pre><code>function log(msg){
  console.log(msg);
}
</code></pre>
  
  <p>
    等函数定义好了，我会更改调用 <code>log</code> 的方式，传入多个参数。我会说清楚，我希望 <code>log</code> 能接收不定数量的参数，而不仅仅两个。我也会提示一个情况：<code>console.log</code> 能接收多个参数。
  </p>
  
  <pre><code>log('hello','world');
</code></pre>
  
  <p>
    但愿你的候选人会直接用上 <code>apply</code>。有时他们会绊倒在 <code>apply</code> 跟 <code>call</code> 的区别上，那你可以提示一下正确的方向。传递 <code>console</code> 上下文也是非常重要的。
  </p>
  
  <pre><code>function log(){
  console.log.apply(console,arguments);
};
</code></pre>
  
  <p>
    接着我会要求他们在每个记录信息前加上 <code>"(app)"</code>，比如：
  </p>
  
  <pre><code>'(app) hello world'
</code></pre>
  
  <p>
    就在这里，事情变得有些棘手。不错点的候选人知道 <code>arguments</code> 是伪数组，要想操作它，我们需要事先将其转化为标准数组。这种情况一般是用 <code>Array.prototype.slice</code>，如下所示：
  </p>
  
  <pre><code>function log(){
  var args = Array.prototype.slice.call(arguments);
  args.unshift('(app)');

  console.log.apply(console,args);
};
</code></pre>
  
  <h2 class="storycontent-h2">
    <span id="i-3">第三部分：上下文</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-3" href="#i-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    接下来的一系列问题，是考察候选人对 JavaScript 上下文和 <code>this</code> 的掌握。我首先定义如下例子。注意 <code>count</code> 属性是从当前上下文取出的。
  </p>
  
  <pre><code>var User = {
  count: 1,

  getCount: function(){
    return this.count;
  }
};
</code></pre>
  
  <p>
    然后我再定义以下几行，之后我问候选人 log 输出结果会是什么。
  </p>
  
  <pre><code>console.log(User.getCount());

var func = User.getCount;
console.log(func());
</code></pre>
  
  <p>
    在这个案例中，正确答案是 <code>1</code> 和 <code>undefined</code>。你可能会感到惊讶，因为有很多人栽在类似这种的基础上下文问题。<code>func</code> 在 <code>window</code> 环境中执行，因此丢失 <code>count</code> 属性。我会解释给他们，然后问他们如何保证 <code>func</code> 的上下文总是绑定给 <code>User</code>，这样它总是会正确返回 <code>1</code>。
  </p>
  
  <p>
    正确答案是使用 <code>Function.prototype.bind</code>，比如：
  </p>
  
  <pre><code>var func = User.getCount.bind(User);
console.log(func());
</code></pre>
  
  <p>
    我一般还会解释说这个函数在旧浏览器中还没有提供，让他们写个垫片函数。弱一点的候选人多数要苦苦挣扎，不过要求你雇用的人全面理解 <code>apply</code> 和 <code>call</code> 是非常重要的。
  </p>
  
  <pre><code>Function.prototype.bind = Function.prototype.bind || function(context){
  var self = this;

  return function(){
    return self.apply(context, arguments);
  };
}
</code></pre>
  
  <p>
    如果候选人只在浏览器原生 <code>bind</code> 不存在时才垫片，可以额外加分。到此为止，如果他们表现都非常不错，我会要求他们柯里化参数<fnref target="11191.b" />。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-4">第四部分：遮罩库</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-4" href="#i-4"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    面试的最后，我会让候选人构建一些实际的东西，通常是一个遮罩库。我发现这很有用，因为它展示了整个前端层：HTML，CSS，和 JavaScript。如果面试的前面部分他们表现非常不错，我就会尽可能快的切入这个问题。
  </p>
  
  <p>
    具体怎么做取决于他们，不过有一些关键东西需要我们留意：
  </p>
  
  <p>
    在创建遮罩时，使用 <code>position:fixed</code> 要比 <code>position:absolute</code> 好，因为它保证遮罩覆盖整个窗口，不论窗口是否滚动。如果候选人没注意到，我会提出来，然后问他们 <code>fixed</code> 与 <code>absolute</code> 定位的区别。
  </p>
  
  <pre><code>.overlay {
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  top: 0;
  background: rgba(0,0,0,.8);
}
</code></pre>
  
  <p>
    他们怎样居中遮罩内容也能说明问题。有些人可能会用 CSS 和绝对定位 &#8211; 内容的宽、高固定的情况下这是可行的。其他人可能会用 JavaScript 来定位。
  </p>
  
  <pre><code>.overlay article {
  position: absolute;
  left: 50%;
  top: 50%;
  margin: -200px 0 0 -200px;
  width: 400px;
  height: 400px;
}
</code></pre>
  
  <p>
    我还会要求他们做到，遮罩被点击时要关闭，这可以切入讨论不同类型事件的传播。经常地，候选人会直接在遮罩上绑定一个单击事件监听器，然后调用它。
  </p>
  
  <pre><code>$('.overlay').clock(closeOverlay);
</code></pre>
  
  <p>
    这可行，但你随后会意识到，遮罩子元素的单击事件同样关闭了遮罩 &#8211; 这显然不是我们想要的。解决办法是检查事件对象，确保事件不会传播，如下：
  </p>
  
  <pre><code>$('.overlay').click(function(e){
  if (e.target == e.currentTarget)
    closeOverlay();
});
</code></pre>
  
  <h2 class="storycontent-h2">
    <span id="i-5">其他想法</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-5" href="#i-5"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    当然，这些问题只覆盖了前端知识的一小部分，你还可以问很多其他方面，比如性能，HTML5 APIs，AMD vs CommonJS 模块，构造器，类型和盒模式。我通常会根据面试者的兴趣，混合使用不同主题的问题。
  </p>
  
  <p>
    我还建议看看前端开发面试问题库<fnref target="11191.1" />找想法，或者 JavaScript 花园<fnref target="11191.2" />列举的任何 JavaScript 行为。
  </p>
  
  <footnotes>
    <fn name="11191.a">
      <p>
        <a href="https://github.com/">Github</a>
      </p>
    </fn>
    
    <fn name="11191.b">
      <p>
        <a href="http://en.wikipedia.org/wiki/Currying">Wikipedia Currying</a>
      </p>
    </fn>
    
    <fn name="11191.1">
      <p>
        <a href="https://github.com/darcyclarke/Front-end-Developer-Interview-Questions">Front-end Developer Interview Questions</a>
      </p>
    </fn>
    
    <fn name="11191.2">
      <p>
        <a href="http://bonsaiden.github.io/JavaScript-Garden">JavaScript Garden</a>
      </p>
    </fn>
  </footnotes>
</div>