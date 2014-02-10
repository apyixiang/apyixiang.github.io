---
layout: post
title: "linux环境下保证ruby单进程运行的方法（适用于所有语言）"
date: 2012-03-31 04:47
comments: true
categories: ruby
---
目的是为了不停的用crond触发程序运行，而保持这个程序始终只有一个进程执行。
因为，我用crond每分钟触发执行一次。即使程序若异常则退出，可以用crond再次保持其运行。若程序运行时间很长，会造成系统同时执行N个进程，造成内存溢出或数据错乱。

方法如下：
$0='the_unique_name_you_give_to_the_process'
exit if `ps aux|grep the_unique_name_you_give_to_the_process|awk '{print $11}'|grep the_unique_name_you_give_to_the_process|wc -l`.to_i>1

其中$0是进程名称。第2句执行了一行shell语句；查询系统进程，统计数量若>1，说明两个进程同时运行，自觉退出。
