---
title: Privoxy 去除 iOS 爱奇艺客户端广告
author: 陈 三
layout: post
date: 2015-01-11T12:03:52+00:00
url: /privoxy-remove-iqiyi-ios-client-ad.html
views:
  - 2456
categories:
  - openSUSE
tags:
  - Privoxy
  - 广告

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 分析</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_Privoxy"><span class="toc_number toc_depth_1">2</span> 设定 Privoxy 规则</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_Privoxy-2"><span class="toc_number toc_depth_1">3</span> 修改 Privoxy 监听地址</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">4</span> 更新</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    此前有人写邮件问我，Privoxy 如何去掉 iOS 上爱奇艺客户端的视频广告。当时我没时间，只大致给了几个建议，然后不了了之，没了下文。但心里记挂，想着什么时候有时间，要认真看看。所以就有了这一篇。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">分析</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    涉及的设备及软件等如下：
  </p>
  
  <ul>
    <li>
      iPhone 4s, 7.1.2 版本
    </li>
    <li>
      ThinkPad，装有 openSUSE 13.2 32 位操作系统
    </li>
    <li>
      Charles Proxy，收费的，Windows 系统下可以使用免费的 Fiddler2
    </li>
  </ul>
  
  <h3>
    预备工具
  </h3>
  
  <ol>
    <li>
      将 iPhone 与 ThinkPad 连入同一个 WIFI 环境
    </li>
    <li>
      打开 iPhone 的 WIFI 连接设置，设置 HTTP Proxy（代理）为 ThinkPad 上 Charles Proxy 的 ip:port，比如我的：<code>192.168.1.102:8888</code>，手机上如有开启 VPN 之类的，请暂先关闭
    </li>
  </ol>
  
  <p>
    现在查看 charles 的话，应该已经能看见 iPhone 上的 HTTP 请求/响应进出了。
  </p>
  
  <h3>
    打开爱奇艺客户端
  </h3>
  
  <p>
    现在打开爱奇艺客户端，点开一个视频，就能看到类似如下的请求：
  </p>
  
  <blockquote>
    <p>
      http://iface2.iqiyi.com/php/xyz/entry/nebula.php?key=8e48946f144759d86a50075555fd5862&app_key=8e48946f144759d86a50075555fd5862&did=b1f4b27f4627d038&type=json&id=&deviceid=&version=5.7.1&os=7.1.2&ua=iPhone4,1&network=1&screen_status=1&udid=aeb89eb1a451f9e6082246e79e077bc543e327ae&ss=1&ppid=&uid=&uniqid=0f607264fc6318a92b9e13c65db7cd3c&openudid=aeb89eb1a451f9e6082246e79e077bc543e327ae&idfv=5D1578BE-ECE1-406E-A99F-42AB99A71130&idfa=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&qyid=aeb89eb1a451f9e6082246e79e077bc543e327ae&mac_md5=e3f5536a141811db40efd6400f1d0a4e&cc=%257B%250A%2520%2520%2520%2520cc%2520%253D%2520%2522%255CU6d77%255CU5916%255CU8fd0%255CU8425%255CU5546%2522%253B%250A%2520%2520%2520%2520city%2520%253D%2520%2522%255CU6d77%255CU5916%2522%253B%250A%2520%2520%2520%2520province%2520%253D%2520%2522%255CU6d77%255CU5916%2522%253B%250A%2520%2520%2520%2520respcode%2520%253D%25200%253B%250A%2520%2520%2520%2520timeout%2520%253D%25200%253B%250A%257D&agenttype=20&screen_res=640<em>960&resolution=640</em>960&cookie=0&ppid=(null)&user_res=4&js=0&a=0&b=0&x=0&y=5&z=0&r=0&v_m=2.5_002&vs=0&vt=0.000000&other=1&block=0&ad=2&ad_str=1&w=0&compat=1&v5=1&core=0&sn=1420974668080402944&api=2.4&cts=1420974668&platform=iPhone&pps=0&support_db=&many_id=331794000_331794000_0
    </p>
  </blockquote>
  
  <p>
    广告就隐藏在这条请求的响应中：
  </p>
  
  <blockquote>
    <p>
      HTTP/1.1 200 OK
    </p>
    
    <p>
      Server: nginx
    </p>
    
    <p>
      Date: Sun, 11 Jan 2015 11:11:09 GMT
    </p>
    
    <p>
      Content-Type: text/json
    </p>
    
    <p>
      Connection: close
    </p>
    
    <p>
      X-Powered-By: PHP/5.3.6
    </p>
    
    <p>
      Vary: Accept-Encoding
    </p>
    
    <p>
      Expires: 0
    </p>
    
    <p>
      Cache-Control: no-cache
    </p>
  </blockquote>
  
  <blockquote>
    {&#8220;_as&#8221;:&#8221;&#8221;,&#8221;_blk&#8221;:0,&#8221;_cid&#8221;:4,&#8221;_ct&#8221;:&#8221;2014-12-05 16:35:45&#8243;,&#8221;_da&#8221;:&#8221;&#8221;,&#8221;_dl&#8221;:1,&#8221;_dn&#8221;:&#8221;219&#8243;,&#8221;_id&#8221;:&#8221;331794000&#8243;,&#8221;_img&#8221;:&#8221;http:\/\/pic8.qiyipic.com\/image\/20141205\/4e\/7f\/v_108765570_m_601_120_160.jpg&#8221;,&#8221;_ip&#8221;:0,&#8221;_ma&#8221;:&#8221;&#8221;,&#8221;_pc&#8221;:0,&#8221;_pid&#8221;:0,&#8221;_reseftv&#8221;:175,&#8221;_t&#8221;:&#8221;\u3010\u521d\u97f3miku\u3011\u30a2\u30ea\u30a2\u30c9\u30cd\u3010\u9ed2\u3046\u3055P\u3011&#8243;,&#8221;_tvct&#8221;:5,&#8221;_tvs&#8221;:1,&#8221;_vt&#8221;:12,&#8221;a_av&#8221;:1,&#8221;a_pro&#8221;:&#8221;&#8221;,&#8221;bpt&#8221;:&#8221;0&#8243;,&#8221;clm&#8221;:&#8221;&#8221;,&#8221;cn_year&#8221;:&#8221;0&#8243;,&#8221;co_album_id&#8221;:&#8221;0&#8243;,&#8221;ctype&#8221;:0,&#8221;desc&#8221;:&#8221;\u65e0&#8243;,&#8221;down&#8221;:3,&#8221;down2&#8243;:&#8221;3&#8243;,&#8221;drm&#8221;:0,&#8221;fst_time&#8221;:&#8221;2014-12-05&#8243;,&#8221;h1_img&#8221;:&#8221;http:\/\/pic8.qiyipic.com\/image\/20141205\/4e\/7f\/v_108765570_m_601_180_236.jpg&#8221;,&#8221;h2_img&#8221;:&#8221;http:\/\/pic8.qiyipic.com\/image\/20141205\/4e\/7f\/v_108765570_m_601_195_260.jpg&#8221;,&#8221;is_h&#8221;:0,&#8221;is_n&#8221;:0,&#8221;is_zb&#8221;:0,&#8221;k_word&#8221;:&#8221;&#8221;,&#8221;language&#8221;:0,&#8221;live_center&#8221;:0,&#8221;live_start_time&#8221;:0,&#8221;live_stop_time&#8221;:0,&#8221;logo&#8221;:1,&#8221;m_av&#8221;:1,&#8221;mts&#8221;:0,&#8221;p_av&#8221;:1,&#8221;p_s&#8221;:1,&#8221;p_s_1&#8243;:1,&#8221;p_s_4&#8243;:1,&#8221;p_s_8&#8243;:1,&#8221;qct&#8221;:25,&#8221;qiyi_pro&#8221;:0,&#8221;qiyi_year&#8221;:&#8221;0&#8243;,&#8221;qt_id&#8221;:&#8221;0&#8243;,&#8221;s_TT&#8221;:&#8221;sm25051115&#8243;,&#8221;songname&#8221;:&#8221;&#8221;,&#8221;t_pc&#8221;:0,&#8221;tag&#8221;:&#8221;\u65e5\u672c \u540c\u4eba ACG \u7279\u522b\u7248&#8243;,&#8221;tv_eftv&#8221;:1,&#8221;tv_pha&#8221;:&#8221;0&#8243;,&#8221;tv_pro&#8221;:&#8221;&#8221;,&#8221;tv_ss&#8221;:&#8221;0&#8243;,&#8221;tvfcs&#8221;:&#8221;\u7231\u5947\u827a\u7231\u52a8\u6f2b&#8221;,&#8221;up&#8221;:9,&#8221;up2&#8243;:&#8221;9&#8243;,&#8221;upcl&#8221;:&#8221;&#8221;,&#8221;v2_img&#8221;:&#8221;http:\/\/pic8.qiyipic.com\/image\/20141205\/4e\/7f\/v_108765570_m_601_284_160.jpg&#8221;,&#8221;v3_img&#8221;:&#8221;http:\/\/pic8.qiyipic.com\/image\/20141205\/4e\/7f\/v_108765570_m_601_480_270.jpg&#8221;,&#8221;vv&#8221;:&#8221;5403&#8243;,&#8221;year&#8221;:&#8221;2014&#8243;,&#8221;tv_id&#8221;:331794000,&#8221;vv_p&#8221;:61,&#8221;vv_f&#8221;:2,&#8221;vv_m&#8221;:39,&#8221;_sc&#8221;:7.5,&#8221;r_vv&#8221;:5403,&#8221;cpt_l&#8221;:0,&#8221;cpt_r&#8221;:0,&#8221;load_img&#8221;:&#8221;st&#8221;,&#8221;fst_time2&#8243;:&#8221;&#8221;,&#8221;disable&#8221;:0,&#8221;weburl&#8221;:&#8221;http:\/\/m.iqiyi.com\/v_19rrn82058.html&#8221;,&#8221;auth&#8221;:1,&#8221;auth_error&#8221;:0,&#8221;tv&#8221;:{&#8220;block&#8221;:[],&#8221;block_now&#8221;:&#8221;0&#8243;,&#8221;count&#8221;:1,&#8221;other&#8221;:[&#8220;331794000~331794000~\u3010\u521d\u97f3miku\u3011\u30a2\u30ea\u30a2\u30c9\u30cd\u3010\u9ed2\u3046\u3055P\u3011~1~2014~http:\/\/pic8.qiyipic.com\/image\/20141205\/4e\/7f\/v_108765570_m_601_160_90.jpg~~~~~~sm25051115~0~1~5403~http:\/\/pic8.qiyipic.com\/image\/20141205\/4e\/7f\/v_108765570_m_601_284_160.jpg~2014~2014-12-05~~~\u65e5\u672c \u540c\u4eba ACG \u7279\u522b\u7248~219~0~1~1~0~0~\u7231\u5947\u827a\u7231\u52a8\u6f2b~~~0~http:\/\/m.iqiyi.com\/v_19rrn82058.html~0~0~0~0~0&#8243;],&#8221;0&#8221;:{&#8220;_id&#8221;:&#8221;331794000&#8243;,&#8221;_n&#8221;:&#8221;\u3010\u521d\u97f3miku\u3011\u30a2\u30ea\u30a2\u30c9\u30cd\u3010\u9ed2\u3046\u3055P\u3011&#8243;,&#8221;desc&#8221;:&#8221;&#8221;,&#8221;_od&#8221;:1,&#8221;_dn&#8221;:219,&#8221;s_t&#8221;:-1,&#8221;e_t&#8221;:-1,&#8221;res&#8221;:[{&#8220;s&#8221;:1,&#8221;t&#8221;:&#8221;TS2&#8243;,&#8221;_v&#8221;:&#8221;e9898ca6870778b9a6f6a909fc763646&#8243;,&#8221;r_t&#8221;:&#8221;8&#8243;,&#8221;url&#8221;:&#8221;&#8221;,&#8221;len&#8221;:24230959,&#8221;vid&#8221;:&#8221;http:\/\/cache.m.iqiyi.com\/dc\/dt\/mobile\/20141205\/dd\/6d\/c495ecbe9e6cace8c70d627f97113b69.m3u8?qypid=331794000_32&qd_src=5be6a2fdfe4f4a1a8c7b08ee46a18887&qd_tm=1420974669000&qd_ip=104.200.18.10&qd_sc=41c33c35701ea3789da74f6233714380&#8243;,&#8221;fid&#8221;:&#8221;OEVB5H6VUDZNWECGMJKPU3KRH7XLIO6B&#8221;,&#8221;pps&#8221;:&#8221;0&#8243;,&#8221;pps_url&#8221;:&#8221;&#8221;,&#8221;uniq_id&#8221;:&#8221;100080001&#8243;,&#8221;_tsurl&#8221;:&#8221;&#8221;,&#8221;type&#8221;:1,&#8221;f4v_url&#8221;:&#8221;http:\/\/cache.video.qiyi.com\/vp\/331794000\/e9898ca6870778b9a6f6a909fc763646\/&#8221;},{&#8220;s&#8221;:2,&#8221;t&#8221;:&#8221;TS1&#8243;,&#8221;_v&#8221;:&#8221;bb620e84cffc480d53f85d8842697cee&#8221;,&#8221;r_t&#8221;:&#8221;4&#8243;,&#8221;url&#8221;:&#8221;&#8221;,&#8221;len&#8221;:11113689,&#8221;vid&#8221;:&#8221;http:\/\/cache.m.iqiyi.com\/dc\/dt\/mobile\/20141205\/95\/52\/cf82ab38c9949b20b2bf82ccab67777e.m3u8?qypid=331794000_32&qd_src=5be6a2fdfe4f4a1a8c7b08ee46a18887&qd_tm=1420974669000&qd_ip=104.200.18.10&qd_sc=c920c9a8c06403a72e0e149661aa683e&#8221;,&#8221;fid&#8221;:&#8221;34DSQJCHX6YW46NDC4KU7CVWZXCT5MVU&#8221;,&#8221;pps&#8221;:&#8221;0&#8243;,&#8221;pps_url&#8221;:&#8221;&#8221;,&#8221;uniq_id&#8221;:&#8221;100040001&#8243;,&#8221;_tsurl&#8221;:&#8221;&#8221;,&#8221;type&#8221;:1,&#8221;f4v_url&#8221;:&#8221;http:\/\/cache.video.qiyi.com\/vp\/331794000\/bb620e84cffc480d53f85d8842697cee\/&#8221;},{&#8220;s&#8221;:3,&#8221;t&#8221;:&#8221;TS4&#8243;,&#8221;_v&#8221;:&#8221;bd5ea43cdb556e035fa5ee99d2157e12&#8243;,&#8221;r_t&#8221;:&#8221;128&#8243;,&#8221;url&#8221;:&#8221;&#8221;,&#8221;len&#8221;:4673682,&#8221;vid&#8221;:&#8221;http:\/\/cache.m.iqiyi.com\/dc\/dt\/mobile\/20141205\/2a\/74\/4f64780f9f4524311fa367414d8e5666.m3u8?qypid=331794000_32&qd_src=5be6a2fdfe4f4a1a8c7b08ee46a18887&qd_tm=1420974669000&qd_ip=104.200.18.10&qd_sc=4fbf13db970809a4e16ac3270f17f688&#8243;,&#8221;fid&#8221;:&#8221;CXFDFGWWNA6NVMBD7RHLEY2X7DQK7QTE&#8221;,&#8221;pps&#8221;:&#8221;0&#8243;,&#8221;pps_url&#8221;:&#8221;&#8221;,&#8221;uniq_id&#8221;:&#8221;101280001&#8243;,&#8221;_tsurl&#8221;:&#8221;&#8221;,&#8221;type&#8221;:1,&#8221;f4v_url&#8221;:&#8221;http:\/\/cache.video.qiyi.com\/vp\/331794000\/bd5ea43cdb556e035fa5ee99d2157e12\/&#8221;}],&#8221;len&#8221;:11113689,&#8221;vid&#8221;:&#8221;http:\/\/cache.m.iqiyi.com\/dc\/dt\/mobile\/20141205\/95\/52\/cf82ab38c9949b20b2bf82ccab67777e.m3u8?qypid=331794000_32&qd_src=5be6a2fdfe4f4a1a8c7b08ee46a18887&qd_tm=1420974669000&qd_ip=104.200.18.10&qd_sc=c920c9a8c06403a72e0e149661aa683e&#8221;,&#8221;url&#8221;:&#8221;&#8221;,&#8221;_img&#8221;:&#8221;http:\/\/pic8.qiyipic.com\/image\/20141205\/4e\/7f\/v_108765570_m_601_160_90.jpg&#8221;,&#8221;web_url&#8221;:&#8221;http:\/\/m.iqiyi.com\/v_19rrn82058.html&#8221;,&#8221;albumid&#8221;:&#8221;331794000&#8243;,&#8221;subtitle&#8221;:&#8221;sm25051115&#8243;,&#8221;comment_on&#8221;:1,&#8221;_dv&#8221;:&#8221;e9898ca6870778b9a6f6a909fc763646&#8243;,&#8221;vote_id&#8221;:&#8221;&#8221;,&#8221;_durl&#8221;:&#8221;http:\/\/data.video.qiyi.com\/videos\/v0\/20141205\/3d\/e7\/5d6c11ae9b1d465afd506c5fefbe4559.mp4?qypid=331794000_32&v=827122190&qd_src=app&qd_tm=1420974669000&qd_ip=104.200.18.10&qd_sc=92f4366fcb5a64db3c00a706388d7fe2&#8243;,&#8221;_dlen&#8221;:11971286,&#8221;pps&#8221;:&#8221;0&#8243;,&#8221;fid&#8221;:&#8221;34DSQJCHX6YW46NDC4KU7CVWZXCT5MVU&#8221;,&#8221;_res&#8221;:&#8221;4&#8243;,&#8221;_v&#8221;:&#8221;bb620e84cffc480d53f85d8842697cee&#8221;,&#8221;pps_url&#8221;:&#8221;&#8221;,&#8221;f4v_url&#8221;:&#8221;http:\/\/cache.video.qiyi.com\/vp\/331794000\/bb620e84cffc480d53f85d8842697cee\/&#8221;,&#8221;ad_str&#8221;:&#8221;{\&#8221;ip\&#8221;:\&#8221;10.11.49.120\&#8221;,\&#8221;cupidExtras\&#8221;:{\&#8221;enableMiaozhenSDK\&#8221;:1,\&#8221;enableAdMasterSDK\&#8221;:1,\&#8221;enableAlimama\&#8221;:0,\&#8221;enableMmaMiaozhen\&#8221;:1,\&#8221;enableMmaCtr\&#8221;:1,\&#8221;alimamaId\&#8221;:71000017,\&#8221;enableMmaNielsen\&#8221;:1,\&#8221;enableMmaAdMaster\&#8221;:1},\&#8221;futureSlots\&#8221;:[{\&#8221;startTime\&#8221;:300,\&#8221;type\&#8221;:4}],\&#8221;reqUrl\&#8221;:\&#8221;\\\/mixer?a=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&b=331794000&c=bb620e84cffc480d53f85d8842697cee&d=qc_100001_100070&e=5.7.1&f=4&g=104.200.18.10&h=331794000&i=iPhone&k=4&l=8e48946f144759d86a50075555fd5862&m=iPhone4%2C1&n=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&o=0b05078afb5a24f5f97fadac83632383&vn=0&vd=0&r=2.5_002&rn=0&bd=219&p=-1&x=0&tp=0&nw=1&vs=0&pi=&pc=0&cts=1420974668&lts=&y=103,1,2&fa=4&ut=0\&#8221;,\&#8221;version\&#8221;:\&#8221;2.0.8526\&#8221;,\&#8221;adSlots\&#8221;:[{\&#8221;startTime\&#8221;:0,\&#8221;duration\&#8221;:30,\&#8221;type\&#8221;:1,\&#8221;slotExtras\&#8221;:{},\&#8221;adZoneId\&#8221;:\&#8221;1000000000381\&#8221;,\&#8221;ads\&#8221;:[{\&#8221;adExtras\&#8221;:{},\&#8221;clickTracking\&#8221;:{\&#8221;adxTracking\&#8221;:[\&#8221;http:\\\/\\\/api.cupid.qiyi.com\\\/etx?i=qc_100001_100070&f=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&q=5000000678217&v=CAASEGseMM8pVUkpiJFs6m_FE1YaIDlhZTlmN2FkN2I4MzFiMDEyZjkwZjIxMzkyNTlhZmNj&c=1a9d6aa5607c24198908e4ecb7f36971&k=331794000&j=4&d=81000009&z=1000000000381&ds=71000001&du=15&n=331794000&g=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&o=1&e=104.200.18.10&l=8e48946f144759d86a50075555fd5862&r=0b05078afb5a24f5f97fadac83632383&a=1&b=1420974669\&#8221;],\&#8221;cupidTracking\&#8221;:[\&#8221;http:\\\/\\\/api.cupid.qiyi.com\\\/track2?a=1&b=1420974669&c=1a9d6aa5607c24198908e4ecb7f36971&d=5000000675829&e=104.200.18.10&f=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&g=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&h=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&i=qc_100001_100070&j=4&k=331794000&kp=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&l=8e48946f144759d86a50075555fd5862&m=iPhone4,1&n=331794000&o=1&p=1000000000381&q=5000000678217&r=0b05078afb5a24f5f97fadac83632383&s=dafea75e967cef6a25e0060b5aefbeb4&t=iPhone&u=1&w=2&up=&v=5000000675829\&#8221;]},\&#8221;impressionId\&#8221;:\&#8221;1a9d6aa5607c24198908e4ecb7f36971\&#8221;,\&#8221;vid\&#8221;:\&#8221;327d76cda8d3e7c29a41a52f1cb41ff8\&#8221;,\&#8221;priority\&#8221;:88,\&#8221;dspId\&#8221;:71000001,\&#8221;order\&#8221;:1,\&#8221;duration\&#8221;:15,\&#8221;clickThroughUrl\&#8221;:\&#8221;http:\\\/\\\/wt.game.pps.tv\\\/index.php?m=adsmd&c=tiepian&a=index&id=7421\&#8221;,\&#8221;impressionTracking\&#8221;:{\&#8221;adxTracking\&#8221;:[\&#8221;http:\\\/\\\/api.cupid.qiyi.com\\\/etx?i=qc_100001_100070&f=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&q=5000000678217&v=CAASEGseMM8pVUkpiJFs6m_FE1YaIDlhZTlmN2FkN2I4MzFiMDEyZjkwZjIxMzkyNTlhZmNj&c=1a9d6aa5607c24198908e4ecb7f36971&k=331794000&j=4&d=81000009&z=1000000000381&ds=71000001&du=15&n=331794000&g=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&o=1&e=104.200.18.10&l=8e48946f144759d86a50075555fd5862&r=0b05078afb5a24f5f97fadac83632383&a=0&b=1420974669\&#8221;],\&#8221;cupidTracking\&#8221;:[\&#8221;http:\\\/\\\/api.cupid.qiyi.com\\\/track2?a=0&b=1420974669&c=1a9d6aa5607c24198908e4ecb7f36971&d=5000000675829&e=104.200.18.10&f=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&g=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&h=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&i=qc_100001_100070&j=4&k=331794000&kp=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&l=8e48946f144759d86a50075555fd5862&m=iPhone4,1&n=331794000&o=1&p=1000000000381&q=5000000678217&r=0b05078afb5a24f5f97fadac83632383&s=dafea75e967cef6a25e0060b5aefbeb4&t=iPhone&u=1&w=2&up=&v=5000000675829\&#8221;]},\&#8221;creativeType\&#8221;:\&#8221;video_m3u8\&#8221;,\&#8221;clickThroughType\&#8221;:\&#8221;0\&#8221;,\&#8221;orderItemId\&#8221;:\&#8221;5000000675829\&#8221;,\&#8221;timePosition\&#8221;:\&#8221;2\&#8221;,\&#8221;adId\&#8221;:\&#8221;5000000677723\&#8221;,\&#8221;creativeObject\&#8221;:{},\&#8221;creativeUrl\&#8221;:\&#8221;\&#8221;,\&#8221;creativeId\&#8221;:\&#8221;5000000678217\&#8221;},{\&#8221;adExtras\&#8221;:{},\&#8221;clickTracking\&#8221;:{\&#8221;adxTracking\&#8221;:[\&#8221;http:\\\/\\\/api.cupid.qiyi.com\\\/etx?i=qc_100001_100070&f=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&q=5000000591849&v=CAASEGseMM8pVUkpiJFs6m_FE1YaIDlhZTlmN2FkN2I4MzFiMDEyZjkwZjIxMzkyNTlhZmNj&c=84e5330e3497a4c52b4ecfcd84e98f05&k=331794000&j=4&d=81000009&z=1000000000381&ds=71000001&du=15&n=331794000&g=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&o=1&e=104.200.18.10&l=8e48946f144759d86a50075555fd5862&r=0b05078afb5a24f5f97fadac83632383&a=1&b=1420974669\&#8221;],\&#8221;cupidTracking\&#8221;:[\&#8221;http:\\\/\\\/api.cupid.qiyi.com\\\/track2?a=1&b=1420974669&c=84e5330e3497a4c52b4ecfcd84e98f05&d=5000000589321&e=104.200.18.10&f=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&g=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&h=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&i=qc_100001_100070&j=4&k=331794000&kp=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&l=8e48946f144759d86a50075555fd5862&m=iPhone4,1&n=331794000&o=1&p=1000000000381&q=5000000591849&r=0b05078afb5a24f5f97fadac83632383&s=ddfc1cc2443276e5f8a2ea298a7774a8&t=iPhone&u=1&w=3&up=&v=5000000589321\&#8221;]},\&#8221;impressionId\&#8221;:\&#8221;84e5330e3497a4c52b4ecfcd84e98f05\&#8221;,\&#8221;vid\&#8221;:\&#8221;7d1bf186a55a5ae0bb2ad051666adb89\&#8221;,\&#8221;priority\&#8221;:88,\&#8221;dspId\&#8221;:71000001,\&#8221;order\&#8221;:2,\&#8221;duration\&#8221;:15,\&#8221;clickThroughUrl\&#8221;:\&#8221;http:\\\/\\\/serv.vip.iqiyi.com\\\/order\\\/preview.action?pid=a0226bd958843452&platform=bb35a104d95490f6&fc=a3dbfe9e7b9dba94#type=0\&#8221;,\&#8221;impressionTracking\&#8221;:{\&#8221;adxTracking\&#8221;:[\&#8221;http:\\\/\\\/api.cupid.qiyi.com\\\/etx?i=qc_100001_100070&f=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&q=5000000591849&v=CAASEGseMM8pVUkpiJFs6m_FE1YaIDlhZTlmN2FkN2I4MzFiMDEyZjkwZjIxMzkyNTlhZmNj&c=84e5330e3497a4c52b4ecfcd84e98f05&k=331794000&j=4&d=81000009&z=1000000000381&ds=71000001&du=15&n=331794000&g=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&o=1&e=104.200.18.10&l=8e48946f144759d86a50075555fd5862&r=0b05078afb5a24f5f97fadac83632383&a=0&b=1420974669\&#8221;],\&#8221;cupidTracking\&#8221;:[\&#8221;http:\\\/\\\/api.cupid.qiyi.com\\\/track2?a=0&b=1420974669&c=84e5330e3497a4c52b4ecfcd84e98f05&d=5000000589321&e=104.200.18.10&f=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&g=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&h=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&i=qc_100001_100070&j=4&k=331794000&kp=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&l=8e48946f144759d86a50075555fd5862&m=iPhone4,1&n=331794000&o=1&p=1000000000381&q=5000000591849&r=0b05078afb5a24f5f97fadac83632383&s=ddfc1cc2443276e5f8a2ea298a7774a8&t=iPhone&u=1&w=3&up=&v=5000000589321\&#8221;]},\&#8221;creativeType\&#8221;:\&#8221;video_m3u8\&#8221;,\&#8221;clickThroughType\&#8221;:\&#8221;3\&#8221;,\&#8221;orderItemId\&#8221;:\&#8221;5000000589321\&#8221;,\&#8221;timePosition\&#8221;:\&#8221;3\&#8221;,\&#8221;adId\&#8221;:\&#8221;5000000591634\&#8221;,\&#8221;creativeObject\&#8221;:{},\&#8221;creativeUrl\&#8221;:\&#8221;\&#8221;,\&#8221;creativeId\&#8221;:\&#8221;5000000591849\&#8221;}]}],\&#8221;videoEventId\&#8221;:\&#8221;0b05078afb5a24f5f97fadac83632383\&#8221;,\&#8221;finalUrl\&#8221;:\&#8221;http:\\\/\\\/cache.m.iqiyi.com\\\/dc\\\/amdt\\\/ae7578x3cd43d3f\\\/327d76cda8d3e7c29a41a52f1cb41ff8-7d1bf186a55a5ae0bb2ad051666adb89\\\/331794000\\\/bb620e84cffc480d53f85d8842697cee.m3u8?qd_asc=ae4f1fc1098e13132ea08c9490e419ee&qd_asrc=8c40568b52a2483ea7e88a948c7ed664&qd_at=1420974669569&qypid=331794000_32\&#8221;}&#8221;}},&#8221;sn&#8221;:&#8221;1420974668080402944&#8243;,&#8221;_tab&#8221;:[{&#8220;id&#8221;:2,&#8221;name&#8221;:&#8221;\u8be6\u60c5\u8bc4\u8bba&#8221;,&#8221;default&#8221;:0},{&#8220;id&#8221;:3,&#8221;name&#8221;:&#8221;\u731c\u4f60\u559c\u6b22&#8243;,&#8221;default&#8221;:1}],&#8221;cupid_app_on&#8221;:1,&#8221;cupid_app_tab&#8221;:3,&#8221;_av&#8221;:1,&#8221;album_barrage&#8221;:1,&#8221;album_barrage_lines&#8221;:3,&#8221;cupid_ut&#8221;:0,&#8221;cupid_nw&#8221;:1,&#8221;cupid_expire&#8221;:3}
  </blockquote>
  
  <p>
    以上是请求的原始响应报文，可以借用 charles 提供的 JSON 方式查看：
  </p>
  
  <p>
    [resp_image id=&#8217;14942&#8242; caption=&#8221; ]
  </p>
  
  <p>
    由于对 iOS 上视频播放的机制并不熟悉，所以我只能一个一个测试过去，然后大致了解返回的数据是什么意思：
  </p>
  
  <ul>
    <li>
      <code>tv</code> 键名下有个 <code>res</code>，里面有三个对象，包含的是三个清晰度的视频版本，其中有视频路径，格式为 m3u8，比如 <code>http://cache.m.iqiyi.com/dc/dt/mobile/20141205/dd/6d/c495ecbe9e6cace8c70d627f97113b69.m3u8?qypid=331794000_32&qd_src=5be6a2fdfe4f4a1a8c7b08ee46a18887&qd_tm=1420974669000&qd_ip=104.200.18.10&qd_sc=41c33c35701ea3789da74f6233714380</code>，在浏览器中打开这个路径，就可以下载 m3u8 文件，然后用 mplayer 等工具即可播放，借助 ffmpeg 工具也可以将它下载到本地。
    </li>
    <li>
      <code>tab</code> 键名下有两个对象，包含是的”详情评论“和”猜你喜欢“，这是视频下的两个标签页。
    </li>
  </ul>
  
  <p>
    经过排查，大致锁定一个叫 <code>ad_str</code> 的键名，其值如下：
  </p>
  
  <blockquote>
    <p>
      {&#8220;ip&#8221;:&#8221;10.11.49.120&#8243;,&#8221;cupidExtras&#8221;:{&#8220;enableMiaozhenSDK&#8221;:1,&#8221;enableAdMasterSDK&#8221;:1,&#8221;enableAlimama&#8221;:0,&#8221;enableMmaMiaozhen&#8221;:1,&#8221;enableMmaCtr&#8221;:1,&#8221;alimamaId&#8221;:71000017,&#8221;enableMmaNielsen&#8221;:1,&#8221;enableMmaAdMaster&#8221;:1},&#8221;futureSlots&#8221;:[{&#8220;startTime&#8221;:300,&#8221;type&#8221;:4}],&#8221;reqUrl&#8221;:&#8221;\/mixer?a=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&b=331794000&c=bb620e84cffc480d53f85d8842697cee&d=qc_100001_100070&e=5.7.1&f=4&g=104.200.18.10&h=331794000&i=iPhone&k=4&l=8e48946f144759d86a50075555fd5862&m=iPhone4%2C1&n=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&o=0b05078afb5a24f5f97fadac83632383&vn=0&vd=0&r=2.5_002&rn=0&bd=219&p=-1&x=0&tp=0&nw=1&vs=0&pi=&pc=0&cts=1420974668&lts=&y=103,1,2&fa=4&ut=0&#8243;,&#8221;version&#8221;:&#8221;2.0.8526&#8243;,&#8221;adSlots&#8221;:[{&#8220;startTime&#8221;:0,&#8221;duration&#8221;:30,&#8221;type&#8221;:1,&#8221;slotExtras&#8221;:{},&#8221;adZoneId&#8221;:&#8221;1000000000381&#8243;,&#8221;ads&#8221;:[{&#8220;adExtras&#8221;:{},&#8221;clickTracking&#8221;:{&#8220;adxTracking&#8221;:[&#8220;http:\/\/api.cupid.qiyi.com\/etx?i=qc_100001_100070&f=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&q=5000000678217&v=CAASEGseMM8pVUkpiJFs6m_FE1YaIDlhZTlmN2FkN2I4MzFiMDEyZjkwZjIxMzkyNTlhZmNj&c=1a9d6aa5607c24198908e4ecb7f36971&k=331794000&j=4&d=81000009&z=1000000000381&ds=71000001&du=15&n=331794000&g=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&o=1&e=104.200.18.10&l=8e48946f144759d86a50075555fd5862&r=0b05078afb5a24f5f97fadac83632383&a=1&b=1420974669&#8243;],&#8221;cupidTracking&#8221;:[&#8220;http:\/\/api.cupid.qiyi.com\/track2?a=1&b=1420974669&c=1a9d6aa5607c24198908e4ecb7f36971&d=5000000675829&e=104.200.18.10&f=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&g=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&h=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&i=qc_100001_100070&j=4&k=331794000&kp=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&l=8e48946f144759d86a50075555fd5862&m=iPhone4,1&n=331794000&o=1&p=1000000000381&q=5000000678217&r=0b05078afb5a24f5f97fadac83632383&s=dafea75e967cef6a25e0060b5aefbeb4&t=iPhone&u=1&w=2&up=&v=5000000675829&#8243;]},&#8221;impressionId&#8221;:&#8221;1a9d6aa5607c24198908e4ecb7f36971&#8243;,&#8221;vid&#8221;:&#8221;327d76cda8d3e7c29a41a52f1cb41ff8&#8243;,&#8221;priority&#8221;:88,&#8221;dspId&#8221;:71000001,&#8221;order&#8221;:1,&#8221;duration&#8221;:15,&#8221;clickThroughUrl&#8221;:&#8221;http:\/\/wt.game.pps.tv\/index.php?m=adsmd&c=tiepian&a=index&id=7421&#8243;,&#8221;impressionTracking&#8221;:{&#8220;adxTracking&#8221;:[&#8220;http:\/\/api.cupid.qiyi.com\/etx?i=qc_100001_100070&f=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&q=5000000678217&v=CAASEGseMM8pVUkpiJFs6m_FE1YaIDlhZTlmN2FkN2I4MzFiMDEyZjkwZjIxMzkyNTlhZmNj&c=1a9d6aa5607c24198908e4ecb7f36971&k=331794000&j=4&d=81000009&z=1000000000381&ds=71000001&du=15&n=331794000&g=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&o=1&e=104.200.18.10&l=8e48946f144759d86a50075555fd5862&r=0b05078afb5a24f5f97fadac83632383&a=0&b=1420974669&#8243;],&#8221;cupidTracking&#8221;:[&#8220;http:\/\/api.cupid.qiyi.com\/track2?a=0&b=1420974669&c=1a9d6aa5607c24198908e4ecb7f36971&d=5000000675829&e=104.200.18.10&f=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&g=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&h=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&i=qc_100001_100070&j=4&k=331794000&kp=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&l=8e48946f144759d86a50075555fd5862&m=iPhone4,1&n=331794000&o=1&p=1000000000381&q=5000000678217&r=0b05078afb5a24f5f97fadac83632383&s=dafea75e967cef6a25e0060b5aefbeb4&t=iPhone&u=1&w=2&up=&v=5000000675829&#8243;]},&#8221;creativeType&#8221;:&#8221;video_m3u8&#8243;,&#8221;clickThroughType&#8221;:&#8221;0&#8243;,&#8221;orderItemId&#8221;:&#8221;5000000675829&#8243;,&#8221;timePosition&#8221;:&#8221;2&#8243;,&#8221;adId&#8221;:&#8221;5000000677723&#8243;,&#8221;creativeObject&#8221;:{},&#8221;creativeUrl&#8221;:&#8221;&#8221;,&#8221;creativeId&#8221;:&#8221;5000000678217&#8243;},{&#8220;adExtras&#8221;:{},&#8221;clickTracking&#8221;:{&#8220;adxTracking&#8221;:[&#8220;http:\/\/api.cupid.qiyi.com\/etx?i=qc_100001_100070&f=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&q=5000000591849&v=CAASEGseMM8pVUkpiJFs6m_FE1YaIDlhZTlmN2FkN2I4MzFiMDEyZjkwZjIxMzkyNTlhZmNj&c=84e5330e3497a4c52b4ecfcd84e98f05&k=331794000&j=4&d=81000009&z=1000000000381&ds=71000001&du=15&n=331794000&g=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&o=1&e=104.200.18.10&l=8e48946f144759d86a50075555fd5862&r=0b05078afb5a24f5f97fadac83632383&a=1&b=1420974669&#8243;],&#8221;cupidTracking&#8221;:[&#8220;http:\/\/api.cupid.qiyi.com\/track2?a=1&b=1420974669&c=84e5330e3497a4c52b4ecfcd84e98f05&d=5000000589321&e=104.200.18.10&f=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&g=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&h=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&i=qc_100001_100070&j=4&k=331794000&kp=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&l=8e48946f144759d86a50075555fd5862&m=iPhone4,1&n=331794000&o=1&p=1000000000381&q=5000000591849&r=0b05078afb5a24f5f97fadac83632383&s=ddfc1cc2443276e5f8a2ea298a7774a8&t=iPhone&u=1&w=3&up=&v=5000000589321&#8243;]},&#8221;impressionId&#8221;:&#8221;84e5330e3497a4c52b4ecfcd84e98f05&#8243;,&#8221;vid&#8221;:&#8221;7d1bf186a55a5ae0bb2ad051666adb89&#8243;,&#8221;priority&#8221;:88,&#8221;dspId&#8221;:71000001,&#8221;order&#8221;:2,&#8221;duration&#8221;:15,&#8221;clickThroughUrl&#8221;:&#8221;http:\/\/serv.vip.iqiyi.com\/order\/preview.action?pid=a0226bd958843452&platform=bb35a104d95490f6&fc=a3dbfe9e7b9dba94#type=0&#8243;,&#8221;impressionTracking&#8221;:{&#8220;adxTracking&#8221;:[&#8220;http:\/\/api.cupid.qiyi.com\/etx?i=qc_100001_100070&f=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&q=5000000591849&v=CAASEGseMM8pVUkpiJFs6m_FE1YaIDlhZTlmN2FkN2I4MzFiMDEyZjkwZjIxMzkyNTlhZmNj&c=84e5330e3497a4c52b4ecfcd84e98f05&k=331794000&j=4&d=81000009&z=1000000000381&ds=71000001&du=15&n=331794000&g=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&o=1&e=104.200.18.10&l=8e48946f144759d86a50075555fd5862&r=0b05078afb5a24f5f97fadac83632383&a=0&b=1420974669&#8243;],&#8221;cupidTracking&#8221;:[&#8220;http:\/\/api.cupid.qiyi.com\/track2?a=0&b=1420974669&c=84e5330e3497a4c52b4ecfcd84e98f05&d=5000000589321&e=104.200.18.10&f=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&g=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&h=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&i=qc_100001_100070&j=4&k=331794000&kp=EAA3CC99-FAB0-46CC-B1A0-67B9BA89BB7F&l=8e48946f144759d86a50075555fd5862&m=iPhone4,1&n=331794000&o=1&p=1000000000381&q=5000000591849&r=0b05078afb5a24f5f97fadac83632383&s=ddfc1cc2443276e5f8a2ea298a7774a8&t=iPhone&u=1&w=3&up=&v=5000000589321&#8243;]},&#8221;creativeType&#8221;:&#8221;video_m3u8&#8243;,&#8221;clickThroughType&#8221;:&#8221;3&#8243;,&#8221;orderItemId&#8221;:&#8221;5000000589321&#8243;,&#8221;timePosition&#8221;:&#8221;3&#8243;,&#8221;adId&#8221;:&#8221;5000000591634&#8243;,&#8221;creativeObject&#8221;:{},&#8221;creativeUrl&#8221;:&#8221;&#8221;,&#8221;creativeId&#8221;:&#8221;5000000591849&#8243;}]}],&#8221;videoEventId&#8221;:&#8221;0b05078afb5a24f5f97fadac83632383&#8243;,&#8221;finalUrl&#8221;:&#8221;http:\/\/cache.m.iqiyi.com\/dc\/amdt\/ae7578x3cd43d3f\/327d76cda8d3e7c29a41a52f1cb41ff8-7d1bf186a55a5ae0bb2ad051666adb89\/331794000\/bb620e84cffc480d53f85d8842697cee.m3u8?qd_asc=ae4f1fc1098e13132ea08c9490e419ee&qd_asrc=8c40568b52a2483ea7e88a948c7ed664&qd_at=1420974669569&qypid=331794000_32&#8243;}
    </p>
  </blockquote>
  
  <p>
    又一段非常长的文本，我想你我都懒得看内容了 &#8211; 不过拜语义化带来的好处，我们一眼就能从 <code>ad_str</code> 里判断它可能是广告入口。且在 Privoxy 里换掉它试试。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Privoxy">设定 Privoxy 规则</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Privoxy" href="#_Privoxy"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    因为是过滤文本，所以要涉及 Privoxy 的两个文件：
  </p>
  
  <ul>
    <li>
      user.filter
    </li>
    <li>
      user.action
    </li>
  </ul>
  
  <ol>
    <li>
      <p>
        首先在 user.filter 文件中添加如下规则：
      </p>
      
      <pre><code>FILTER: blockQiyiAd 去除爱奇艺 iOS 版本视频广告
s|"ad_str"|"fuck_ad_str"|g
</code></pre>
      
      <p>
        这里，我创建了一条规则，把 <code>ad_str</code> 键名替换掉。
      </p>
    </li>
    
    <li>
      <p>
        然后在 user.action 文件中启用过滤规则：
      </p>
      
      <pre><code>{+filter{blockQiyiAd}}
iface2.iqiyi.com
</code></pre>
      
      <p>
        再开启爱奇艺的客户端，视频广告已经不见。感谢语义，蒙对了。目前来看，也没有其他引发异常的副作用。
      </p>
    </li>
  </ol>
  
  <h2 class="storycontent-h2">
    <span id="_Privoxy-2">修改 Privoxy 监听地址</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Privoxy-2" href="#_Privoxy-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    上面说明的是开启 charles 的情况，一旦 charles 关闭，我们就要把 iPhone 上的 HTTP PROXY 改为电脑上的 Privoxy 端口，比如 <code>192.168.1.102:8118</code>。
  </p>
  
  <p>
    但 Privoxy 默认监听的地址是 <code>127.0.0.1:8118</code>，如果不做修改，会导致 iPhone 设置的 HTTP 代理无法访问。所以我新增一个 Privoxy 的监听地址。
  </p>
  
  <p>
    打开 <code>config</code> 文件，查找 <code>listen-address  127.0.0.1:8118</code>，在它下一行新增如下内容：
  </p>
  
  <pre><code>listen-address  192.168.1.102:8118
</code></pre>
  
  <p>
    其中 192.168.1.102 是我笔记本电脑的 IP。
  </p>
  
  <p>
    最后，重启 Privoxy。
  </p>
  
  <p>
    更多规则，请看我维护的 <a href="https://github.com/chenxsan/Privoxy">Privoxy 配置文件库</a>。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">更新</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    2015.2.8 爱奇艺把 &#8216;ad_str&#8217; 换成 &#8216;ad_info&#8217; 了，配置文件已更新。
  </p>
</div>