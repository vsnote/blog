---
title: Google 查询的 URL 参数
author: 陈 三
layout: post
date: 2012-12-06T05:37:23+00:00
url: /google-search-url-parameters.html
views:
  - 1927
dsq_thread_id:
  - 960575428
categories:
  - 未分类
tags:
  - Google

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 设定输入输出编码</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 限定显示结果数目</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-3"><span class="toc_number toc_depth_1">3</span> 限定网站地理位置</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_Google"><span class="toc_number toc_depth_1">4</span> 限定 Google 界面语言</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-4"><span class="toc_number toc_depth_1">5</span> 限定语言</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-5"><span class="toc_number toc_depth_1">6</span> 限定时间</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#URL"><span class="toc_number toc_depth_1">7</span> URL 参数作用说明表</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-6"><span class="toc_number toc_depth_1">8</span> 扩展阅读</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    在 Google 搜索里，有许多高级的<strong>「搜索设置」</strong>，比如屏蔽不需要的结果(Blocking unwanted results)，开/关 Google 即搜即得联想功能(Google Instant predictions)，设置「每页搜索结果数」等。
  </p>
  
  <p>
    同时，这些设置也可以通过修改 Google 查询的 <strong>URL 参数</strong>来完成，并且灵活性比上述的「搜索设置」更高。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">设定输入输出编码</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    先来看一个最简单的 Google 查询 URL:
  </p>
  
  <pre><code>https://www.google.com/search?q=vimperator&ie=utf-8&oe=utf-8  
</code></pre>
  
  <p>
    这个 URL 的意思是在 Google 中搜索 &#8220;vimperator&#8221;，且输入编码(ie &#8211; input encoding)为 utf-8，输出编码(oe &#8211; output encoding)也为 utf-8。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">限定显示结果数目</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    一般来说，搜索引擎在一页里显示10个结果，Google 里这个数目可以通过「搜索设置」调整为10、20、30、40、50、100，但我们也可以通过 URL 参数来做更多的调整。
  </p>
  
  <p>
    仍举上面那个 URL 为例：
  </p>
  
  <pre><code>https://www.google.com/search?q=vimperator&ie=utf-8&oe=utf-8&num=100
</code></pre>
  
  <p>
    URL 末尾添加的 &#8220;<strong>num=100</strong>&#8221; 表示在 Google 在搜索结果页里每一页显示100个结果。这个数字取值范围为1-100，并且需要关闭 「Google 即搜即得联想功能」，如果打开的话，则只能显示10个，因为即搜即得联想功能需要耗费较多的资源。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-3">限定网站地理位置</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-3" href="#i-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    如果你熟悉 vimperator，大概会知道 vimperator 很多内容都是日语 &#8211; 因为有维护者是岛国人民，vimperator 插件的开发者也多是岛国人民。但如果在 Google 以 &#8220;vimperator&#8221; 为关键词进行搜索，查找出来的结果多是英文，如何限定日语？也许可以考虑打开 Google.co.jp 网站，但仍能找到大量的英文。
  </p>
  
  <p>
    这时我们可以通过 &#8220;<strong>restrict=countryJP</strong>&#8221; 来限定搜索结果里仅显示服务器地理位置处于日本的站点：
  </p>
  
  <pre><code>https://www.google.com/search?q=vimperator&ie=utf-8&oe=utf-8&restrict=countryJP
</code></pre>
  
  <p>
    从概率上说，寄放在日本国内的网站很可能是日语站点。这样，我们就离我们的目的更进一步了。
  </p>
  
  <p>
    另外，与 <code>restrict=country..</code> 相近的有 <code>gl=country..</code> 和 <code>cr=country..</code>，详见扩展阅读2。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Google">限定 Google 界面语言</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Google" href="#_Google"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    上一个链接访问的页面里，Google 的菜单等显示的仍是英文，如果也想把它换成日文，则可以如下：
  </p>
  
  <pre><code>https://www.google.com/search?q=vimperator&ie=utf-8&oe=utf-8&restrict=countryJP&hl=ja
