---
title: MVC 的概念
author: 陈 三
layout: post
date: 2013-01-17T07:50:40+00:00
url: /what-is-mvc.html
views:
  - 694
dsq_thread_id:
  - 1030708637
categories:
  - 未分类
tags:
  - MVC

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_MVC"><span class="toc_number toc_depth_1">1</span> 为什么有 MVC</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_sprintf_Smarty_MVC"><span class="toc_number toc_depth_1">2</span> 由 sprintf 与 Smarty 说到 MVC</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#MVC"><span class="toc_number toc_depth_1">3</span> MVC 框架的案例</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    刚开始，MVC 的概念给我这编程经历不多的人的感觉是，无从下口。
  </p>
  
  <p>
    就像面向对象概念。
  </p>
  
  <p>
    前些天看到一篇讲<a href="http://www.aqee.net/you-wanted-a-banana-but-you-got-a-gorilla-holding-the-banana/">面向对象的</a>，说我们本来只是想要香蕉，结果得到的却是一只猩猩拿着香蕉。
  </p>
  
  <p>
    我觉得挺有意思，对我这种函数式编程经历远多于面向对象的人来说，面向对象需要经验，不到某个境界，马上就上手，就颇有种造猩猩的感觉。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_MVC">为什么有 MVC</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_MVC" href="#_MVC"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    MVC 的概念也一样。
  </p>
  
  <p>
    为什么要把程序分成三个部分？
  </p>
  
  <p>
    理由当然有不少，比如 MVC 设计模式(Design Pattern)有利于后期维护，程序灵动性强，等等等等。
  </p>
  
  <p>
    但这种话就好像教育小孩子说，你一定要怎样怎样，不然会怎样怎样。他们没有情境，并无法领会这种东西。我为了弄清楚 MVC 的概念，看了大量的相关内容，但结果呢？还是不知所谓。
  </p>
  
  <p>
    Wikipedia 上 <a href="https://en.wikipedia.org/wiki/Model–view–controller">MVC 的词条</a>配了张图，倒让我有点直观感受(<em>注：图片来自 Wikipedia</em>)：
  </p>
  
  <p>
    <img src="https://upload.wikimedia.org/wikipedia/commons/f/fd/MVC-Process.png" alt="model-view-controller" />
  </p>
  
  <p>
    但也只是到此为止。再看再多的内容，也不会有助于我理解这个概念。我只好说，光看手册，不下水，是永远无法学会游泳的。
  </p>
  
  <p>
    于是找了个 PHP 的 MVC 框架操作。PHP 的基于 MVC 设计模式的框架不少，我用的是 <a href="http://ellislab.com/codeigniter/">CodeIgniter</a>，原因是以前曾经糊里糊涂地用它做过一个站点。
  </p>
  
  <p>
    再结合点 <a href="http://www.smarty.net/">Smarty 模板引擎</a>与 <a href="http://www.zfanw.com/blog/php-mysql-query-sprintf.html">PHP 的 sprintf() 函数</a>，MVC 的概念就渐渐清晰了。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_sprintf_Smarty_MVC">由 sprintf 与 Smarty 说到 MVC</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_sprintf_Smarty_MVC" href="#_sprintf_Smarty_MVC"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    来看个 <a href="http://www.zfanw.com/blog/php-mysql-query-sprintf.html">PHP 中构建查询语句</a> 中所举的例子：
  </p>
  
  <blockquote>
    <pre><code>$sql = "SELECT * FROM `SAM` WHERE Reason ='" . $_POST['why'] . "' AND WHERE Time = '". $_POST['when'] . "'";
