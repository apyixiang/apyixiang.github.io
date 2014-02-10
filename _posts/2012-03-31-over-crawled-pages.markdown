---
layout: post
title: "找到过度抓取的页面"
date: 2012-03-31 05:16
comments: true
categories: seo
---

将最近1个月的访问日志过滤出来，只要user-agent是Baiduspider和Googlebot的

cat * | awk '{print $7}'| sort |uniq -c|sort -n|tac >/tmp/result

然后看看result文件即可，前边的数字表示被访问次数，理想状态下每天1次即可，也就是1个月30次左右，但我估计爬虫为了考虑效率和程序设计的简单性，爬虫对目标页面没有做全面的重复性检查，造成轻微过度访问也是可以的，比如平均每天30次，那加起来每个月也不过900次


SEO其实并不单单是刚入门的人理解的SEO，而是对网站整体质量和效率的优化。
