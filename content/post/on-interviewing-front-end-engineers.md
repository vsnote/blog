---
title: 关于面试前端工程师
author: 陈 三
layout: post
date: 2014-01-01T04:44:05+00:00
url: /on-interviewing-front-end-engineers.html
views:
  - 1561
categories:
  - 前端开发
tags:
  - 前端工程师
  - 前端开发
  - 翻译
  - 面试

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 我们雇佣聪明的人</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 人力资源</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-3"><span class="toc_number toc_depth_1">3</span> 成长</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-4"><span class="toc_number toc_depth_1">4</span> 理解前端工程师</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-5"><span class="toc_number toc_depth_1">5</span> 什么是重点</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-6"><span class="toc_number toc_depth_1">6</span> 我们说给自己的谎</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-7"><span class="toc_number toc_depth_1">7</span> 结论</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    <strong>声明</strong>：本文译自 Nicholas C. Zakas 的 <a href="http://www.nczonline.net/blog/2013/12/27/on-interviewing-front-end-engineers/">On interviewing front-end engineers</a>。感谢作者的翻译许可。译文有不到之处，也欢迎指出。
  </p>
  
  <p>
    Philip Walton 上周写了篇很有意思的文章<fnref target="11171.1" />，说的是他在旧金山几家公司面试前端工程师的经历。概述一下，就是他很惊讶，被问到他的（大部分跟计算机科学概念有关）及没问到他的问题（DOM 怎么看）惊到了。我很想自己也惊讶下，不过在过去七年里，我一直住在硅谷，所以这些故事是听了无数遍。再怎么想<fnref target="11171.a" />，我都不觉得这些问题只发生在旧金山湾区内 &#8211; 我认为这是我们行业的问题，对前端工程师做什么以及创造什么价值的持续误解。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">我们雇佣聪明的人</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Google 当初崭露头角时，他们有个刻板的招聘方式。他们的想法是，尽可能招最聪明的人，这些人一旦招进来了，他们总能找出最能发挥你聪明才智的地方。这多少意味着，每个想进来的人，都会经历相似的面试，这面试试图标注一个工程师的「聪明」门槛<fnref target="11171.b" />。换句话说，不管你专长或专注的领域是什么，你的面试跟其他人基本差不多。一旦被视为「聪明」，你就被放进来了，只是还不知道你要做什么，直到你以一个真正资格的员工身份出现在校园里<fnref target="11171.c" />。
  </p>
  
  <p>
    今天的行业内，围绕前端工程师的许多糟糕的招聘实践，我认为是 Google 的做法带的坏头。在我参加 Google 的面试时，我被那些跟我专业没半点关系的问题吓到了。我还记得，有好几个情况下我都在考虑自己是不是该放弃，因为我压根不知道怎样用堆排序<fnref target="11171.d" />来准确跟踪数以亿计的请求的搜索查询时间。那不是我职业生涯中想要做的，我对计算机科学的这个领域不感兴趣；这个问题究竟能提供什么价值？
  </p>
  
  <p>
    （注意：我不知道 Google 今天是不是还在坚持类似的招聘方式。出于这篇文章的目的，我且把它称作「Google 的做法」，但我绝不在影射 Google 现在还在这样干。此外，Google 现在有，也曾经有一些世界上最优秀的前端工程师为他们工作。我绝不是说，他们在前端招聘上做得不好。）
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">人力资源</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    从实用的角度出发，并且在经历创业失败后，我理解 Google 的做法。在一个公司还小，刚起步的时候，你需要能做各种不同事情的人。你没法要求有一个前端工程师、一个后端工程师、一个数据库管理员、一个网站可靠性工程师<fnref target="11171.e" />，这太奢侈。你需要的是能做很多事的人，至于他们是否达到专家水平就无所谓了 &#8211; 他们只是需要把事情做好，然后在新任务出现时能够熟练上手。
  </p>
  
  <p>
    在这种情况下，Google 的做法非常适用。资源有限，你要明白，你的公司能接受的工程师需要具备哪些技能。最重要的一点，是考虑工程师的流转性，他们是否能在各个任务间高效切换，雇用那些能随事情主次、需求变化而随时做出调整的人。年轻的公司不要奢望专业人士。为了把工作做完，每个人都需要尽可能地什么都能干<fnref target="11171.f" />。
  </p>
  
  <p>
    好消息是，如果你只是在找全能型的工程师，只要求他们具备起码的核心技能，那么这个流程会有不错的效果。在公司还小，还在成长时，这常常是最好办法。Google 即便在壮大后，也一直在用这个方法，不过确实有针对一些专业人士对流程做些加强（在我参加他们的面试时，的确被问到一些 JavaScript 的问题）。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-3">成长</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-3" href="#i-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    我看到的成长型公司最大的问题是，他们未能调整他们的面试流程，来适应公司的成长、团队形态的变化。在你决定聘请专业人士及经验丰富的工程师时，Google 的招聘做法开始遭遇滑铁卢。万金油式的面试做法不再有效，你遇上麻烦了。对一家公司来说，这个阶段是艰难的。如果你以前从没招聘过专业人士，并且对该专业你也没有任何经验，那么你怎么能规划出一个能够准确探测你想要的技能库的面试流程呢？
  </p>
  
  <p>
    太多的公司在使用「和」的方法。首先，你要符合我们目下对每个工程师起码的核心技能的要求，然后还得有能力做专业的事情。招聘公司们相信，它们在给工程师们保留完整的神奇门槛的同时，还可以招到他们需要的专业人士。这有时确实可行，但大多数时候并不如此。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-4">理解前端工程师</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-4" href="#i-4"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    任何一家公司，如果没有相关专业的经验，那么要招聘一个专家就会非常困难。原因很明显：专家在某些事情上有他们的独到之处。他们专注于一些别人不关心的事情，并且下意识地会忽视一些别人关心的事情。大脑只能处理这么多量的数据，要想在特定主题上深入，经常需要丢弃其他一些宽泛的信息。比如，过去有一时，我可以在 Visual Basic 4.0 里做任何事情。但现在，要我写出可以运行的代码就很困难了，我得从网上找。正因为我不想在这种事情上耗费我的精力，所以我才渐渐遗忘。
  </p>
  
  <p>
    前端工程师当然是专业人士。我们关心一些别人看来十分疯狂的事情：了解各种浏览器间的差异，像素与 em 单位，PNG 与 JPEG，JavaScript APIs 兼容性，如何构建 DOM 来呈现 UI，等等。当我尝试给后端工程师解释一些我做过的很酷的事情时，他们的眼神很快变得呆滞无神。他们永远不会明白我是如何仓促地在 Internet Explorer、Firefox、Chrome 和 Safari 上测试东西，并且让它正常运行起来。他们永远不会明白为什么粗体在某些情形下看起来要比斜体好。他们永远不会明白我是怎么在浏览器里找 bug。当然，他们不必知道。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-5">什么是重点</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-5" href="#i-5"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    一直以来，都不断地有人问我，招前端工程师的话，是否需要他们知道计算机科学算法跟数据结构。我简单的回答是：不需要。我看不出，这些是人们成功成为前端工程师的必要条件。原因是大部分前端工程师每天接触的并不是这些。我用算法跟数据结构吗？有时吧，但我一般是在我需要它们的时候才去查找。这些信息在网上很容易找到，而关于这些主题，身边总是有人知道得比我更清楚。
  </p>
  
  <p>
    我对前端工程师要求的东西，跟传统计算机科学概念没有太多关系。我以前写过什么造就一个好的前端工程师<fnref target="11171.2" />和如何面试前端工程师<fnref target="11171.3" />，大体上，我现在还认同我过去在这些文章里所写的东西。我要求你热爱 web，理解 HTML，CSS 跟 JavaScript，最重要的，知道怎么组合它们来解决问题。
  </p>
  
  <p>
    总的来说，我认为面试应该设计来展示一个候选人每天要用的技能。说句好样的，我们来聊聊 O-notation（我开始我的职业7年左右才听到这么个词）或者堆排序（我第一次碰上堆排序是在我参加 Google 面试的时候）实在太简单不过，但这些是否能说明一个人能够成功干成前端工程师？绝对不能。
  </p>
  
  <p>
    对细枝末节的问题，我也不太感冒。比如，「说三个右边对齐的方法」这种问题。这些问题让我想起高中的测试，只是在测试你反刍信息的能力，而不是让你展现技能。那么你应该问些什么？想想，这个角色，日常要做些什么，然后问些近似的问题。不确定？你总是可以从公司经历过的问题中找一些出来，然后问候选人们他们会怎么处理。我想知道的是，当我给你某些特定类型的问题时，你愿意、并且能够解决它。
  </p>
  
  <p>
    我想看看你在你的领域里是怎么解决困难的，你怎样梳理问题、不兼容，在你卡壳的时候你的直觉怎样做判断，你是否能够采纳反馈并且将其纳入你的进程里。这些是人们成功的因素。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-6">我们说给自己的谎</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-6" href="#i-6"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    找出回文，计算数组总和这些问题之所以无处不在，经常是因为人们认为它们能够在评估一个候选人时提供关键的数据。关于这些问题，我们有各种美好意愿，可惜多是自欺：
  </p>
  
  <ol>
    <li>
      <p>
        <strong>我们可以洞察他们的思考过程</strong> &#8211; 胡说八道。大学计算机科学考试上才经常出现的细枝末节或随机问题，可不会让我们洞察一个人的思考过程，但情景模拟可以。扔给一个人一个问题，而这问题跟他日常工作几乎没有关系，根本就无助于我们评估他们的价值。当然，我们可以借此看到他们是如何处理他们并不擅长的情况的。如果这是你所关心的，那么请继续问这类问题。但大部分工程师要处理的是某一特定的问题空间<fnref target="11171.g" />。这才是我们的问题应该关心的地方。
      </p>
    </li>
    
    <li>
      <p>
        <strong>我们坚持每个人都要达到这个标准</strong> &#8211; 这是量丈聪明的神方法。你相信，每个人问上一些同样的问题就是给你一把放之四海而皆准的量尺。只是，这样的量尺并不存在。叫迈克尔·乔丹扔个100英里每小时的快球<fnref target="11171.h" />，并不能让你洞察他的高超技能。当然，有一些人什么事情都非常擅长，但专业人士为了成为专业人士，倾向于放手一些他们日常中不用的知识。世上没有量丈聪明的方法。
      </p>
    </li>
    
    <li>
      <p>
        <strong>目前为止，运行良好</strong> &#8211; 通常是成长中的公司的喊声。我们过去用这些问题招聪明的人，为什么不再继续？你不再继续的原因是，整个团队的情况已经变了。你现在可以雇用专家，他们在他们领域里知道的比你公司里任何人都要多。你当然可以继续使用你过去一直在用的流程来招聘相同类型的人，但要想用同样的流程招到不同类型的人，那就有点痴人说梦了。
      </p>
    </li>
  </ol>
  
  <p>
    在我的职业生涯里，这些东西我是听了一遍又一遍，烦到我看不到歇停的一天。将问题跟候选人做为职员真正要做的事情匹配起来，这才是最重要的。这才是有用信息所在之地。找不到一个单词的回文是个值得关注的小事，但它是否真正告诉你这人雇用后成功的概率呢？
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-7">结论</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-7" href="#i-7"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    在我近14年的职业生涯里，我负责招聘了很大数量的前端工程师，我可以自豪地说，我从来没有招错人。他们中有些证明只是不错，有些则是非常杰出，但没有一个是糟糕的。我是怎样做到？是的，我不关心那些他们日常里根本不会碰上的细枝末节问题，我问的都是些我的计划任务里他们未来需要处理的问题，透过这些问题，我可以看到他们的处理方式。在人们的问题空间里了解他们很重要，这对所有的专业人士来说都是一样的，而不仅限于前端工程师 &#8211; 如果我在这篇文章里说得还不够清楚的话。
  </p>
  
  <p>
    对专业人士来说，参加公司的面试也常是件令人沮丧的事。怎样让事情变好起来？提供反馈。如果你是第一个被雇用的专业人士，对招聘流程提出反馈，看看是不是可以做调整。即便你没有被录用，也可以反馈给你的招聘方，告诉他们，他们问你的这些问题，根本没有给你展示你技能的机会。
  </p>
  
  <p>
    不幸的是，仍有大量的公司使用万金油方法来招聘工程师，你不会得到一个根据你特殊技能量身定制的面试。请别搞错，招聘是艰难的，而让公司增长更是难上加难。最好的改变方法是从内部发起，所以你可以提供反馈，参与你的公司的招聘，帮助别人有个更好的面试经历。
  </p>
  
  <footnotes>
    <fn name="11171.1">
      <p>
        <a href="http://css-tricks.com/interviewing-front-end-engineer-san-francisco/">Interviewing as a Front-End Engineer in San Francisco</a>
      </p>
    </fn>
    
    <fn name="11171.a">
      <p>
        by any stretch of the imagination
      </p>
    </fn>
    
    <fn name="11171.b">
      <p>
        in an attempt to standardize the bar for &#8220;smart&#8221; as an engineer
      </p>
    </fn>
    
    <fn name="11171.c">
      <p>
        until you showed up on campus as a fully-credentialed employee
      </p>
    </fn>
    
    <fn name="11171.d">
      <p>
        <a href="http://en.wikipedia.org/wiki/Heap_sort">heap sort</a>
      </p>
    </fn>
    
    <fn name="11171.e">
      <p>
        site reliability engineer
      </p>
    </fn>
    
    <fn name="11171.f">
      <p>
        Everyone needs to be as full stack as possible to get work done
      </p>
    </fn>
    
    <fn name="11171.2">
      <p>
        <a href="http://www.nczonline.net/blog/2007/08/15/what-makes-a-good-front-end-engineer/">What makes a good front end engineer</a>
      </p>
    </fn>
    
    <fn name="11171.3">
      <p>
        <a href="http://www.nczonline.net/blog/2010/01/05/interviewing-the-front-end-engineer/">Interviewing the front end engineer</a>
      </p>
    </fn>
    
    <fn name="11171.g">
      <p>
        Most engineers will be dealing with a particular problem space
      </p>
    </fn>
    
    <fn name="11171.h">
      <p>
        fastball &#8211; 译注，指棒球
      </p>
    </fn>
  </footnotes>
</div>