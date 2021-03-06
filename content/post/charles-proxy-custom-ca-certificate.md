---
title: Charles Proxy 自定义 CA 证书
author: 陈 三
layout: post
date: 2015-01-25T05:17:28+00:00
url: /charles-proxy-custom-ca-certificate.html
views:
  - 1331
categories:
  - Firefox
  - openSUSE
tags:
  - Charles Proxy
  - HTTPS

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_CA"><span class="toc_number toc_depth_1">1</span> 自建 CA 证书</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_charles"><span class="toc_number toc_depth_1">2</span> 配置 charles</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_Firefox"><span class="toc_number toc_depth_1">3</span> 导入证书到 Firefox</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    <a href="http://www.charlesproxy.com/documentation/using-charles/ssl-certificates/">Charles Proxy</a> 跟 Windows 平台下的 <a href="http://www.telerik.com/fiddler">Fiddler</a> 一样可以查看 HTTPS 流量，但使用 Charles 官方提供的 <a href="http://www.charlesproxy.com/documentation/using-charles/ssl-certificates/">CA 证书</a>检查 HTTPS 请求时，Firefox 35 下网页会出现如下错误：
  </p>
  
  <blockquote>
    <p>
      twitter.com uses an invalid security certificate. The certificate is not trusted because the issuer certificate has expired. (Error code: sec_error_expired_issuer_certificate)
    </p>
  </blockquote>
  
  <p>
    <a href="https://muffinresearch.co.uk/proxying-connections-from-ffos/">据说</a>原因是这样的：
  </p>
  
  <blockquote>
    <p>
      The more recent versions of Firefox only allow certs with start dates after the unix epoch (1st Jan 1970). As the Charles CA cert has a start year of 1899 it&#8217;s seen as expired.
    </p>
  </blockquote>
  
  <p>
    最新版本的 Firefox 只允许证书的起始时间在 1970 以后，而 Charles CA 证书的起始时间是 1899。
  </p>
  
  <p>
    解决办法是<a href="http://0x74696d.com/posts/CharlesSSL/">自建一个证书</a>。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_CA">自建 CA 证书</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_CA" href="#_CA"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    我的过程基于 openSUSE 13.2 操作系统。
  </p>
  
  <ol>
    <li>
      <p>
        逐行执行以下命令（openSUSE 下需要管理员权限）。
      </p>
      
      <pre><code>mkdir -p /usr/local/CharlesCA
cd /usr/local/CharlesCA
mkdir certs private newcerts
echo 01 &gt; serial
touch index.txt
</code></pre>
    </li>
    
    <li>
      <p>
        生成 CA 证书
      </p>
      
      <pre><code>openssl req -new -x509 -days 3650 -extensions v3_ca \
-keyout private/ca_key.pem -out certs/ca_cert.pem \
-config /etc/ssl/openssl.cnf
</code></pre>
      
      <p>
        请注意 <code>-config</code> 后指向的路径，这里是我 openSUSE 下 openssl.cnf 文件路径，请根据自己的操作系统确认其路径。
      </p>
      
      <p>
        这一步中也会要求填写 <code>passphrase</code> 及其它信息，<code>passphrase</code> 后面在 Charles 中会用到。
      </p>
    </li>
    
    <li>
      <p>
        转换为 PKCS12 格式
      </p>
      
      <p>
        因为 Charles 需要 pkcs12 格式的证书，所以还需要做个转换：
      </p>
      
      <pre><code>openssl pkcs12 -export -out ca_cert.pfx -inkey private/ca_key.pem -in certs/ca_cert.pem
</code></pre>
      
      <p>
        这样，/usr/local/CharlesCA 目录下会生成 ca_cert.pfx 文件。
      </p>
    </li>
  </ol>
  
  <p>
    我们总共得到了 3 个重要的文件：
  </p>
  
  <ul>
    <li>
      ca_cert.pfx &#8211; charles 添加自定义证书用的
    </li>
    <li>
      ca_cert.pem &#8211; 提供给客户端使用的
    </li>
    <li>
      ca_key.pem &#8211; 钥匙（请保证它的安全）
    </li>
  </ul>
  
  <h2 class="storycontent-h2">
    <span id="_charles">配置 charles</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_charles" href="#_charles"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      打开 charles -> Proxy -> Proxy Settings&#8230; 菜单
    </li>
    <li>
      点击 SSL 标签页
    </li>
    <li>
      勾选 &#8216;Use a custom CA certificate&#8217;
    </li>
    <li>
      点击 <kbd>Choose</kbd> 按键，选择 <code>/usr/local/CharlesCA/ca_cert.pfx</code> 文件
    </li>
  </ol>
  
  <p>
    这样就配置好 charles 的证书。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Firefox">导入证书到 Firefox</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Firefox" href="#_Firefox"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      打开 Firefox -> Preferences
    </li>
    <li>
      选择 Advanced -> Certificates 标签页
    </li>
    <li>
      点击 <kbd>View certificates</kbd>
    </li>
    <li>
      点击 <kbd>Import...</kbd>
    </li>
    <li>
      定位到 <code>/usr/local/CharlesCA/certs/ca_cert.pem</code> 文件
    </li>
    <li>
      勾选 &#8216;This certificate can identify websites&#8217;
    </li>
    <li>
      确认
    </li>
  </ol>
  
  <p>
    最后重启 Charles，会弹窗口要求填写上面创建证书时设置的 passphrase。之后 https 流量可以正常分析了。
  </p>
</div>