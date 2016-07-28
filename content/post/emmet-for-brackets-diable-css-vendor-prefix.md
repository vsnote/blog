---
title: Emmet for Brackets禁用CSS浏览器前缀
author: 陈 三
layout: post
date: 2014-08-16T00:44:59+00:00
url: /emmet-for-brackets-diable-css-vendor-prefix.html
views:
  - 669
categories:
  - 前端开发
tags:
  - Brackets

---
Emmet[^13389.1]有自动添加CSS**浏览器前缀**(vendor prefix)的功能。

譬如在Brackets输入以下CSS(*表示光标位置)：

    div{
      bgs*
    

按<kbd>Tab</kbd>键展开后如下，

    div{
      -webkit-background-size:
      background-size:
    

不过我不乐意它来主张。我更愿意用Autoprefixer[^13389.2]配合Grunt.js或Gulp.js做处理，可控度更高，而且源代码保持干净。

所以我需要禁用这个功能。

Emmet提供了一个配置项：`css.autoInsertVendorPrefixes`[^13389.3]，但在Brackets下，这个配置过程非常纠结。

我的系统是openSUSE 13.1，禁用的步骤如下：

  1. 主目录/home/sam下新建一个目录emmet(你要建在其他地方也无妨)
  2. 在emmet目录中添加preferences.json文件
  3. 文件中添加如下代码：`{"css.autoInsertVendorPrefixes": false}`
  4. 打开Brackets主界面中的`Emmet`菜单，选择`Preferences...`
  5. 在Extension folder里填入`/home/sam/emmet`(不能使用~/emmet)
  6. 重启Brackets

[^13389.1]:    
    [emmetio/brackets-emmet][1]

[^13389.2]:    
    [ai/autoprefixer][2]

[^13389.3]:    
    [preferences.json][3]

 [1]: https://github.com/emmetio/brackets-emmet
 [2]: https://github.com/ai/autoprefixer
 [3]: http://docs.emmet.io/customization/preferences/