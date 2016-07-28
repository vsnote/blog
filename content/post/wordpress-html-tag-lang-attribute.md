---
title: WordPress html 标签的 lang 属性
author: 陈 三
layout: post
date: 2014-04-15T14:50:58+00:00
excerpt: 修改 WordPress 前台页面的 lang 属性值
url: /wordpress-html-tag-lang-attribute.html
views:
  - 516
categories:
  - WordPress

---
WordPress 的 header.php 文件里，html 标签是这么写的：

    <html <?php language_attributes(); ?>>
    

如果你安装 WordPress 时下载的是中文包，则前台页面输出后的 html 标签为：

    <html lang="zh-CN">
    

但如果你安装时下载的是英文包，那么前台页面页面输出的 html 标签里 lang 属性为：

    <html lang="en-US">
    

W3 [^12320.1]有论述添加这个属性的种种好处。

可如果你安装了英文包，写的内容却是中文，或说你现在想把 lang 属性值设置为 &#8220;zh-CN&#8221;。`language_attributes()` 帮不了忙，WordPress 文档会建议你安装一个中文语言包[^12320.2]。

但我只想修改前台页面输出，后端界面是中文或英文倒是无所谓，所以一个最快捷的方法，是直接硬编码：

    <html lang="zh-CN">
    

对硬编码反感者来说，这行代码可能罪大恶极 &#8211; 那还是建议安装一个中文语言包，参考脚注2。

[^12320.1]:    
    [Why use the language attribute?][1]

[^12320.2]:    
    [Installing WordPress in Your Language « WordPress Codex][2]

 [1]: http://www.w3.org/International/questions/qa-lang-why.en
 [2]: http://codex.wordpress.org/Installing_WordPress_in_Your_Language