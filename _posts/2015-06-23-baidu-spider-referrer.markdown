---
layout: post
title: "百度蜘蛛（Baiduspider）的referrer"
date: 2015-06-23 14:02
comments: true
categories: seo
tags: [SEO,referrer,spider,baidu]
---


什么是百度蜘蛛的referrer
------------------

百度蜘蛛的referrer，是指当百度蜘蛛访问网站某一个URL的时候，在HTTP头中标识的referrer字段。请注意，这个定义和百度最近声明去除referrer中关键词数据没有任何关系。

举个例子，蜘蛛在抓取 http://zhanzhang.baidu.com/site/index/ 的时候，可能会告诉你他是从 http://zhanzhang.baidu.com/ 过来的，如图所示：

![百度蜘蛛referrer的定义](/images/baiduspider_referrer_header.png)

对于站长的意义
---------------

1. 如果你关心百度从哪个页面上发现了当前这个URL的话（可以理解为抓取轨迹），那么这个字段是唯一的参考依据。

1. 如果你发现有一批URL报错（4xx或者5xx），但是一直找不到入口在哪，也就是说你不明白百度蜘蛛是从哪里发现这些错误URL的。这个字段可以帮助你迅速定位。

举个例子
------------

比如我们的SEO日志分析系统中可以看到，符合下面这种URL Pattern的路径每天有6万到10万的抓取而且全部报404。

```
/\d{6}/\d{2}/.+
```

![日志统计中的404]({{ site.url }}/images/baiduspider_referrer.png)

从发现问题至今过了1个月，查遍整个网站我也没找到入口。今天偶然仔细查了一下日志，想起了百度蜘蛛的referrer，马上就能定位问题了。这些404的URL来自于一套没人维护也没人关注的页面（往往是这样）。收录流量都不错。由于最近公司图片系统更新，图片的URL全部更改了，但这套页面并没有跟着更新。

结束语
-----------

* 很多SEO问题并不是立即致命的，所以没有及时解决，流量就像蚂蚁啃大象一样一点一点啃掉了。
* 系统性的知识积累还是会在关键时刻发挥作用的。
