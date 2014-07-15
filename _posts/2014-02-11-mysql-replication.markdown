---
layout: post
title: "mysql/mariadb 主从同步"
date: 2014-02-11 14:22
comments: true
categories: dev
tags: [mysql,mariadb,replication]
---

配置文件是/etc/my.cnf(或/etc/my.cnf.d/server.cnf)

首先检查所有数据库机器的配置中,数据库datadir的位置, 保证这个位置的owner是mysql, 即让mysql有读写权限.



然后启动主库mysql服务
```bash
sudo service mysql start
```

修改配置文件

```bash
[mysqld]
skip-networking
```

查看datadir中的错误日志,如果启动后出现错误说mysql库中的表找不到,可能需要执行一下

```bash
mysql_upgrade
```

在主库中执行,看两个值,mysql-bin编号, master_log_pos, 记录下来
```mysql
SHOW MASTER STATUS;
```

如果SHOW MASTER STATUS返回空结果, 很可能SHOW BINARY LOGS也返回空结果. 这样的话一般是bin-log没有正常启动. 如果datadir对mysql有写权限. 修改配置文件
```bash
[server]
log-bin=mysql-bin
```


登陆从库的linux机器,修改配置文件.假设三台机器,一主二从,那么server-id分别是1,2,3. 需要保证id是唯一的.

```bash
[server]
server-id = 2
```

到从库中执行
```mysql
CHANGE MASTER TO MASTER_HOST='sem1', MASTER_PORT=3306, MASTER_USER='rep',MASTER_PASSWORD = 'mysqlrep', MASTER_LOG_FILE='mysql-bin.000013', MASTER_LOG_POS=11187; #填入之前show master status记录的数值

START SLAVE; #开启从库同步模式

SHOW SLAVE status; #查看从库同步状态

```


修改所有机器的配置,skip_name_resolve,否则会经常看到报警
```bash
[mysqld]
skip_name_resolve
```


常用debug方式
```mysql
SET GLOBAL SQL_SLAVE_SKIP_COUNTER = 1;  #忽略slave上的一条错误
SET GLOBAL expire_logs_days = 30; #binlog只保留30天
```