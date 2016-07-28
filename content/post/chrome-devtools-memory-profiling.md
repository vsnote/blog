---
title: Chrome 开发者工具之内存使用分析
author: 陈 三
layout: post
date: 2015-12-06T12:43:44+00:00
url: /chrome-devtools-memory-profiling.html
views:
  - 933
categories:
  - 前端开发
tags:
  - Chrome

---
对我们 JavaScript 开发者来说，因为内存有自动回收机制，所以大部分时间，我们并没打算关心内存。

但是，移动设备的内存通常有限，卡顿、崩溃的现象并不少见，于是我们又不得不开始关心内存。

从哪里开始？怎样的一个步骤？

（因为 chrome 开发者工具经常变动，所以这里说明一下，以下截图如果不是特别强调，用到的浏览器均指 Chrome 49.0.2582.0 (Official Build) canary (64-bit) 版本）

  1. Chrome 内置的 task manager，（图片来自 [Google Devtools 网站][1]），粗略观察
    
    ![chrome 任务管理器][2]

  2. 在 Chrome 内置任务管理器中发现内存可能有问题后，我们想知道，具体是怎样：
    
      1. 打开 Chrome Devtools
      2. 点击 Timeline 标签页
      3. 勾选 **Memory** 选项
      4. 点击录制按钮
    
    <a href="https://www.zfanw.com/blog/wp-content/uploads/2015/12/chrome-devtools-timeline-memory.png" rel="attachment wp-att-17720"><img src="https://www.zfanw.com/blog/wp-content/uploads/2015/12/chrome-devtools-timeline-memory.png" alt="chrome devtools timeline panel with memory option on" width="792" class="alignnone size-full wp-image-17720" srcset="https://www.zfanw.com/blog/wp-content/uploads/2015/12/chrome-devtools-timeline-memory.png 792w, https://www.zfanw.com/blog/wp-content/uploads/2015/12/chrome-devtools-timeline-memory-300x197.png 300w, https://www.zfanw.com/blog/wp-content/uploads/2015/12/chrome-devtools-timeline-memory-100x66.png 100w, https://www.zfanw.com/blog/wp-content/uploads/2015/12/chrome-devtools-timeline-memory-768x505.png 768w, https://www.zfanw.com/blog/wp-content/uploads/2015/12/chrome-devtools-timeline-memory-520x342.png 520w" sizes="(max-width: 792px) 100vw, 792px" /></a>
    
    如图，我们能看到，滚动页面时，内存用量在逐步升高。

  3. 是谁引起的内存增加？增加的内存是否可以回收，如果不能，是否导致内存泄漏？Chrome 开发者工具 Profiles 面板下有两个内存分析的工具，
    
      * [Take Heap Snapshot][3]
      * [Record Heap Allocations][4]
    
    前者能够捕捉当前的内存分配情况，后者可纪录不同时间里内存分配与回收的情况。它们的用法，Chrome devtools 网站上均有说明，虽然文档配图部分老旧，但内容多数并没有问题。另外，这两个工具涉及到大量的内存知识，所以算是 devtools 里比较复杂的应用。
    
    我个人的经验，Take Heap Snapshot 用得更多，我们可以多次录制快照，然后比对快照，哪些操作引发了哪些类型的数据增加或减小，非常容易定位。

## 扩展阅读

  1. 视频 &#8211; [对我们 JavaScript 开发者来说，因为内存有自动回收机制，所以大部分时间，我们并没打算关心内存。

但是，移动设备的内存通常有限，卡顿、崩溃的现象并不少见，于是我们又不得不开始关心内存。

从哪里开始？怎样的一个步骤？

（因为 chrome 开发者工具经常变动，所以这里说明一下，以下截图如果不是特别强调，用到的浏览器均指 Chrome 49.0.2582.0 (Official Build) canary (64-bit) 版本）

  1. Chrome 内置的 task manager，（图片来自 [Google Devtools 网站][1]），粗略观察
    
    ![chrome 任务管理器][2]

  2. 在 Chrome 内置任务管理器中发现内存可能有问题后，我们想知道，具体是怎样：
    
      1. 打开 Chrome Devtools
      2. 点击 Timeline 标签页
      3. 勾选 **Memory** 选项
      4. 点击录制按钮
    
    <a href="https://www.zfanw.com/blog/wp-content/uploads/2015/12/chrome-devtools-timeline-memory.png" rel="attachment wp-att-17720"><img src="https://www.zfanw.com/blog/wp-content/uploads/2015/12/chrome-devtools-timeline-memory.png" alt="chrome devtools timeline panel with memory option on" width="792" class="alignnone size-full wp-image-17720" srcset="https://www.zfanw.com/blog/wp-content/uploads/2015/12/chrome-devtools-timeline-memory.png 792w, https://www.zfanw.com/blog/wp-content/uploads/2015/12/chrome-devtools-timeline-memory-300x197.png 300w, https://www.zfanw.com/blog/wp-content/uploads/2015/12/chrome-devtools-timeline-memory-100x66.png 100w, https://www.zfanw.com/blog/wp-content/uploads/2015/12/chrome-devtools-timeline-memory-768x505.png 768w, https://www.zfanw.com/blog/wp-content/uploads/2015/12/chrome-devtools-timeline-memory-520x342.png 520w" sizes="(max-width: 792px) 100vw, 792px" /></a>
    
    如图，我们能看到，滚动页面时，内存用量在逐步升高。

  3. 是谁引起的内存增加？增加的内存是否可以回收，如果不能，是否导致内存泄漏？Chrome 开发者工具 Profiles 面板下有两个内存分析的工具，
    
      * [Take Heap Snapshot][3]
      * [Record Heap Allocations][4]
    
    前者能够捕捉当前的内存分配情况，后者可纪录不同时间里内存分配与回收的情况。它们的用法，Chrome devtools 网站上均有说明，虽然文档配图部分老旧，但内容多数并没有问题。另外，这两个工具涉及到大量的内存知识，所以算是 devtools 里比较复杂的应用。
    
    我个人的经验，Take Heap Snapshot 用得更多，我们可以多次录制快照，然后比对快照，哪些操作引发了哪些类型的数据增加或减小，非常容易定位。

## 扩展阅读

  1. 视频 &#8211;][5] 
  2. 视频 &#8211; [Google I/O 2013 &#8211; A Trip Down Memory Lane with Gmail and DevTools][6]

 [1]: https://developers.google.com/web/tools/chrome-devtools/profile/memory-problems/memory-diagnosis?hl=en#monitor-memory-using-chrome-task-manager
 [2]: https://developers.google.com/web/tools/chrome-devtools/profile/memory-problems/imgs/task-manager.png
 [3]: https://developers.google.com/web/tools/chrome-devtools/profile/memory-problems/heap-snapshots?hl=en
 [4]: https://developers.google.com/web/tools/chrome-devtools/profile/memory-problems/allocation-profiler?hl=en
 [5]: https://www.youtube.com/watch?v=L3ugr9BJqIs
 [6]: https://www.youtube.com/watch?v=x9Jlu_h_Lyw