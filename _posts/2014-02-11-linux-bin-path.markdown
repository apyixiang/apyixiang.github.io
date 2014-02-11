---
layout: post
title: "linux下可执行目录解释和使用方法"
date: 2014-02-11 13:21
comments: true
categories: dev
tags: [linux,ssh]
---


以下均为本人猜测,正确理解请查阅官方资料.
s表示script, bin表示可执行文件, local表示本机的, usr表示用户的

```bash
/usr/local/sbin #用户自己安装的,脚本可执行文件
/usr/local/bin #用户自己安装的,二进制可执行文件
/usr/sbin #发行版默认安装的,脚本可执行文件
/usr/bin #发行版默认安装的,二进制可执行文件
/sbin #linux自带的,脚本可执行文件
/bin #linux自带的,二进制可执行文件
```

如果自己安装了一个软件,想在shell中当命令使用, 需要做软连接到相应目录. 比如
假设 /home/xxx/softwares/rspec/bin/rspec是用户自己装的软件, 基于ruby写的脚本程序.那么应该:

```bash
ln -s /home/xxx/softwares/rspec/bin/rspec /usr/local/sbin
```

并且保证/usr/local/sbin在$PATH中能找到,就可以当普通命令用了.