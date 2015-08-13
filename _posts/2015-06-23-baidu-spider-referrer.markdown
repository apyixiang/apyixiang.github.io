---
layout: post
title: "百度蜘蛛（Baiduspider）的referer"
date: 2015-06-23 14:02
comments: true
categories: seo
tags: [SEO,referer,spider,baidu]
---


什么是百度蜘蛛的referer
------------------

百度蜘蛛的referer，是指当百度蜘蛛抓取某一个URL的时候，在HTTP头中带的Referer字段。请注意，这个定义和百度最近声明去除Referer中关键词数据没有任何关系。这次讲的是spider发起的HTTP请求，百度而去除的是用户发起的。如果百度蜘蛛抓取百度首页的logo，会发起这样的请求：

```
GET /img/bd_logo1.png HTTP/1.1
Host: www.baidu.com
Connection: keep-alive
Cache-Control: max-age=0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
User-Agent: Mozilla/5.0 (compatible; Baiduspider/2.0; +http://www.baidu.com/search/spider.html
Referer: https://www.baidu.com/
```

上面Referer字段很明确的表示了他是从www.baidu.com这个页面上发现并抓取了www.baidu.com/img/bd_logo1.png。而大家在服务器访问日志中也应该能看到相应的记录。目前发现只有当百度抓取一个网页的同时，又抓取了网页中的：img、js和css才会带上referer字段。这部分额外的抓取量，应该不会占用百度分配的抓取配额，属于“买1送1”。

对于站长的意义
---------------

如果你发现有一批URL（仅限于img,js,css）报错（4xx或者5xx），但是一直找不到入口在哪，也就是说你不明白百度蜘蛛是从哪里发现这些错误URL的。这个字段可以帮助你迅速定位。

举个例子
------------

比如我们的SEO日志分析系统中可以看到，符合下面这种URL Pattern的路径每天有6万到10万的抓取而且全部报404。

```
/\d{6}/\d{2}/.+
```

![日志统计中的404](/images/baiduspider_referrer.png)

从发现问题至今过了1个月，查遍整个网站我也没找到入口。今天偶然仔细查了一下日志，想起了百度蜘蛛的referer，马上就能定位问题了。这些404的URL来自于一套没人维护也没人关注的页面（往往是这样）。收录流量都不错。由于最近公司图片系统更新，图片的URL全部更改了，但这套页面并没有跟着更新。

如果站点没有记录referer怎么办
--------------

iis请在这里勾选“cs(Referer)”：

![iis-log-1](/images/iis-log-1.png)
![iis-log-2](/images/iis-log-2.png)

apache请参考:

* [apache log配置](http://www.t086.com/code/apache2.2/logs.html)“Combined Log Format”章节
* [apache log配置的官方链接](http://httpd.apache.org/docs/2.2/logs.html)

```
LogFormat "%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-agent}i\"" combined
CustomLog log/access_log combined
```


Nginx请参考：

* [nginx log配置](http://who0168.blog.51cto.com/253401/569615)
* [nginx log配置的官方链接](http://wiki.nginx.org/NginxHttpLogModule#log_format)

```
log_format combined '$remote_addr - $remote_user [$time_local]  '
                    '"$request" $status $body_bytes_sent '
                    '"$http_referer" "$http_user_agent"';
```

结束语
-----------

* 很多SEO问题并不是立即致命的，所以没有及时解决。流量就像蚂蚁啃大象一样一点一点啃掉了。
* 系统性的知识积累还是会在关键时刻发挥作用的。
* 感谢飞鹰对本文的修正。
