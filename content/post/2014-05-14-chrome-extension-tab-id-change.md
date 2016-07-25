---
title: Chrome扩展开发中的标签页id变化
author: 陈 三
layout: post
date: 2014-05-14T13:46:23+00:00
url: /chrome-extension-tab-id-change.html
views:
  - 823
categories:
  - 前端开发
tags:
  - Chrome

---
如果你认为，Chrome浏览器中，每一个标签页的id是唯一的，且打开时是不变的。那么你是对的。

但在我的开发过程中，却出现tab id发生变化的情况。

整个过程是大概这样的：

  1. background.js监控到页面上的点击事件，创建一个新标签页，并将新标签页的id值赋给一个全局变量taskTab：
    
        var taskTab;
        chrome.tabs.create({url: 'http://www.zfanw.com/blog/}, function(tab) {
        taskTab = tab.id;
        });
        

  2. 同时，在background.js里监听webNavigation的onCommitted事件，用于动态注入内容脚本：
    
        chrome.webNavigation.onCommitted.addListener(function(details) {
        if (details.tabId === taskTab) {
            chrome.tabs.executeScripts(taskTab, {file: 'example.js'}); 
        }
        });
        

在新标签页打开并注入内容脚本后，内容脚本会找出页面里的链接&#8221;http://www.zfanw.com/blog/about&#8221;，并模拟点击。

且假定新标签页页面HTML代码中还包含如下内容：

    <link rel="prerender" href="http://www.zfanw.com/blog/about">
    

prerender[^12710.1]是Chrome浏览器的一个加速访问的特性。它可以在我们访问A页面时，先在背景加载好B页面，这样我们访问B页面时，就非常神速。

摘取链接1中的一段描述：

> A hidden page is created for the prerendered URL, which will do full loading of all dependent resources, as well as execution of Javascript. If the user navigates to the page, the hidden page will be swapped into the current tab and made visible.

B页面是在一个隐藏页中加载的，当我们点击B链接时，隐藏页就替入当前标签页并置为可见。

从字面上看，没有任何字眼暗示说tab id会变化。

但实际上，tab id确实变了，这可以在background.js里绑定一个onReplaced事件来检查。

onReplaced[^12710.2]事件描述如下：

> Fired when the contents of the tab is replaced by a different (usually previously pre-rendered) tab.

绑定的代码如下：

    chrome.tabs.onReplaced.addListener(function(addedTabId, removedTabId) {
      console.log "added tabid: " + addedTabId;
      console.log "removed tabid: " + removedTabId;
      });
    

打开背景页的开发者工具，我们就能看到，模拟的点击事件发生时，Chrome浏览器移除了一个标签页，并新增了一个。只是从我们肉眼来说，根本看不到置换过程。

我的情况里，因为tab id变化，所以taskTab的值其实已经没用，结果导致点击打开的about页面没能注入内容脚本。如果你也碰上内容脚本动态注入失败的情况，不妨检查下标签页的id值。

[^12710.1]:    
    [Chrome Prerendering &#8211; The Chromium Projects][1]

[^12710.2]:    
    [chrome.webNavigation &#8211; Google Chrome][2]

 [1]: http://www.chromium.org/developers/design-documents/prerender
 [2]: https://developer.chrome.com/extensions/webNavigation#event-onTabReplaced