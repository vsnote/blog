---
title: JavaScript 收藏网页
author: 陈 三
layout: post
date: 2013-03-03T04:21:28+00:00
url: /javascript-add-to-favorite.html
views:
  - 608
dsq_thread_id:
  - 1115139003
categories:
  - 未分类
tags:
  - JavaScript

---
很不幸，在收藏网页到浏览器书签这件事上，浏览器们的意见也不太一样。

于是照旧，要写上好几种语句进行判断，首先是一个函数：

    function add_to_favorite()
    {
        var title=document.title;
        var url=location.href;
        try{
            if ( window.sidebar && typeof( window.sidebar ) === 'object' && typeof( window.sidebar.addPanel ) === 'function'){
                window.sidebar.addPanel(title, url, '');
    //针对 firefox
            } else if ( document.all && typeof( window.external ==='object' ) ){
                window.external.AddFavorite(url, title); 
    //针对 ie
            } else {alert('浏览器不支持此功能，请按“Ctrl+D”键手工收藏页面');}
        } catch(e) {
            alert('浏览器不支持此功能，请按“Ctrl+D”键手工收藏页面');} 
    // 其他的，比如 chrome 与 safari 这些基于 webkit 内核的浏览器，包括以后的 opera
        return false;
    };
    

然后将函数绑定给相应的 HTML 事件。

另外需要注意，本地开发中，HTML 文件需要使用 WEB 服务器上的路径，比如 `localhost/xx`，如果以本地文件形式打开，则收藏代码会失效。。

## 参考

  1. [window.sidebar][1]
  2. [AddFavorite method (Internet Explorer)][2]

 [1]: https://developer.mozilla.org/en-US/docs/DOM/window.sidebar
 [2]: http://msdn.microsoft.com/en-us/library/ms535926(v=vs.85).aspx