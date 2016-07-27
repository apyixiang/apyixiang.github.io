---
layout: post
title: "Windows下简易Jenkins环境的搭建"
date: 2015-12-24 09:37
comments: true
categories: dev
tags: [windows,jenkins]
---

> **写在最前：**
> 挖坑Jenkins，一个从来没有用过，更没有听说过的东西，只能说要学的东西还有很多很多。
> 
> 这篇文章主要介绍一下，windows在Jenkins的搭建，以及插件的安装，接下来的几篇将详细介绍，Jenkins下自动打包Android程序。


**1.下载Jenkins**

百度关键字，Jenkins下载，如下图：

![百度Jenkins](http://upload-images.jianshu.io/upload_images/1346485-68967d8bc03516c3?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
点击红色区域的网址，或者直接点击[Jenkins官网](http://jenkins-ci.org/)链接，出现下图的网址，

![Jenkins官网](http://upload-images.jianshu.io/upload_images/1346485-7e8cb73394424495?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

点击Windows版本的后缀为.war的文件下载。

**2.安装Jenkins**

解压.war安装包

![解压](http://upload-images.jianshu.io/upload_images/1346485-762b05a48eda9875?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

点击setup.exe文件，进行安装。
安装完毕后，在浏览器输入localhost:8080，查看Jenkins页面。

![jenkins页面](http://upload-images.jianshu.io/upload_images/1346485-cfa8bef9855c1203?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![这里写图片描述](http://upload-images.jianshu.io/upload_images/1346485-e465fb00b1f2495a?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
OK，Jenkins安装成功

**3.安装插件**

这里拿几个简单的插件来做介绍，还有笔者遇到的一个问题，以及解决办法一同写在这里。

点击“系统管理”

![系统管理](http://upload-images.jianshu.io/upload_images/1346485-d9ceee312803e1ab?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

进入管理页面，之后点击“插件管理”

![插件管理](http://upload-images.jianshu.io/upload_images/1346485-130696304f43a69a?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

进入插件页面，然后点击“可选插件”，在右上角可以过滤一个你想要的插件，

![过滤插件](http://upload-images.jianshu.io/upload_images/1346485-808dbb36eb44c471?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

随后，勾选插件，点击“直接安装”，下载即可，等待其下载安装即可。

在这里我遇到一个问题，就是下载插件时，不能连接到jenkins插件的服务器，坑爹。。。

**解决办法之一：**下载插件 然后手动安装，点击插件管理--》高级，

![高级插件管理](http://upload-images.jianshu.io/upload_images/1346485-de9e21d7b40af6d8?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

点击之后，页面下拉，你会看到“上传插件”如图：

![上传插件](http://upload-images.jianshu.io/upload_images/1346485-92dcbd4bb279b0d5?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

点击“选择文件”找到之前下载完成的.hpi后缀名的安装包，选择安装包，之后点击“上传”，然后静静等它安装完毕即可。

**解决办法二：**翻墙。。

**到此，Windows下简单的配置Jenkins完成了**