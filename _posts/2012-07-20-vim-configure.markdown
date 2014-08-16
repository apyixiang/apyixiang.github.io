---
layout: post
title: "vim configure"
date: 2012-07-20 18:48
comments: true
categories: linux
tags: [vim,configuration]
---

安装方法：
http://spf13.com/project/spf13-vim

安装后：
在~/.vimrc中非注释的第2行加入set t_Co=256

建议：
删除~/.vimrc中的spell那行，这玩意注释掉都没用，用起来很恶心 如果不起作用，在~/.vimrc中加入set nospell。也许这样也没用...自求多福吧，除了这点其他都很爽。
在~/.vimrc.local中加入color molokai
搜索tree，找到C-e，改成C-t, 否则与原来快捷键冲突
