---
layout: post
title: "使用sshfs将远程linux的目录映射到本机"
date: 2014-02-11 14:28
comments: true
categories: dev
tags: [linux,ssh,sshfs]
---


首先安装 sshfs

```bash
brew install sshfs
```

查看fuse4x的说明

```bash
brew info fuse4x-kext
```

执行其中的两行

```bash
sudo /bin/cp -rfX /usr/local/Cellar/fuse4x-kext/0.9.2/Library/Extensions/fuse4x.kext /Library/Extensions
sudo chmod +s /Library/Extensions/fuse4x.kext/Support/load_fuse4x
```

建立映射关系

```bash
sshfs charles@seo:~ share
```