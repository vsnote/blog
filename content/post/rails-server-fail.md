---
title: rails server 错误
author: 陈 三
layout: post
date: 2014-11-17T05:33:25+00:00
url: /rails-server-fail.html
views:
  - 920
categories:
  - 前端开发
tags:
  - ruby
  - Ruby on Rails

---
在我安装好 Ruby on Rails 后，使用 `rails new` 命令新建一个项目，然后切换到项目下执行 `rails server`，出现如下错误：

    sam@linux-qo4p:~/front/ror|master⚡⇒  rails server
    Ignoring RedCloth-4.2.9 because its extensions are not built.  Try: gem pristine RedCloth-4.2.9
    Ignoring posix-spawn-0.3.9 because its extensions are not built.  Try: gem pristine posix-spawn-0.3.9
    Ignoring rdiscount-2.1.7.1 because its extensions are not built.  Try: gem pristine rdiscount-2.1.7.1
    /usr/lib/ruby/site_ruby/2.0.0/rubygems/core_ext/kernel_require.rb:54:in `require': cannot load such file -- bundler/setup (LoadError)
            from /usr/lib/ruby/site_ruby/2.0.0/rubygems/core_ext/kernel_require.rb:54:in `require'
            from /home/sam/front/ror/config/boot.rb:4:in `<top (required)>'
            from bin/rails:3:in `require_relative'
            from bin/rails:3:in `<main>'
    

这似乎是我把 openSUSE 系统从 13.1 升级到 13.2 后才出现的错误。

我的情况里，尝试错误信息中的提示方法 `gem pristine RedCloth` 并不能消除以上错误。

最后的解决办法是：

  1. `gem pristine --all`
  2. 切换到项目根目录，`bundle install`

再次跑 `rails server`，可以正常启动不报错。此后，`rails new` 新建的项目也不再报错。

## 参考

[How to rebuild native Ruby gems after a lib/system upgrade? | Jérémy Lecour][1]

 [1]: https://jeremy.wordpress.com/2014/03/14/how-to-rebuild-native-ruby-gems-after-a-libsystem-upgrade/