</code></pre>
  </blockquote>
  
  <p>
    类似上面的查询语句，如果我们的 PHP 页面是由 PHP 语言混合 HTML 语言进行构造的，可以想像，它很乱，让人写过一次后就不想再动它。
  </p>
  
  <p>
    然而，上述查询语句可以通过 sprintf() 函数来改进：
  </p>
  
  <blockquote>
    <pre><code>$sql = sprintf("SELECT * FROM `SAM` WHERE Reason = '%s' AND WHERE Time = '%s'",%_POST['why'],%_POST['when'];
</code></pre>
  </blockquote>
  
  <p>
    我们先构建 <code>SELECT * FROM &lt;code>SAM</code> WHERE Reason = '%s' AND WHERE Time = '%s'</code> 这个字符串，并且用两个 <code>%s</code> 来暂时占位，然后传入两个变量，做相应的替代。
  </p>
  
  <p>
    这样做的好处是，我们清楚的知道第一个字符串说明的是什么，并且将变量从中分离，如果要做修改，无论改变量还是改字符串，都是件很方便的事。
  </p>
  
  <p>
    同理，Smarty 模板引擎，先构建一个模板文件，比如，index.tpl：
  </p>
  
  <pre><code>&lt;html&gt;
&lt;head&gt;
&lt;title&gt;{$title}&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
</code></pre>
  
  <p>
    在这个过程中，我们并不管 title 标签对中包含的是什么，我们只要知道，它个变量就行，就像 sprintf 函数里的 <code>%s</code> 那样，占好位置先。
  </p>
  
  <p>
    有变量给我们在模板中占好位置后，我们就需要往模板中传入变量的值，那才是真正要展现给最终用户看的内容：
  </p>
  
  <pre><code>&lt;?php
require_once('Smarty.class.php');
$smarty = new Smarty();
$smarty-&gt;assign('title','Hello world!');
$smarty-&gt;display('index.tpl');
?&gt;
</code></pre>
  
  <p>
    在这里，Smarty 将变量 $title 的值通过 <code>$smarty-&gt;assign('title','Hello world!')</code> 传入。跟 sprintf 函数的思路很接近。
  </p>
  
  <p>
    也就是这样，我们完成了一个分离，即 <strong>View 与 Controller 的分离</strong>，在上面所举的例子中，View 可以理解为 Smarty 模板 index.tpl 或 sprintf 的第一个参数字符串。
  </p>
  
  <p>
    在上面的例子中可以看到，我所传入的变量值都是随手拿来的，现成的，并没有通过数据库取得。当这些变量值存在「存取」状态，与数据库需要来往时，我们就又能从上面的 「Controller」 概念中分离出 「Model」 &#8211; 即数据哪儿来，怎么来，怎么去。所以，上面所说的 <strong>View 与 Controller 的分离</strong> 中，Controller 其实是个伪 Controller，我们还可以从中分离出 Model。
  </p>
  
  <p>
    以 Smarty 模板来阐释 MVC 概念，则 index.tpl 负责 View，Controller 负责将数据指定给变量，它相当于程序中的粘合剂，Model 则负责数据哪儿来。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="MVC">MVC 框架的案例</span><a title="标题链接地址" class="u-floatRight hidden" id="heyMVC" href="#MVC"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    再来看 <a href="http://ellislab.com/codeigniter/user-guide/tutorial/create_news_items.html">CodeIgniter 的一段教程</a>，可以加深上面的概念(注：以下代码均来自 CodeIgniter 网站，未作修改)，
  </p>
  
  <h3>
    view 部分
  </h3>
  
  <pre><code>&lt;h2&gt;Create a news item&lt;/h2&gt;

&lt;?php echo validation_errors(); ?&gt;

&lt;?php echo form_open('news/create') ?&gt;

    &lt;label for="title"&gt;Title&lt;/label&gt; 
    &lt;input type="input" name="title" /&gt;&lt;br /&gt;

    &lt;label for="text"&gt;Text&lt;/label&gt;
    &lt;textarea name="text"&gt;&lt;/textarea&gt;&lt;br /&gt;

    &lt;input type="submit" name="submit" value="Create news item" /&gt; 

&lt;/form&gt;
</code></pre>
  
  <h3>
    Model 部分
  </h3>
  
  <pre><code>public function set_news()
{
    $this-&gt;load-&gt;helper('url');

    $slug = url_title($this-&gt;input-&gt;post('title'), 'dash', TRUE);

    $data = array(
        'title' =&gt; $this-&gt;input-&gt;post('title'),
        'slug' =&gt; $slug,
        'text' =&gt; $this-&gt;input-&gt;post('text')
    );

    return $this-&gt;db-&gt;insert('news', $data);
}
</code></pre>
  
  <h3>
    Controller 部分
  </h3>
  
  <pre><code>public function create()
{
    $this-&gt;load-&gt;helper('form');
    $this-&gt;load-&gt;library('form_validation');

    $data['title'] = 'Create a news item';

    $this-&gt;form_validation-&gt;set_rules('title', 'Title', 'required');
    $this-&gt;form_validation-&gt;set_rules('text', 'text', 'required');

    if ($this-&gt;form_validation-&gt;run() === FALSE)
    {
        $this-&gt;load-&gt;view('templates/header', $data);   
        $this-&gt;load-&gt;view('news/create');
        $this-&gt;load-&gt;view('templates/footer');

    }
    else
    {
        $this-&gt;news_model-&gt;set_news();
        $this-&gt;load-&gt;view('news/success');
    }
}
</code></pre>
  
  <p>
    具体的代码作用且不说，从上面三段代码中，可以看到，View 部分基本只负责页面的展示，它显示一个表单，用于创建新条目；而 Model 部分也只是将新生成的数据插入到数据库；至于 Controller 部分，就负责得比较多：如果表单检测不通过，则调用 View 部分($this->load->view&#8230;)，返回原页面；如果表单检测通过，则调用 Model 部分($this->news_model->set_news()) 把数据插入到数据库中，并且显示($this->load->view(&#8216;news/success&#8217;)) 成功信息。
  </p>
  
  <p>
    你可能觉得 Controller 部分做的事有点多，实际上也有人说 MVC 的设计模式中 Controller 部分堆入了太多内容，而建议 <a href="http://cirw.in/blog/time-to-move-on">MOVE</a> 的设计模式。但那已经是另一个境地。
  </p>
</div>