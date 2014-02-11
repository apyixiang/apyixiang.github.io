---
layout: post
title: "安装ruby 找不到 openssl的解决办法"
date: 2014-02-11 17:16
comments: true
categories: dev
tags: [ruby,openssl,setup]
---


```bash
irb(main):001:0> require 'openssl'
LoadError: cannot load such file -- openssl
  from /usr/local/lib/ruby/2.0.0/rubygems/core_ext/kernel_require.rb:45:in `require'
  from /usr/local/lib/ruby/2.0.0/rubygems/core_ext/kernel_require.rb:45:in `require'
  from (irb):1
  from /usr/local/bin/irb:12:in `<main>'
```

解决方法:
In your source location, cd ext/openssl and then ruby extconf.rb. This will generate a makefile in the ext/openssl directory. Simply make && sudo make install it to build the ruby openssl extension, and install the .so into the appropriate location.

参考:
http://askubuntu.com/questions/261914/install-ruby-2-0-with-openssl-and-readline-support