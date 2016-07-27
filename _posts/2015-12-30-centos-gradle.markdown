---
layout: post
title: "CentOS下gradle的配置"
date: 2015-12-30 08:39
comments: true
categories: dev
tags: [centos,gradle]
---

> **写在最前：**
> 最近一直在研究CentOS下Jenkins的配置Android自动打包工程时，使用到了gradle，所以这里介绍一下CentOS下Jenkins的配置

**gradle与其他比如JDK、Android SDK等的配置不同，它并无系统区分，不管你是Windows、Linux还是MAC都可以使用同一个安装包**

**1.下载压缩包**

进入gradle官网，下载压缩包，

![gradle官网](http://upload-images.jianshu.io/upload_images/1346485-78d6116aa73c7f6e?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在红色圈的区域选择版本，我写博客时最新版本为2.9，如图所示，压缩包分为三种，按照自己的需求来下载就好。

**2.Copy到CentOS中解压**

复制的话，可以选用Xftp这个软件，它与XShell是一套的，比较好用，使用方法与XShell相同，简单易懂。

我把压缩包放到了`/usr/local/`下，便于自己的管理，

随后打开XShell，连接到服务器，使用命令`vim /etc/profile`打开 etc下的profile文件，配置环境如下：

![配置环境](http://upload-images.jianshu.io/upload_images/1346485-4db90e17b6fcb7c6?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

写完之后，保存之后，运行命令`source /etc/profile` 使刚刚的配置生效。

**3.检测配置是否成功**

打开XShell，运行命令`gradle -version`，有过JDK环境配置的同学，应该懂。

然后会出现：

![gardle -version](http://upload-images.jianshu.io/upload_images/1346485-38a7b58f2e07b1b8?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

包括的东西如上。

OK，配置起来相对比较简单。