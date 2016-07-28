---
title: IE6、7、8 与 RGBA
author: 陈 三
layout: post
date: 2013-07-18T14:46:07+00:00
excerpt: 使用微软私有 filter，实现 IE6、7、8 下 RGBA 效果。
url: /ie6-ie7-ie8-rgba.html
dsq_thread_id:
  - 1509845696
views:
  - 1061
categories:
  - 前端开发
tags:
  - css hack
  - ie6
  - ie7
  - ie8

---
Google Chrome 自 1.0 开始支持 RGBA，Firefox 从 3.0 开始，IE 比较晚，从 IE9 才开始。

rgba 很常用，可以给颜色设置透明度，比如：

    <p style="background:rgba(0,255,0,.3);">hello rgba</p>
    

显示效果如下：

<p style="background:rgba(0,255,0,.3)">
  hello rgba
</p>

现代浏览器中，我们看到的是浅绿色背景，黑色字体。IE6、7、8 不认识 rgba 规则，所以会忽略它，就像没有声明过背景一样 &#8211; 所以是白底黑字。

但借助 IE 私有滤镜(filter)，我们可以达到同样效果：

    <p class="bga">hello rgba</p>
    
    <!--[if IE]> 
    <style>
    .bga{
        background:transparent;
        -ms-filter: "progid:DXImageTransform.Microsoft.gradient(GradientType=1, StartColorStr='#4C00FF00', EndColorStr='#4C00FF00')";/* IE8 */
        filter: progid:DXImageTransform.Microsoft.Gradient(GradientType=1, StartColorStr='#4C00FF00', EndColorStr='#4C00FF00');/* IE6、7 */
        zoom: 1;
    }
    <![endif]-->
    

现在，IE6、7、8 中，效果就跟现代浏览器一样了：

<p class="bga">
  hello rgba
</p>

<!--[if IE]> 

<![endif]-->

## 参考

  1. [MDN &#8211; CSS color value][1]
  2. [MSDN -ms-filter property][2]
  3. [rgba &#8211; argb 转换工具][3]

 [1]: https://developer.mozilla.org/en-US/docs/Web/CSS/color_value
 [2]: http://msdn.microsoft.com/en-us/library/ie/ms530752(v=vs.85).aspx
 [3]: http://www.zfanw.com/tools/argb-rgba.html