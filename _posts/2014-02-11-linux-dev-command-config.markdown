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

```bash
scp username@hostname:/path/to/dir/filename\* .
```

删除文件开头BOM标记

```bash
awk '{if(NR==1)sub(/^\xef\xbb\xbf/,"");print}' inputfile > outputfile
```
查看网络使用情况

```zsh
lsof -i
netstat -lptu
netstat -tulpn
```