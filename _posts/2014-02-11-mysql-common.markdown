---
layout: post
title: "mysql常用操作"
date: 2014-02-11 14:22
comments: true
categories: dev
tags: [mysql]
---

如果对数据精确性要求不高,可以设置读写不互锁
=====================

非事务型引擎(Myisam/Aria)
----------------
```mysql
SET GLOBAL concurrent_insert = 2; #NEVER=0,AUTO=1,ALWAYS=2
```
这个设置完需要定期优化表,否则会造成大量碎片.

查看参数状态:
```mysql
show variables like 'concurrent_insert';
```


事务型引擎(Innodb)
----------------

```mysql
SET GLOBAL TRANSACTION ISOLATION LEVEL READ UNCOMMITTED ;
```
查看参数状态:
```mysql
SELECT @@global.tx_isolation
```

用mysql主从同步做测试环境
======================
既想使用主库数据, 又想随意update/delete/insert. 做一个省心的测试环境
在从库/etc/my.cnf中加入选项:
slave_skip_errors = all

Mysiam/Aria性能调优
=======================
key Buffer 命中率
mysql>show  global   status  like   'key%';
key_buffer_read_hits = (1-key_reads / key_read_requests) * 100%
key_buffer_write_hits = (1-key_writes / key_write_requests) * 100%


按pattern导出表
=====================

```bash
mysql development -udevelopment -pdevelopment -e 'show tables like "root_%"' |grep -v Tables_in |xargs mysqldump development -udevelopment -pdevelopment > root.sql
```

删除重复项
===============

```mysql
ALTER IGNORE TABLE your_table ADD UNIQUE INDEX `tmp_index` (URL_ADDR);
```

表之间批量拷贝数据
===============

```mysql
insert into table2(column3,column4) select column1,column2 from table1 where 1;
```


设置用户权限
=================

```mysql
GRANT ALL PRIVILEGES ON *.* TO 'myuser'@'%' IDENTIFIED BY 'mypassword' WITH GRANT OPTION;
FLUSH   PRIVILEGES;
```

批量删除列
================

```mysql
ALTER TABLE poi drop column name_py,
drop column typename,
drop column typename_py,
drop column provinceid,
drop column provincename,
drop column provincename_py,
drop column cityname,
drop column cityname_py,
drop column districtid,
drop column districtname,
drop column districtname_py,
drop column streetname_py,
drop column address,
drop column address_py,
drop column cid,
drop column showflag,
drop column trip_py,
drop column namelen,
drop column displayorder;
```

