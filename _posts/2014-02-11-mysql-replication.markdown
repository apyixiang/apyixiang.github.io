---
layout: post
title: "mysql/mariadb 主从同步"
date: 2014-02-11 14:22
comments: true
categories: dev
tags: [mysql,mariadb,replication]
---


```mysql
SHOW MASTER STATUS; #在主库执行, 看两个值,mysql-bin编号, master_log_pos, 记录下来

START SLAVE; #开启从库同步模式
CHANGE MASTER TO MASTER_HOST='sem1', MASTER_PORT=3306, MASTER_USER='rep',MASTER_PASSWORD = 'mysqlrep', MASTER_LOG_FILE='mysql-bin.000013', MASTER_LOG_POS=11187; #填入之前记录的数值

SHOW SLAVE status; #查看从库同步状态

SET GLOBAL SQL_SLAVE_SKIP_COUNTER = 1;  #忽略slave上的一条错误
```