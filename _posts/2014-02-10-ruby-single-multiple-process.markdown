---
layout: post
title: "ruby控制程序的进程数"
date: 2014-02-10 05:02
comments: true
categories: dev
tags: [ruby,process]
---

单进程：

```ruby
require 'pidfile'
PidFile.new
```

多进程：

```ruby
require 'pidfile'
param = ARGV[0]
PidFile.new(:pidfile => param)
```

官方文档：
https://github.com/samullen/pidfile