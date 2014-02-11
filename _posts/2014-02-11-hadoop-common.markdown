---
layout: post
title: "hadoop常用操作"
date: 2014-02-11 13:21
comments: true
categories: dev
tags: [hadoop]
---

参考文献
==========
http://www.cnblogs.com/forfuture1978/archive/2010/11/14/1877086.html  map-reduce
http://hbtc2012.hadooper.cn/
http://www.ibm.com/developerworks/cn/opensource/os-log-process-hadoop/
http://www.ibm.com/developerworks/cn/linux/l-hadoop-3/
http://blog.csdn.net/zhaoyl03/article/details/8657031
https://192.168.9.247:8443 azkaban azkaban
http://hive001.hadoop.bjy.elong.com:81/data/input/iis/website/tj/20121218/


调试 中间结果(mapping 后的结果)
================
-numReduceTasks 0

常用命令
==============
```bash
hadoop fs -ls /data/logs/webserver/website/hotel/20131128
hadoop fs -cat /data/logs/webserver/website/hotel/20131128/log.1385589547988
```

删除文件和目录

```bash
hadoop fs -rmr /data/logs/webserver/website/hotel/20131128
hadoop fs -rm /data/logs/webserver/website/hotel/20131128/log.1385589547988
```

结果合并后导出
=============
```bash
hadoop fs -getmerge  /data/logs/webserver/website/hotel/20131128 /homedir/username/output
```

按范围查询hdfs
===============

```bash
hadoop fs -ls /data/logs/webserver/website/hotel/{20131129..20131205}
```

按范围输入
================

```bash
input /homedir/username/keyword_convertion/searchengine/{20131202,20131203,20131204,20131205,20131206,20131207,20131208}
```
