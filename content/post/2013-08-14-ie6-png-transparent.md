---
title: IE6 下的 PNG 透明
author: 陈 三
layout: post
date: 2013-08-14T11:19:46+00:00
url: /ie6-png-transparent.html
dsq_thread_id:
  - 1766148515
views:
  - 413
categories:
  - 前端开发
tags:
  - css
  - ie6
  - png

---
就我的实践经验，IE6 下解决 PNG 图片透明问题，[DD_belatedPNG][1] 是比较方便的。

它的用法如下：

    <!--[if IE 6]>
    <script src="DD_belatedPNG.js"></script>
    <script>
      /* EXAMPLE */
      DD_belatedPNG.fix('.png_bg');
    
      /* string argument can be any CSS selector */
      /* .png_bg example is unnecessary */
      /* change it to what suits you! */
    </script>
    <![endif]--> 
    

很多人可能就参照它的示例写，比如，腾讯旗下的导航站是这样写的：

    <script type="text/javascript">
    try{
        if(DD_belatedPNG){
            DD_belatedPNG.fix('img,li.png-filter a span.qqicon-logout,li.png-filter a span.qqicon,.icon-weixin,.mailInput-icon-unfold,#changeSearchEngine_ICON,#currentMail-s,.engineWrap a,.game-box .caption a.little-game, .game-box .caption a.page-game, .game-box .caption a.web-game, .xzSelect .drop, .xzClosed, .xzClosed.hover,ul.channel-videoImg span.title em,.down-icon,.history-del,.channel-videoline,.videoplay,.video-pages a,.v-new');
        }
    }catch(e){};
    </script>
    

我们能看到，`fix` 里有一堆的 class 及 id 又或者其他 CSS 选择符。这一堆代码维护起来很困难 &#8211; 写了基本就不要想修改。

我的方法是，只设定一个 CSS 类 `pngfix`，凡使用 PNG 透明图片的元素，都加上该类，

    <h2 class="pngfix">Goodbye IE6</h2>
    

然后 JavaScript 语句只要一句：

    DD_belatedPNG.fix('.pngfix');   
    

又因为我在 CSS 中抽象出一个 [贴图定位的类][2] `.sprite`，则连 `.pngfix` 都可以省掉，直接使用 `.sprite`：

    DD_belatedPNG.fix('.sprite');
    

## 注意事项

  1. 如果背景图片使用 CSS 贴图定位，DD_belatedPNG 这个方法同样存在些问题，比如背景图片有1像素的偏移
  2. 如果 PNG 使用 map 热点，则 DD_belatedPNG 处理后，热点的链接会无法点击，一个替代方法是 [Unit PNG Fix][3]

 [1]: http://www.dillerdesign.com/experiment/DD_belatedPNG/
 [2]: http://www.zfanw.com/blog/css-sprite.html
 [3]: http://labs.unitinteractive.com/unitpngfix.php