---
layout: post
title: "R语言统计图表叠加"
date: 2014-02-11 17:27
comments: true
categories: statistics
tags: [r,graph]
---


```r
require(ggplot2)
d2 <- read.csv('~/Documents/sort_time_sem_order_by_minute',header=T)
d1 <- read.csv('~/Documents/sort_time_order_by_minute',header=T)
ggplot(d1,aes(x=time,y=order)) + geom_point(color = 'red') + geom_point(data=d2,colour = "blue")
```