</code></pre>
  
  <p>
    参数 <code>hl</code>(注意是小写的 L，而不是数字1)用于修改 Google 界面语言，简体中文是 <code>zh-cn</code>，台湾正体是 <code>zh-tw</code>，香港繁体则是 <code>zh-hk</code>。当然，这些从左往右阅读的语言可能感觉不到大变化，请加个 <code>hl=iw</code>，希伯来语界面，你就可以看到整个 Google 界面的变化非常大。更多语言代码请见扩展阅读1。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-4">限定语言</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-4" href="#i-4"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    在使用 &#8220;restrict=countryJP&#8221; 时说到一个问题，该参数是通过服务器地址来过滤搜索结果的，但是也有可能其他语言的网站寄存在日本的服务器上。则还有个参数 <code>lr=lang_ja</code> 来限定搜索结果语言为日语。更多语言代码仍是参考扩展阅读1。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-5">限定时间</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-5" href="#i-5"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Google 的搜索工具里提供限定时间(一般是指页面发布的时间)的功能，比如「过去1小时」，「过去24小时」，「过去1周」，甚至是自定义某一段日期。这些功能也可以通过 URL 参数 <code>as_qdr=..</code> (as 表示 Advanced search)完成。
  </p>
  
  <p>
    比如 <code>as_qdr=m2</code> 表示过去两个月，<code>as_qdr=y2</code> 表示过去两年，<code>as_qdr=d2</code> 表示过去两天，<code>as_qdr=s3</code> 表示过去3秒内，<code>w</code> 表示一周，<code>s</code> 表示秒，<code>n</code> 表示分钟，<code>h</code> 表示小时。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="URL">URL 参数作用说明表</span><a title="标题链接地址" class="u-floatRight hidden" id="heyURL" href="#URL"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    最末，列个表格说明：
  </p>
  
  <table>
    <tr>
      <th>
        URL 参数
      </th>
      
      <th>
        取值
      </th>
      
      <th>
        作用
      </th>
    </tr>
    
    <tr>
      <td>
        ie
      </td>
      
      <td>
        utf-8&#8230;
      </td>
      
      <td>
        输入编码
      </td>
    </tr>
    
    <tr>
      <td>
        oe
      </td>
      
      <td>
        utf-8&#8230;
      </td>
      
      <td>
        输出编码
      </td>
    </tr>
    
    <tr>
      <td>
        num
      </td>
      
      <td>
        1-100
      </td>
      
      <td>
        限定一页内显示的数目
      </td>
    </tr>
    
    <tr>
      <td>
        restrict
      </td>
      
      <td>
        countryXX
      </td>
      
      <td>
        限定服务器地理
      </td>
    </tr>
    
    <tr>
      <td>
        hl
      </td>
      
      <td>
        en,zh-cn&#8230;
      </td>
      
      <td>
        设置界面语言
      </td>
    </tr>
    
    <tr>
      <td>
        lr
      </td>
      
      <td>
        lang_en&#8230;
      </td>
      
      <td>
        限定结果语言
      </td>
    </tr>
    
    <tr>
      <td>
        as_qdr
      </td>
      
      <td>
        s3,n2,h1,d3,w3,m3,y3&#8230;
      </td>
      
      <td>
        限定网页发布时间
      </td>
    </tr>
    
    <tr>
      <td>
        safe
      </td>
      
      <td>
        on,off
      </td>
      
      <td>
        开/关 safe search
      </td>
    </tr>
    
    <tr>
      <td>
        &#8230;
      </td>
      
      <td>
        &#8230;
      </td>
      
      <td>
        &#8230;
      </td>
    </tr>
  </table>
  
  <p>
    更多 URL 参数可以参考文末链接。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-6">扩展阅读</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-6" href="#i-6"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <a href="https://sites.google.com/site/tomihasa/google-language-codes">Google 语言代码</a>
    </li>
    <li>
      <a href="http://www.blueglass.com/blog/google-search-url-parameters-query-string-anatomy/">Google Search URL Parameters – Query String Anatomy</a>
    </li>
    <li>
      <a href="http://www.rankpanel.com/blog/google-search-parameters/">Google search parameters in 2012</a>
    </li>
  </ol>
</div>