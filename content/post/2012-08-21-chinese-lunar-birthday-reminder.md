---
title: 农历生日提醒
author: 陈 三
layout: post
date: 2012-08-21T04:15:37+00:00
url: /chinese-lunar-birthday-reminder.html
views:
  - 1439
dsq_thread_id:
  - 812807895
categories:
  - 未分类
tags:
  - Google
  - JavaScript
  - 农历生日

---
我觉得农历生日存在意义不大。但我妈总提醒我的农历生日，所以，在我妈失忆前，我猜想我得适应她的习惯。

想写这个脚本是因为新近接触 Google Apps script，看到里面提供日历接口，而我又知道 Google 日历里有中国农历，所以猜想可能会有中国农历 API 接口 &#8211; 可惜最后查下，并没有农历接口，只好另想他法。就是这篇内容。

原理很简单，就是每天凌晨检查电子表格列表，看当天是否有人过农历生日，如果有，就发送邮件提醒。

[resp_image id=&#8217;15782&#8242; caption=&#8221; ]

上图是 Google 电子表格，总共三列，第一列为姓名，第二列为农历生日，“8月22日”是为农历，即八月廿二，写成新历形式只是着方便程序书写，第三列为接收邮箱的地址，可以只填写第一个，之后如果留空，则默认使用第一个邮箱接收。

  1. 首先[复制一份“**农历生日提醒**”电子表格][1]到 Google 文档里,其中包含表格及脚本代码

  2. 打开该文档，访问菜单 Tools -> Script editor&#8230;，然后访问 Resources -> Current script&#8217;s triggers&#8230;
    
    设置触发时间为每天的凌晨0点到1点，这样 Googel Apps script 就会每天运行这个函数，然后根据函数结果决定发送或不发送邮件提醒。设置过程中 Google 会要求授权访问 Google mail 及 Google spreadsheet，请允许。

  3. 感谢台湾中央研究院计算中心提供的[两千年中西历转换工具][2]。根据它的说明，以上方法可以用到 2100 年。希望我还能活到那一天.

邮件标题及邮件内容均可以到代码中更改.

 [1]: https://docs.google.com/spreadsheet/ccc?key=0AntAce2hG9gQdEpDVTVabmcyN19qeWkwZGtNYUtveWc&newcopy=true
 [2]: http://sinocal.sinica.edu.tw/