---
title: Markdown 语法怎么写 HTML 表格
author: 陈 三
layout: post
date: 2013-07-02T16:50:38+00:00
url: /markdown-and-table.html
dsq_thread_id:
  - 1459438223
views:
  - 5101
categories:
  - 未分类

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#PHP_Extra_Markdown"><span class="toc_number toc_depth_1">1</span> PHP Extra Markdown</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#Pandoc"><span class="toc_number toc_depth_1">2</span> Pandoc</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    首先，Markdown <a href="http://daringfireball.net/projects/markdown/syntax">官方</a> 并没有提供语法来写 HTML 表格，我们只能写 HTML 标签：
  </p>
  
  <pre><code>&lt;table&gt;
    &lt;tr&gt;
        &lt;td&gt;&lt;/td&gt;
    &lt;/tr&gt;
&lt;/table&gt;
</code></pre>
  
  <p>
    简洁的 Markdown 语法中插入这一堆 HTML 标签，多少有点刺眼，表格数据多的话，写起来也不方便。解决办法是使用扩展过的 Markdown 语法。就我目前所知，有以下几个实现。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="PHP_Extra_Markdown">PHP Extra Markdown</span><a title="标题链接地址" class="u-floatRight hidden" id="heyPHP_Extra_Markdown" href="#PHP_Extra_Markdown"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    这是一个 PHP 版本的 Markdown 实现（implement），我博客后台就安装了这个插件，它支持<a href="http://michelf.ca/projects/php-markdown/extra/#table">Markdown 表格的书写</a>，格式如下：
  </p>
  
  <pre><code>你好|Markdown|表格
---|---|---
我|不是|人
</code></pre>
  
  <p>
    转换后的 HTML 代码如下：
  </p>
  
  <pre><code>&lt;table&gt;
&lt;thead&gt;
&lt;tr&gt;
  &lt;th&gt;你好&lt;/th&gt;
  &lt;th&gt;Markdown&lt;/th&gt;
  &lt;th&gt;表格&lt;/th&gt;
&lt;/tr&gt;
&lt;/thead&gt;
&lt;tbody&gt;
&lt;tr&gt;
  &lt;td&gt;我&lt;/td&gt;
  &lt;td&gt;不是&lt;/td&gt;
  &lt;td&gt;人&lt;/td&gt;
&lt;/tr&gt;
&lt;/tbody&gt;
&lt;/table&gt;
</code></pre>
  
  <p>
    浏览器输出如下：
  </p>
  
  <table>
    <tr>
      <th>
        你好
      </th>
      
      <th>
        Markdown
      </th>
      
      <th>
        表格
      </th>
    </tr>
    
    <tr>
      <td>
        我
      </td>
      
      <td>
        不是
      </td>
      
      <td>
        人
      </td>
    </tr>
  </table>
  
  <h2 class="storycontent-h2">
    <span id="Pandoc">Pandoc</span><a title="标题链接地址" class="u-floatRight hidden" id="heyPandoc" href="#Pandoc"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    <a href="http://johnmacfarlane.net/pandoc/">Pandoc</a> 用于不同文档格式间转换，它的表格语法和 PHP Markdown Extra 一样，可参见它的<a href="http://johnmacfarlane.net/pandoc/try/?text=你好|Markdown|表格%0A---|---|---%0A我|不是|人&from=markdown&to=html">在线演示</a>。
  </p>
</div>