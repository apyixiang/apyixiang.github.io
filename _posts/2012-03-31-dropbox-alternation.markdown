---
layout: post
title: "发现了Dropbox的替代品:花生壳+ssh+rsync+淘汰的笔记本"
date: 2012-03-31 04:42
comments: true
categories: fun
tags: [dropbox,ssh,rsync]
---
家里的宽带基本都是包年或者包月,不利用浪费.测试的时候发现直接rsync会导致域名解析失败,不知道为啥,所以需要通过ssh.

准备一个eeebox或者淘汰的笔记本,24小时开机,省电.装linux系统,装上打开sshd,rsyncd,crond
注册花生壳账户,得到一个二级域名
在家中机器上按照花生壳的说明用curl和crond每N分钟尝试更新花生壳的DNS
在办公室机器上安装rsync,ssh-keygen,并且把~/.ssh/id_rsa.pub scp到家里机器~/.ssh/authorized_keys
rsync -avz src -e ssh des:/path/for/backup/ (可以利用crond触发)
参考文章: http://baiqiuyi.com/rsync/
