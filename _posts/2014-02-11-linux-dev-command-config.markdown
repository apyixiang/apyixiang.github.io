---
layout: post
title: "linux下开发的常用配置/命令笔记"
date: 2014-02-11 13:12
comments: true
categories: dev
tags: [linux,ssh]
---

让authorized_keys生效必须保证~/.ssh权限是700

scp复制远端文件带通配符,就是需要把星号转义一下
=============

```bash
scp username@hostname:/path/to/dir/filename\* .
```

删除文件开头BOM标记
=============

```bash
awk '{if(NR==1)sub(/^\xef\xbb\xbf/,"");print}' inputfile > outputfile
```

查看网络使用情况
=============

```bash
lsof -i
netstat -lptu
netstat -tulpn
```

查看当前使用的shell
==============

```
echo $0
```

关闭ssh连接后，仍然保持程序后台运行的方法
===============
nohup program &
例如：

```bash
nohup ruby something.rb 2>errors &
```


crond配置说明
==============

```
* * * * * command
```

按前后顺序,分别表示:

分钟    0 ~59
小时  0 ~ 23
Day of Month    0 ~ 31
月   0 ~ 12
Day of Week 1 ~ 7


CentOS  163镜像使用方法
==============
http://mirrors.163.com/.help/centos.html
http://mirrors.163.com/.help/CentOS6-Base-163.repo