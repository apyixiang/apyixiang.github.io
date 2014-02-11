---
layout: post
title: "ssh免用户名登陆"
date: 2014-02-11 14:22
comments: true
categories: dev
tags: [linux,ssh]
---

实现本功能的前提是已经实现了"ssh免密码登陆"
新建或者编辑配置文件: ~/.ssh/config

```
Host machine1
HostName machine1
Port 22
User username1

Host machine2
HostName machine2
Port 22
User username2
```

实际使用时:

```
ssh machine1
ssh machine2
```