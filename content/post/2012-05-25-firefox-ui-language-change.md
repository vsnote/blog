---
title: 更改 Firefox 界面语言
author: 陈 三
layout: post
date: 2012-05-25T07:26:52+00:00
url: /firefox-ui-language-change.html
views:
  - 4091
dsq_thread_id:
  - 703074038
dsq_needs_sync:
  - 1
categories:
  - Firefox
tags:
  - Firefox
  - 界面语言

---
因为前些日子在台湾正体里打酱油（指翻译些 Firefox 相关文章），用英文界面 Firefox 的话，许多专用名称查找不便，就打算把 Firefox 的界面语言从英文改成台湾正体。

方法如下：

  1. 下载安装你需要的语言包 (language pack)，[下载地址][1]，请选择相应版本号 -> 操作系统 -> xpi 文件夹 -> 你要安装的语言包插件，即 xpi 组件，我选择的是 zh-TW.xpi。

  2. 打开 `about:config`，搜索 “general.useragent.locale” &#8211; 这是在 Firefox 12 里的情况，双击修改默认值 &#8220;en-US&#8221; 为 &#8220;zh-TW&#8221;。

  3. 修改 `intl.locale.matchOS` 值为 `false`（见评论），然后重启 Firefox 即可。

当然，你也可以用些扩展组件来切换语言，不过我还是更喜欢上面的办法。个人喜好。

 [1]: http://releases.mozilla.org/pub/mozilla.org/firefox/releases/