---
title: 从meta viewport聊起
author: 陈 三
layout: post
date: 2014-05-31T03:23:49+00:00
url: /从meta-viewport聊起.html
views:
  - 1701
categories:
  - 前端开发
tags:
  - viewport

---
iPhone 4s的参数：

> 960-by-640-pixel resolution at 326 ppi

长960像素，宽640像素，ppi指pixels per inch，每英寸长度的像素数。

但Safari里，渲染页面默认是按980px宽来的。

比如如下的HTML：

    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8">
      <title>iOS7 safari</title>
    </head>
    <body>
      <div>陈三</div>
    </body>
    </html>
    

CSS规则：

    div{
      width:980px;
      background-color:green;
      color: white;
      font-size:100px;
    }
    

Safari里该页面效果：

[<img src="http://www.zfanw.com/blog/wp-content/uploads/2014/05/2014-05-30-23.56.07.png" alt="ios7 safari 980px" width="320" height="480" class="alignnone size-full wp-image-12858" srcset="https://www.zfanw.com/blog/wp-content/uploads/2014/05/2014-05-30-23.56.07.png 640w, https://www.zfanw.com/blog/wp-content/uploads/2014/05/2014-05-30-23.56.07-200x300.png 200w, https://www.zfanw.com/blog/wp-content/uploads/2014/05/2014-05-30-23.56.07-66x100.png 66w" sizes="(max-width: 320px) 100vw, 320px" />][1]

一个自称宽为640像素宽的手机，带的一个浏览器却可以布置一个980px的div块。

怎么回事？

问题在于`viewport`[^12845.1]。

在Safari里，默认视口宽度为980px。你可以把它想像成桌面浏览器宽度为980px的样子。

所以，上面的HTML代码，我们写成：

    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8">
      <meta name="viewport" content="width=980"><!-- 加了这一句 -->
      <title>iOS7 safari</title>
    </head>
    <body>
      <div>陈三</div>
    </body>
    </html>
    

效果跟上面是一样的。

(如果你愿意做个试验，不断增加`content`里`width`的值，会发现，`width`值超过1293时，safari底部会出现横向滚动条。这是否意味着640像素宽的4S屏幕最多只能把握1293px？有待说明。)

设计自适应页面时，我们常常能看到`content`的另外一个取值：

    <meta name="viewport" content="width=device-width">
    

这一句的意思是，把`viewport`的宽度设置为`device-width`(设备宽度)。

拿4s手机说，我们马上能想到，`viewport`的宽度为640像素。

但这个判断是错的，`viewport`的值是320px，可以通过设置

    <meta name="viewport" content="width=320">
    

来验证。这一句的效果跟设置`content="width=device-width"`是一样的。

也就是说，所谓的`device-width`，在4s手机上的取值是320px。是`640/2`得来的(2是4S的device pixel ratio取值)。

这看起来简直混乱且莫名其妙。

但如果从「适用」的角度说，就能理解这混乱。早期的15寸、17寸CRT显示器，那时屏幕分辨率通常就1024&#215;768，甚至更小，800&#215;600，同样大小的字体，比如14px，在15寸屏幕上可以看清楚，但换成同样分辨率大小仅3.5寸的屏幕，还看得清楚吗？这会招致使用上的问题。

于是在手机上，我们需要做些调整。14px的字体，我们会用更多的物理像素来表示。

这里，两个概念需要区别，一是CSS的px单位，二是物理像素。

CSS里定义的px，是会变的，它不是绝对单位，比如1cm就是1cm，走遍地球都一样。我们借助一张图片来说明，这张图片大小为710&#215;425 px(注：图片来自维基)：

  1. `content="width=980"`
    
    [<img src="http://www.zfanw.com/blog/wp-content/uploads/2014/05/2014-05-31-10.38.33.png" alt="width=980 css px" width="320" height="480" class="alignnone size-full wp-image-12900" srcset="https://www.zfanw.com/blog/wp-content/uploads/2014/05/2014-05-31-10.38.33.png 640w, https://www.zfanw.com/blog/wp-content/uploads/2014/05/2014-05-31-10.38.33-200x300.png 200w, https://www.zfanw.com/blog/wp-content/uploads/2014/05/2014-05-31-10.38.33-66x100.png 66w" sizes="(max-width: 320px) 100vw, 320px" />][2]

  2. `content="width=320"`
    
    [<img src="http://www.zfanw.com/blog/wp-content/uploads/2014/05/2014-05-31-10.39.00.png" alt="width=320 viewport" width="320" height="480" class="alignnone size-full wp-image-12902" srcset="https://www.zfanw.com/blog/wp-content/uploads/2014/05/2014-05-31-10.39.00.png 640w, https://www.zfanw.com/blog/wp-content/uploads/2014/05/2014-05-31-10.39.00-200x300.png 200w, https://www.zfanw.com/blog/wp-content/uploads/2014/05/2014-05-31-10.39.00-66x100.png 66w" sizes="(max-width: 320px) 100vw, 320px" />][3]

这张长710px的图片，物理尺寸却完全不一样。我们通过改变`viewport`的值，改变了单位px的绝对长度。

但4S手机的**物理像素**不会变，不可能因为我们改个`viewport`的值苹果就得调整4S的参数页面。

所以设计师给4S手机设计网页时，敲下640&#215;960的图片大小，我们就知道，前端的不和谐长存。

[^12845.1]:    
    [Safari Web Content Guide: Configuring the Viewport][4]

 [1]: http://www.zfanw.com/blog/wp-content/uploads/2014/05/2014-05-30-23.56.07.png "点击查看大图"
 [2]: http://www.zfanw.com/blog/wp-content/uploads/2014/05/2014-05-31-10.38.33.png
 [3]: http://www.zfanw.com/blog/wp-content/uploads/2014/05/2014-05-31-10.39.00.png
 [4]: https://developer.apple.com/library/ios/documentation/appleapplications/reference/safariwebcontent/usingtheviewport/usingtheviewport.html