---
layout: post
title: "linux初学者笔记[转]"
date: 2012-03-31 05:05
comments: true
categories: linux
---

linux目录架构
/       根目录
/bin         常用的命令   binary   file   的目錄
/boot       存放系统启动时必须读取的档案，包括核心   (kernel)   在内
/boot/grub/menu.lst       GRUB设置
/boot/vmlinuz       内核
/boot/initrd           核心解壓縮所需   RAM   Disk
/dev         系统周边设备
/etc         系统相关设定文件
/etc/DIR_COLORS       设定颜色
/etc/HOSTNAME       设定用户的节点名
/etc/NETWORKING       只有YES标明网络存在
/etc/host.conf   文件说明用户的系统如何查询节点名
/etc/hosts   设定用户自已的IP与名字的对应表
/etc/hosts.allow   设置允许使用inetd的机器使用
/etc/hosts.deny   设置不允许使用inetd的机器使用
/etc/hosts.equiv   设置远端机不用密码
/etc/inetd.conf   设定系统网络守护进程inetd的配置
/etc/gateways   设定路由器
/etc/protocols   设定系统支持的协议
/etc/named.boot   设定本机为名字服务器的配置文件
/etc/sysconfig/network-scripts/ifcfg-eth0       设置IP
/etc/resolv.conf         设置DNS
/etc/X11     X   Window的配置文件,xorg.conf   或   XF86Config   這兩個   X   Server   的設定檔
/etc/fstab         记录开机要mount的文件系统
/etc/inittab   设定系统启动时init进程将把系统设置成什么样的runlevel
/etc/issue   记录用户登录前显示的信息
/etc/group   设定用户的组名与相关信息
/etc/passwd   帐号信息
/etc/shadow   密码信息
/etc/sudoers   可以sudo命令的配置文件
/etc/securetty   设定哪些终端可以让root登录
/etc/login.defs   所有用户登录时的缺省配置
/etc/exports   设定NFS系统用的
/etc/init.d/       所有服務的預設啟動   script   都是放在這裡的，例如要啟動或者關閉
/etc/xinetd.d/     這就是所謂的   super   daemon   管理的各項服務的設定檔目錄
/etc/modprobe.conf       内核模块额外参数设定
/etc/syslog.conf       日志设置文件
/home       使用者家目录
/lib         系统会使用到的函数库
/lib/modules       kernel   的相关模块
/var/lib/rpm       rpm套件安装处
/lost+found         系統不正常產生錯誤時，會將一些遺失的片段放置於此目錄下
/mnt           外设的挂载点
/media       与/mnt类似
/opt           主机额外安装的软件
/proc         虚拟目录，是内存的映射
/proc/version       内核版本
/proc/sys/kernel       系统内核功能
/root         系统管理员的家目录
/sbin         系统管理员才能执行的指令
/srv           一些服務啟動之後，這些服務所需要取用的資料目錄
/tmp           一般使用者或者是正在執行的程序暫時放置檔案的地方
/usr           最大的目录，存许应用程序和文件
/usr/X11R6：       X-Window目录
/usr/src：         Linux源代码
/usr/include：系统头文件
/usr/openwin   存放SUN的OpenWin
/usr/man   在线使用手册
/usr/bin                       使用者可執行的   binary   file   的目錄
/usr/local/bin           使用者可執行的   binary   file   的目錄
/usr/lib                       系统会使用到的函数库
/usr/local/lib           系统会使用到的函数库
/usr/sbin                     系统管理员才能执行的指令
/usr/local/sbin         系统管理员才能执行的指令
/var       日志文件
/var/log/secure         記錄登入系統存取資料的檔案，例如   pop3,   ssh,   telnet,   ftp   等都會記錄在此檔案中
/var/log/wtmp             記錄登入者的訊息資料,   last
/var/log/messages     幾乎系統發生的錯誤訊息
/var/log/boot.log     記錄開機或者是一些服務啟動的時候，所顯示的啟動或關閉訊息
/var/log/maillog       紀錄郵件存取或往來(   sendmail   與   pop3   )的使用者記錄
/var/log/cron             記錄   crontab   這個例行性服務的內容
/var/log/httpd,   /var/log/news,   /var/log/mysqld.log,   /var/log/samba,   /var/log/procmail.log：
分別是幾個不同的網路服務的記錄檔

原文地址：http://topic.csdn.net/u/20070302/11/8d39802a-17b3-42b2-81ec-8f547811a728.html?39922

