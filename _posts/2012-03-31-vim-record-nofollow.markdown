---
layout: post
title: "利用vim的宏录制功能批量给超链接增加nofollow的小技巧"
date: 2012-03-31 04:43
comments: true
categories: seo
tags: [SEO,nofollow,rel,vim]
---
由于中国的页面无用链接普遍较高,在修改页面模板的时候经常要批量增加rel="nofollow"属性,这时候可以利用vim做到这点.(这是我第一次用到record功能,李炜你丫要是敢给我不期望的评论,必将遭到我的诅咒!!!)

1.打开模板文件 ==&gt; vim your_template.html

2.查询"&lt;a " ==&gt; /&lt;a

3.移动到上一行,准备开始录制 ==&gt; k

4.开始录制动作,标记为a,查询下一个节点,右移1格,进入insert模式,插入rel="nofollow" ,回到普通模式,停止录制 ==&gt; qanlirel="nofollow"[esc]q

5.重复动作10次 ==&gt;10@a

目前不知道如何自动识别需要重复多少次,我是通过肉眼估算的,先来10次,不够就再来几次,也不费事

不用sed批量替换是为了肉眼检查一遍,避免替换错了,也避免多加了一次nofollow
