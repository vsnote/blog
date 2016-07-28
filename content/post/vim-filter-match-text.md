---
title: Vim 过滤匹配的文本
author: 陈 三
layout: post
date: 2014-02-23T04:22:13+00:00
excerpt: 用 Vim 从文件里过滤出需要的内容
url: /vim-filter-match-text.html
views:
  - 809
categories:
  - 未分类
tags:
  - vim

---
我偶尔会有这样一种需求：从文本中过滤出需要的内容 &#8211; 这个内容可以用正则表达式匹配到。比如这一个 [HTTP 请求/响应信息][1]文件，取一小段如下：

    
    POST http://d.web2.qq.com/channel/send_sess_msg2 HTTP/1.1
    Origin: http://web2.qq.com
    User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64; rv:23.0) Gecko/20100101 Firefox/23.0
    Content-Type: application/x-www-form-urlencoded
    Accept: */*
    Referer: http://web2.qq.com
    Content-Length: 716
    Cookie: pgv_pvid=5576286324; pgv_info=pgvReferrer=&ssid=s3145890760; verifysession=h02MUeRLXDVh33iXxfbIXP7QPznYyuVOP4qCJPVhXD-BDw72d9W6sLl7dfrUx2Wfsq4w1Vhw2ggRjxhhzMf2vfANA**; ptui_loginuin=2804187804; ptisp=ctc; RK=dBvTz+lA+k; ptcz=45fbc214cbc91062f919bf6c753c60da6fa4ea937a08bfd0a94b33a29f3eab94; ptwebqq=2f4cdbb354c4cfe971e15aa3872ffbffe86bff65c8b0cc4a2998e4e0e9f89c23; pt2gguin=o2804187804; uin=o2804187804; skey=@0uc0QCvS5; p_uin=o2804187804; p_skey=*HFTMH8l0rM5Gszdip1vHyJI4MneS73LL*xTsgtViNM_; pt4_token=BGcr-KPcEj-TDwNlt6HJhQ__
    Connection: Keep-Alive
    Accept-Encoding: gzip
    Accept-Language: zh-CN,en,*
    Host: d.web2.qq.com
     
    r={"to":<mark>3105771284</mark>,"content":"[[\"font\",{\"name\":\"宋体\",\"size\":20,\"style\":[0,0,0],\"color\":\"ff0000\"}]]","clientid":"36385748","psessionid":"8368046764001d636f6e6e7365727665725f77656271714031302e3133392e372e31363000007ba400000228036e04009c8224a76d0000000a403075633051437653356d00000028d2cbdb5f463a51f3eb82c04c37cce7848ebb9d449aca351811c72a04a5f75412ab0590b690630bdb","service_type":0,"group_sig":"da531819808f120bd0b6c9fc377e6fc76af363ef80d7ba965e7aa1de952fbaf9710ff04e74743c2dd104aba1f357758b"}
    HTTP/1.1 200 OK
    Date: Fri, 03 Jan 2014 06:51:14 GMT
    Content-Type: text/plain; charset=utf-8
    Content-Length: 29
    Cache-Control: no-cache
    Connection: close
     
    {"retcode":0,"result":"ok"}
    

我需要 `r={"to":` 后的一组数字 &#8211; 号码。

我马上可以想到的处理方式是：

  1. 匹配该组数字外的所有文本并删除
  2. 匹配该组数字，删除不匹配的所有文本

但就我查找的资料， Vim 并没有便利的方法实现上面的处理 &#8211; 你也可以认为上面的处理方式本身就有些问题。所以还是要绕点远路。

有一个需要声明的概念是，Vim 在查找/替换时，是针对**行**做处理的，这个与 grep 或 sed 是一样的。

  1. 删除所有不匹配规则 `r={"to":` 的行[^11613.1]
    
        :v/r={"to":\d\+,/d
        
    
    或者：
    
        :g!/r={"to":\d\+,/d
        
    
    命令中最后一个 `d` 表示**删除不匹配的行**。
    
    处理后，文件剩下如下格式的内容：
    
        r={"to":3105771284,"content":"[[\"font\",{\"name\":\"宋体\",\"size\":20,\"style\":[0,0,0],\"color\":\"ff0000\"}]]","clientid":"36385748","psessionid":"8368046764001d636f6e6e7365727665725f77656271714031302e3133392e372e31363000007ba400000228036e04009c8224a76d0000000a403075633051437653356d00000028d2cbdb5f463a51f3eb82c04c37cce7848ebb9d449aca351811c72a04a5f75412ab0590b690630bdb","service_type":0,"group_sig":"da531819808f120bd0b6c9fc377e6fc76af363ef80d7ba965e7aa1de952fbaf9710ff04e74743c2dd104aba1f357758b"}
        r={"to":3688265155,"content":"[[\"font\",{\"name\":\"宋体\",\"size\":20,\"style\":[0,0,0],\"color\":\"ff0000\"}]]","clientid":"36385748","psessionid":"8368046764001d636f6e6e7365727665725f77656271714031302e3133392e372e31363000007ba400000228036e04009c8224a76d0000000a403075633051437653356d00000028d2cbdb5f463a51f3eb82c04c37cce7848ebb9d449aca351811c72a04a5f75412ab0590b690630bdb","service_type":0,"group_sig":"61e61272ea83bba9efbe74ce82081c2cd9d4b4c88773f4e72e7fa535cdf9c2dc0801edb02719e6c7abd5e24ce8dec4aa"}
        r={"to":1559096246,"content":"[[\"font\",{\"name\":\"宋体\",\"size\":20,\"style\":[0,0,0],\"color\":\"ff0000\"}]]","clientid":"36385748","psessionid":"8368046764001d636f6e6e7365727665725f77656271714031302e3133392e372e31363000007ba400000228036e04009c8224a76d0000000a403075633051437653356d00000028d2cbdb5f463a51f3eb82c04c37cce7848ebb9d449aca351811c72a04a5f75412ab0590b690630bdb","service_type":0,"group_sig":"24437e4e1f42517f3c6900eb26407dcbd607ca3a474957e0d056b77a98820b5038dd4fbdc56b9a178e128861b9097481"}
        

  2. Vim 替换命令[^11613.2]
    
        :%s/^r={"to":\(\d\+\),.*$/\1
        
    
    `%` &#8211; 查找文件中所有行
    
    `s` &#8211; Vim 的替换命令 substitute 命令的短写法
    
    `^r={"to":\(\d\+\),.$*` &#8211; 正则规则，指示要匹配的内容
    
    `\1` &#8211; 前面正则规则中 () 匹配到的内容

Vim 的正则看起来略绕，比如 + 要转义，( 也要转义。我在写 JavaScript 正则时是不需要的。

如此，我们就过滤出文件里所有的号码了。

[^11613.1]:    
    [Power of g &#8211; Vim Tips Wiki][2]

[^11613.2]:    
    [Vim documentation: pattern][3]

 [1]: https://gist.github.com/chenxsan/9166312 "Gist"
 [2]: http://vim.wikia.com/wiki/Power_of_g
 [3]: http://vimdoc.sourceforge.net/htmldoc/pattern.html