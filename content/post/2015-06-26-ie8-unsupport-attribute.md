---
title: IE8 不支持的
author: 陈 三
layout: post
date: 2015-06-26T07:24:43+00:00
excerpt: IE8 不支持的一些 CSS 属性、JavaScript 方法及对策
url: /ie8-unsupport-attribute.html
views:
  - 756
categories:
  - 前端开发
tags:
  - ie8

---
国内的前端开发大环境一向糟糕，比如早两年，还有好多网站要求支持 IE6，现在稍微好些，但因为微妙的国情，大部分还是在支持 IE8。以下是我经常碰上的、IE8 不支持的 CSS 属性或 JavaScript 功能。

  1. opacity
    
    可以使用 [微软私有的 filter][1] 替代：
    
        -ms-filter: "progid:DXImageTransform.Microsoft.Alpha(Opacity=50)";
        
    
    如果你的前端工具箱中有 PostCSS，则可以使用 [PostCSS Opacity][2] 插件，它可以检测 `opacity` 属性并添加相应 `-ms-filter`。

  2. rgba
    
    同样使用微软私有 filter 替补，[具体点击查看 rgba 与 Microsoft 私有 filter 转换工具][3]。

  3. Date.now()
    
    [IE8 还不支持 Date.now() 方法][4]，解决办法见 [es5 shim][5]：
    
        if (!Date.now) {
            Date.now = function now() {
                return new Date().getTime();
            };
        }
        

## 附

  1. 微软在 2016.1.12 起，将不再给 [IE8、9、10][6] 提供支持

 [1]: https://msdn.microsoft.com/en-us/library/ms530752(v=vs.85).aspx
 [2]: https://github.com/iamvdo/postcss-opacity
 [3]: http://www.zfanw.com/tools/argb-rgba.html "rgba 与 filter 转换工具"
 [4]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/now#Browser_compatibility
 [5]: https://github.com/es-shims/es5-shim/blob/master/es5-shim.js#L1189
 [6]: http://blogs.msdn.com/b/ie/archive/2014/08/07/stay-up-to-date-with-internet-explorer.aspx