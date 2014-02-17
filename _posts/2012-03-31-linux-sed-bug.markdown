---
layout: post
title: "linux sed替换utf8字符的bug"
date: 2012-03-31 04:48
comments: true
categories: dev
tags: [unicode,utf8,linux]
---
经过上次的研究，郁闷的碰上了sed的一个bug，
UTF8字符 9FA5~9FFF 在sed里做正则替换会报告
sed: -e expression #1, char 31: Invalid collation character
那么折中的办法就是：
sed 's/[xE4xB8x80-xE9xBExA5]//g' filename>newfilename

也就是说9FA5~9FFF这些中文是无法用sed替换的，希望高人指点
