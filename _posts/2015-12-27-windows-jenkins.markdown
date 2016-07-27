---
layout: post
title: "Windows + Jenkins + Ant 进行Android自动打包"
date: 2015-12-27 16:49
comments: true
categories: dev
tags: [windows,jenkins]
---

> **写在最前：**
> 挖坑Jenkins，自己一个人研究一个啥都不懂的东西对我来说是一个难度比较大的事，毕竟我是一个喜欢跟大伙一起工作的人。今天记录一下Windows下Jenkins构建Android自动打包，由于前两天事情比较多，博客就只能延误了，罪过罪过。废话不多说，马上开始。

在正式开始之前，首先来介绍一下Jenkins到底是一个什么样的工具呢？Jenkins是一个集成开发环境，它的前身是Hadson，被Oracle收购之后，就换成Jenkins这个名字了，但是还是开源的。这一点是比较不错的。

Jenkins其实就是一个后台服务加上Web管理配置页面的一个应用，它可以自动化or定时or事件触发地执行某项任务（就是jenkins里面的job），比如编译、测试、打包、发布等等。这个在Web开发、APP开发等大项目的多人合作上是非常有帮助的。只要配置好了，每个人只需要把自己的工作做好即可，Jenkins会自动的从svn或git上获取最新的代码，整合编译发布。也就是说发布版本的流程上很大一部分工作都由jenkins自动完成了，确实帮程序猿们省了时间。

Jenkins软件的设计是基于主从（Master–Slave）式框架，在Windows、MAC或Linux配置好了主程序（Master）之后，再配置多个执行任务的节点（Slave），然后主程序（Master）发出构建任务的命令，这些任务的执行者-节点（Slave）就会去执行编译、测试、打包、发布等任务，最后发布版本。下图为本人目前对Jenkins集成开发的理解：

![我对jenkins的理解](http://upload-images.jianshu.io/upload_images/1346485-91d9469b53cd0fdd?imageMogr2/auto-orient/strip)

首先来简单介绍一下，Jenkins自动构建app（不管是Android还是IOS或是其他平台的应用）的整个思路，Jenkins主程序（Master）构建任务，将任务（job）分配给job依赖的节点（Slave），那么这个节点就会按照任务的整个流程一个一个走，如果中间哪里出错了，会立即停止运行，或一直走完整个流程构建成功为止。拿打包Android APP的例子来说吧，首先节点将代码从SVN或GIT中download下来，然后执行构建，打包，再执行构建完成之后的工作。

**本文以Android ant打包为例，来介绍构建Android APP的例子。因为这个例子是拿我本地jenkins来写的，所以没有体现主从（Master–Slave）的关系，后面会详细介绍。**


**1.新建任务Job**

点击"新建"

![新建job](http://upload-images.jianshu.io/upload_images/1346485-0ade50f74dfe1e8f?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

进入新建job首页，

![新建1](http://upload-images.jianshu.io/upload_images/1346485-407651f53dbc66c1?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
Item名称填写这个Job的名称，往下，一般选择"构建一个自由风格的软件项目"，之后进入主要设置界面，

![项目介绍](http://upload-images.jianshu.io/upload_images/1346485-0e8543a8e7a0a006?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
项目介绍，不用多说，往下翻

**2.配置代码库**

我用的snv，与git的配置有点区别，但是不大，也比较简单，

![svn配置](http://upload-images.jianshu.io/upload_images/1346485-87c0c41d69f301c7?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

一般简单配置如上，就行。如果有不懂填什么的话，可以点击右边红色框框里的问号图案，该怎么填，里面都有介绍，详细的不能再详细了。

**3.配置构建触发器**

构建触发器，红色圈内，设置说明比较详细：
![构建触发器](http://upload-images.jianshu.io/upload_images/1346485-36a827a63a4b4607?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

构建任务配置：
![配置ant构建](http://upload-images.jianshu.io/upload_images/1346485-1e0434d9a1b79285?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

里面可以配置许多东西，这里只用到了Ant，所以其他选项没有设置

**4.构建后配置**

构建后配置：
![构建后](http://upload-images.jianshu.io/upload_images/1346485-b990d0fb9b71b2a4?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/1346485-623ad3dba34cb850?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
可以看见构建之后的配置也是非常多的。详细介绍可以看问号的详细说明

完成配置之后，点击"立即构建"

![立即构建](http://upload-images.jianshu.io/upload_images/1346485-8b2b55874ccf983a?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**5.查看控制台**

构建开始，点击"Console Output"，就可以看到控制台的输出，如下图：

![控制台输出](http://upload-images.jianshu.io/upload_images/1346485-c6b451602a8cfb47?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**6.构建完成结果**

构建完成之后，最后输出结果，如下图：
![最后输出结果](http://upload-images.jianshu.io/upload_images/1346485-5e842fcaa0962f5a?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

可以看到"最后一次成功的构建结果"，就是上述构建之后配置的结果，好处在于便于我们查看最后的显示结果。


OK，Windows配置基本完成，下面来说一下配置注意的问题


**注意事项：**

 1. 首先在本机把jdk、Android sdk、ant配置好**（因为目前博客主要讲的是单机的Jenkins，没有体现M/S的构架）**。
 
 2. 其次在本机上使用`ant build`命令运行工程下的`build.xml`文件，查看是否能正确打包，再配置job
 
 3. 再者，如果只会使用eclipse打包，没有接触过ant打包Android项目的同学，建议先学习一下ant打包，里面知识非常多，功能也比较齐全，我在这里就不一一赘述了。

> **最后：**
> 由于第一次写比较长的博客，所以可能会有一部分没有表达完整。。如果有哪里不懂，可以直接邮箱[^hello]给我。多多指教！





[^hello]: ap.yixiang@qq.com