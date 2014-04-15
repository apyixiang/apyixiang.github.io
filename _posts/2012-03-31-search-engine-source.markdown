---
layout: post
title: "如何判断搜索引擎爬虫的来源"
date: 2012-03-31 05:11
comments: true
categories: seo
tags: [SEO,spider]
---

判断来源一般有4个途径：
1.cookie，只适用于用户行为，浏览器需开启cookie功能，接受服务器的cookie请求
2.http referer，只适用与用户行为，浏览器都会自动写这个字段
3.url参数，完全通用
4.javascript，只适用于用户行为，需要浏览器支持

因此想统计搜索引擎爬虫来源，只能在url上添加参数了，例如,www.domain.com/path/?src=product.domain.com 并且这类url做301跳转=&gt;www.domain.com/path/
建议在服务器中寻求解决方案,跳转的同时增加?src=product.domain.com的访问日志.否则只能在www.domain.com/path/对应的程序中处理了.

