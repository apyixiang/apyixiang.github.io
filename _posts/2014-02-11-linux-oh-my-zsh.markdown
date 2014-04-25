---
layout: post
title: "配置oh-my-zsh"
date: 2014-02-11 13:21
comments: true
categories: dev
tags: [linux,zsh,oh-my-zsh,shell]
---

- 安装最新版zsh
- 把bash换成zsh

```
chsh -s $(which zsh)
```
- 安装 oh my zsh

```
curl -L https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh | sh
```

使用ctrl+r查找历史命令
=====================
```bash
bindkey "^R" history-incremental-search-backward
```
