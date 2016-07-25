---
title: JSONP
author: 陈 三
layout: post
date: 2013-11-20T14:05:25+00:00
url: /jsonp.html
views:
  - 737
categories:
  - 前端开发
tags:
  - jsonp

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#JSONP"><span class="toc_number toc_depth_1">1</span> JSONP的由来</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#JSONP-2"><span class="toc_number toc_depth_1">2</span> JSONP的概念</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#jQueryJSONP"><span class="toc_number toc_depth_1">3</span> jQuery与JSONP</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">4</span> 参考</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    Ajax 请求如果返回JSON数据，我们可以用<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse">JSON.parse</a>析出，又或者用jQuery提供的<a href="http://api.jquery.com/jQuery.parseJSON/">parseJSON</a>。这个概念很容易理解。但名称与它接近的JSONP概念却有些复杂。起码，情况要比返回JSON数据复杂、难理解些。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="JSONP">JSONP的由来</span><a title="标题链接地址" class="u-floatRight hidden" id="heyJSONP" href="#JSONP"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    之所以会有JSONP出现，是因为浏览器的<a href="http://www.zfanw.com/blog/javascript-same-origin-policy.html">同源策略限制</a> &#8211; 我们无法跨域请求数据。但我们又有跨域请求数据的需求，那么我们就需要一个变通方法。既然JavaScript脚本不受同源策略的限制，于是它就被应用到跨域请求数据的实践中。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="JSONP-2">JSONP的概念</span><a title="标题链接地址" class="u-floatRight hidden" id="heyJSONP-2" href="#JSONP-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    JSONP的全文是JSON with padding，表示一串JSON数据用函数名称包装起来。
  </p>
  
  <p>
    举个例子：
  </p>
  
  <pre><code>{"firstName":"Sam","lastName":"Chen","gender":"male"}
</code></pre>
  
  <p>
    上面是一串JSON数据，假设它放在github.com/chenxsan域上的human.json文件里，因为它与我的博客不同源，所以我并无法从我的博客发Ajax请求，要求github说返回该文件然后解析。但我可以把该数据包装在一个JavaScript函数里，保存为human.js文件：
  </p>
  
  <pre><code>human({"firstName":"Sam","lastName":"Chen","gender":"male"});
</code></pre>
  
  <p>
    这其实就是一个函数传入一个对象并执行的代码。
  </p>
  
  <p>
    而我在我博客页面可预先定义一个同名函数：
  </p>
  
  <pre><code>function human(data) {
    console.log(data.firstName + data.lastName + "is" + data.gender);
}
</code></pre>
  
  <p>
    之后在博客页面通过script标签动态调用github.com域上的human.js文件，这就类似于在页面插入如下语句：
  </p>
  
  <pre><code>&lt;script src = "https://raw.github.com/chenxsan/blog/master/human.js"&gt;&lt;/script&gt;
</code></pre>
  
  <p>
    这样，通过在博客页面上定义函数，并且调用不同域上的JS传入数据执行了函数，我得到JSON数据 &#8211; 查看浏览器的控制台信息，我可以看到字符串&#8217;Sam Chen is male&#8217;。
  </p>
  
  <p>
    上面的说明中，包含JSON数据的文件是保存为human.js的，实际上，src并不介意它是什么文件格式，我甚至可以把它保存为.html或者其他格式，照样可以用，没有影响。在实际应用中，服务器端语言可以自由定义请求的URL &#8211; 前端页面只关心服务器端能不能返回相应格式的数据。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="jQueryJSONP">jQuery与JSONP</span><a title="标题链接地址" class="u-floatRight hidden" id="heyjQueryJSONP" href="#jQueryJSONP"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    jQuery中，JSONP的实现与上面描述的差别不大。jQuery通过在URL附加<code>?callback=?</code>这样的参数提交请求给服务器(参数名称是客户端和服务器共同协定的，不必要叫callback，比如接下来的例子中，回调名用的是jsoncallback。
  </p>
  
  <p>
    例子：
  </p>
  
  <pre><code>$.getJSON('http://api.flickr.com/services/feeds/photos_public.gne?tags=cat&tagmode=any&format=json&jsoncallback=?',function(data){
    console.log(data.title);
    console.log(typeof data);
});
</code></pre>
  
  <p>
    demo如下，请按console中的run按钮：
  </p>
  
  <p>
    <a class="jsbin-embed" href="http://jsbin.com/aceGoruq/2/embed?js,console">测试JSONP</a>
  </p>
  
  <p>
    用浏览器开发者工具查看请求的URL：
  </p>
  
  <p>
    <a href="http://www.zfanw.com/blog/wp-content/uploads/2013/11/jsonp-flickr.png"><img src="http://www.zfanw.com/blog/wp-content/uploads/2013/11/jsonp-flickr.png" alt="jsonp 请求 flickr 数据" width="617" height="343" class="alignnone size-full wp-image-11007" srcset="https://www.zfanw.com/blog/wp-content/uploads/2013/11/jsonp-flickr.png 617w, https://www.zfanw.com/blog/wp-content/uploads/2013/11/jsonp-flickr-300x166.png 300w" sizes="(max-width: 617px) 100vw, 617px" /></a>
  </p>
  
  <p>
    我们能看到，我们请求的URL地址中最后一个问号被替换成<code>jQuery20206085280561819673_1384954063431&_=1384954063432</code>。这是jQuery处理的结果，不需要我们打理。
  </p>
  
  <p>
    HTTP 返回的数据则是下面这样：
  </p>
  
  <blockquote>
    <p>
      jQuery20206085280561819673_1384954063431&_=1384954063432({&#8230;&#8230;});
    </p>
  </blockquote>
  
  <p>
    还有些情况下，需要特定的回调名称，则可以设置 <code>jsonpCallback</code>：
  </p>
  
  <pre><code>$.ajax({
    url: 'http://api.flickr.com/services/feeds/photos_public.gne?tags=cat&tagmode=any&format=json&jsoncallback=?', 
    dataType: "jsonp",
    jsonpCallback: "_preloadCallback",
    success: function(data) {
        alert(data.title);
    }
});
</code></pre>
  
  <p>
    既然有了定义好的回调函数，又有了远程取回的带数据的执行函数，我们就得到不同域的JSON数据。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">参考</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <a href="http://www.ibm.com/developerworks/cn/web/wa-aj-jsonp1/">使用 JSONP 实现跨域通信</a>
    </li>
    <li>
      <a href="http://www.flickr.com/services/feeds/docs/photos_public/">flickr 公開的 Feed</a>
    </li>
  </ol>
</div>