---
layout: post
title: "R语言统计24x60分钟的订单分布实例"
date: 2014-02-11 17:29
comments: true
categories: statistics
tags: [r,statistics,ruby]
---

ruby代码:

```ruby
require 'database'
include Database
FlowStatiOrder.find_each(:batch_size => 5000) do |row|
  time = row['LogTime']
  hour = "%02d" % time.hour
  min = "%02d" % time.min
  period = "#{hour}#{min}"
  puts period
end
```

执行 ruby, 并使用shell统计订单数量

```bash
ruby export_order_by_minute.rb > time
sort time|uniq -c > sort_time #还需做一些简单的人工处理
```

执行 R 语言

```r
require(ggplot2)
d <- read.csv('/tmp/sort_time',header=T)
p <- ggplot(d,aes(x=time,y=order)) + geom_point()
ggsave(p,filename='/tmp/image.png')
```
