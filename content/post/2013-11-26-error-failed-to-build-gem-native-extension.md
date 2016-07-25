---
title: 'ERROR: Failed to build gem native extension'
author: 陈 三
layout: post
date: 2013-11-25T22:05:44+00:00
url: /error-failed-to-build-gem-native-extension.html
dsq_thread_id:
  - 2008557031
views:
  - 846
categories:
  - openSUSE
tags:
  - openSUSE
  - ruby
  - Ruby on Rails

---
[Ruby on Rails][1] 网站上说，安装好 Ruby 后运行 `gem install rails` 就好了。

但整个过程折腾了我好几个小时。首先，openSUSE 13.1 自带有 Ruby 2.0.0p-247，我因为打算用 rbenv 管理 Ruby，就草率地把 Ruby 卸载：

    $ sudo zypper rm ruby
    

结果 Konsole 没了，YAST 没了，似乎连着 KDE 桌面都被卸掉。

那么就先将就用系统自带的吧。但 `gem install rails` 报错了：

> Building native extensions. This could take a while&#8230;
> 
> ERROR: Error installing rails:
> 
> ERROR: Failed to build gem native extension.
> 
> /usr/bin/ruby2.0 extconf.rb
> 
> mkmf.rb can&#8217;t find header files for ruby at /usr/lib/ruby/include/ruby.h
> 
> Gem files will remain installed in /usr/lib/ruby/gems/2.0.0/gems/atomic-1.1.14 for inspection.
> 
> Results logged to /usr/lib/ruby/gems/2.0.0/gems/atomic-1.1.14/ext/gem_make.out

`gem install compass` 却是没有任何问题。

网上的资料说要安装 ruby-devel：

    sudo zypper in ruby-devel
    

再次安装 Rails，如你所见，从我开始写这篇到现在，还在安装中。但后来总算安装完成。

 [1]: http://rubyonrails.org/download