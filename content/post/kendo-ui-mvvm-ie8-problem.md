---
title: Kendo UI MVVM模板在IE8下渲染问题
author: 陈 三
layout: post
date: 2014-06-25T14:22:20+00:00
url: /kendo-ui-mvvm-ie8-problem.html
views:
  - 764
categories:
  - 前端开发
tags:
  - kendo UI

---
根据Kendo UI的文档声明[^12995.1]，它支持IE7+。

但我在IE8下使用它的MVVM[^12995.2]时，却发现数据绑定后渲染不完整。Firefox、Google Chrome下均正常。

代码大概如下：

    <div id="example" data-template="category-template" data-bind="source: blog"></div>
    
    <script id="category-template" type="text/x-kendo-template"><!--分类模板-->
      <div>
        <h2 data-bind="text: category"></h2>
        <div data-bind="source: posts" data-template="post-template"></div>
      </div>
    </script>
    
    <script id="post-template" type="text/x-kendo-template">
      <div>
        <h2 data-bind="text: title"></h2>
        <div data-bind="text: content"></div>
      </div>
    </script>
    
    <script type="text/javascript">
    var viewModel = kendo.observable({ 
      blog: [ 
        { category: "随便说说", posts: [{"title": "陈三的博客", "content": "这是一个长草的地方"}, {"title": "夏日来临", "content": "要去哪里吗"}] }, 
        { category: "前端开发", posts: [{"title": "JavaScript闭包", "content": "闭包是什么意思"}, {"title": "夏日来临", "content": "要去哪里吗"}]}
         ]
        });
        kendo.bind($("#example"), viewModel);
    </script>
    
    

渲染的结果可以见[jsbin链接][1]。

对比图如下：

[<img src="http://www.zfanw.com/blog/wp-content/uploads/2014/06/firefox-ie8-kendo-ui.png" alt="kendo ui under firefox and ie8" width="400" height="500" class="alignnone size-full wp-image-13000" srcset="https://www.zfanw.com/blog/wp-content/uploads/2014/06/firefox-ie8-kendo-ui.png 400w, https://www.zfanw.com/blog/wp-content/uploads/2014/06/firefox-ie8-kendo-ui-240x300.png 240w, https://www.zfanw.com/blog/wp-content/uploads/2014/06/firefox-ie8-kendo-ui-80x100.png 80w" sizes="(max-width: 400px) 100vw, 400px" />][2]

IE8下，渲染不完整，某些数据不见了。

最后找出的原因是代码中的注释：

    <!--分类模板-->
    

因为我把它写在Kendo的自定义script标签里，于是IE8下就出问题，移出去后就恢复正常。这是一个非常细微却又让人觉得非常坑爹的问题。

[^12995.1]:    
    [Technical Requirements for using Kendo UI JavaScript framework][3]

[^12995.2]:    
    [Kendo UI MVVM pattern, integrated with Kendo UI jQuery-powered framework][4]

 [1]: http://jsbin.com/qiyiwo/1/
 [2]: http://www.zfanw.com/blog/wp-content/uploads/2014/06/firefox-ie8-kendo-ui.png
 [3]: http://docs.telerik.com/kendo-ui/getting-started/technical-requirements
 [4]: http://docs.telerik.com/kendo-ui/getting-started/framework/mvvm/overview