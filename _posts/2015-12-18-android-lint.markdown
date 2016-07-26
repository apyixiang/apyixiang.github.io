---
layout: post
title: "[Android Lint] XXXX is not translated in en (English),zh (Chinese)"
date: 2015-12-18 11:25
comments: true
categories: dev
tags: [android,lint]
---

**1.出现问题：**

今天打包具有双语的Android工程，在引用中报了一个莫名其妙的错误，如下图：![问题出现](http://upload-images.jianshu.io/upload_images/1346485-9f5db7fa9ddc3794?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)也就是说在打包导出的时候有错误，再来看一下错误，

![查看错误](http://upload-images.jianshu.io/upload_images/1346485-7f4f372bce484193?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
`"XXXX" is not translated in "en" (English), "zh" (Chinese)`报的是Lint Warnings错误。

**2.问题原因**

根据错误信息，是说我没有对string文件进行国际化翻译操作，查看报错位置，原来是当前项目引用的一个Library有国际化操作，包含values-en和values-zh两个文件夹，才导致我到处当前项目的时候报出此错误。

**3.临时方法**

Eclipse-&gt;Windows-&gt; Preferences-&gt;Android -&gt;Lint Error Checking的Correctness: Messages -&gt;MissingTranslate

![临时解决办法](http://upload-images.jianshu.io/upload_images/1346485-91bc4d9d675bd8ae?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)把MissingTranslate的Severity的值改为Warning。

**4.最终方法**

如果你的项目是国际化，或是双语的，那么在项目中创建values-en和values-zh两个文件夹，然后把中文的string.xml放到values-zh问价夹下，把英文的string.xml放到values-en下。

![](http://upload-images.jianshu.io/upload_images/1346485-b68b95be37fc455e.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)