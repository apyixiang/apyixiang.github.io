---
layout: post
title: "linux环境下保证ruby单进程运行的方法（适用于所有语言）"
date: 2012-03-31 04:47
comments: true
categories: dev
tags: [ruby,crond,linux,process]
---

做单进程目的是为了不停的用crond触发程序运行，而保持这个程序始终只有一个进程执行。
因为，我用crond每分钟触发执行一次。即使程序若异常则退出，可以用crond再次保持其运行。若程序运行时间很长，会造成系统同时执行N个进程，造成内存溢出或数据错乱。

最简单的方法是直接使用pidfile
require 'pidfile'
PidFile.new
他的原理是在系统临时目录中(/tmp)创建一个空文件, 比如/tmp/program_name_342534636.lock
这个文件存在则表示程序在运行, 运行完毕会删除这个文件. 从而保证进程执行的进程唯一性.

比较原始的方法是直接指定进程名称, 每次执行之前查看是否存在此进程.

```ruby
$0='the_unique_name_you_give_to_the_process'
exit if `ps aux|grep the_unique_name_you_give_to_the_process|awk '{print $11}'|grep the_unique_name_you_give_to_the_process|wc -l`.to_i>1
```

其中$0是进程名称。第2句执行了一行shell语句；查询系统进程，统计数量若>1，说明两个进程同时运行，自觉退出。