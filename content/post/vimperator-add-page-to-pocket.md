---
title: Vimperator 里保存网页到 Pocket
author: 陈 三
layout: post
date: 2012-06-14T07:03:24+00:00
url: /vimperator-add-page-to-pocket.html
views:
  - 2019
dsq_thread_id:
  - 725438223
categories:
  - Firefox
  - vimperator
tags:
  - JavaScript
  - vimperator

---
**2015.05.24** 推荐一个[新方法][1]，以下不再推荐使用。

以前 [tombloo][2] 还能用的时候，就直接用它保存链接到 Pocket 里，但现在不知道什么原因无法保存（可能因为从 Read it later 改名为 Pocket？），就只好另寻方法。

还好 Pocket 针对 Firefox 提供一个[书签小程式 bookmarklet][3]，你只要拖动保存它到浏览器的书签栏上，在需要保存的页面按下该按钮即可保存网页到 Pocket 里。

但作为 Vimperator 用户，用鼠标显然不合习惯，所以需要找个办法，可以通过键盘完成上面需要通过鼠标完成的任务。

  1. 通过 `:qmark` 命令给 Vimperator 添加快速书签 p &#8211; Javascript 代码拷自小书签程式的链接[^3955.1]
    
        :qmark p javascript:(function(){var%20e=function(t,n,r,i,s){var%20o=[6087319,5700434,1277186,3061050,5288415,3121548,4527391,4232602,2376464,5969755];var%20i=i||0,u=0,n=n||[],r=r||0,s=s||0;var%20a={'a':97,'b':98,'c':99,'d':100,'e':101,'f':102,'g':103,'h':104,'i':105,'j':106,'k':107,'l':108,'m':109,'n':110,'o':111,'p':112,'q':113,'r':114,'s':115,'t':116,'u':117,'v':118,'w':119,'x':120,'y':121,'z':122,'A':65,'B':66,'C':67,'D':68,'E':69,'F':70,'G':71,'H':72,'I':73,'J':74,'K':75,'L':76,'M':77,'N':78,'O':79,'P':80,'Q':81,'R':82,'S':83,'T':84,'U':85,'V':86,'W':87,'X':88,'Y':89,'Z':90,'0':48,'1':49,'2':50,'3':51,'4':52,'5':53,'6':54,'7':55,'8':56,'9':57,'\/':47,':':58,'?':63,'=':61,'-':45,'_':95,'&':38,'$':36,'!':33,'.':46};if(!s||s==0){t=o[0]+t}for(var%20f=0;f<t.length;f++){var%20l=function(e,t){return%20a[e[t]]?a[e[t]]:e.charCodeAt(t)}(t,f);if(!l*1)l=3;var%20c=l*(o[i]+l*o[u%o.length]);n[r]=(n[r]?n[r]+c:c)+s+u;var%20p=c%(50*1);if(n[p]){var%20d=n[r];n[r]=n[p];n[p]=d}u+=c;r=r==50?0:r+1;i=i==o.length-1?0:i+1}if(s==344){var%20v='';for(var%20f=0;f<n.length;f++){v+=String.fromCharCode(n[f]%(25*1)+97)}o=function(){};return%20v+'a3dcd699e5'}else{return%20e(u+'',n,r,i,s+1)}};var%20t=document,n=t.location.href,r=t.title;var%20i=e(n);var%20s=t.createElement('script');s.type='text/javascript';s.src='https://getpocket.com/b/r4.js?h='+i+'&u='+encodeURIComponent(n)+'&t='+encodeURIComponent(r);e=i=function(){};var%20o=t.getElementsByTagName('head')[0]||t.documentElement;o.appendChild(s)})()
        

  2. Vimperator 会自动将上述设置保存到 quickmarks 文件中

  3. 正常模式下键入 <kbd>gop</kbd> 即可保存你要保存的网页到 Pocket

另一种办法，可以使用 vimperator [readitlater.js 插件][4]，由 [@dunkelsvL][5] 君提供地址，由热情的岛国人民开发。

参考链接：[second life][6]

[^3955.1]:    
    2015.05.24 订正 bookmarklet 代码，多谢 Geng-G-Razor 在 Github report 库上帮忙报告错误

 [1]: https://github.com/chenxsan/report/issues/2#issuecomment-104982715
 [2]: https://github.com/to/tombloo/wiki/
 [3]: https://getpocket.com/add?sb=1
 [4]: https://github.com/vimpr/vimperator-plugins/blob/a5a7259a23509164e7ca3bf92deff6aa23209538/readitlater.js
 [5]: http://twitter.com/dunkelsvL
 [6]: http://subtech.g.hatena.ne.jp/secondlife/20080919/1221795410