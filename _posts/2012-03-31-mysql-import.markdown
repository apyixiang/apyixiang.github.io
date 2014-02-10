---
layout: post
title: "大量数据快速导入mysql的方法"
date: 2012-03-31 04:51
comments: true
categories: database
tags: [mysql]
---
当你有几千万行数据，N多个文件，需要导入mysql对应表的时候，可以试试这样做
1.假设数据表只有id和string两个字段,其中string可以做一个unique索引，避免重复
2.先建立好这些文件，用sed过滤一下特殊字符，用uniq排重一下，
3.用sed在行首插入一个";"，这是为了区分不同字段的
4.设定mysql链接方式为socket，本机不需要密码
5.用文本编辑器批量写出以下命令
mysql -uroot  -e "load data local infile '/path/to/your/file/1' into table tablename1 files terminated by ';'" databasename
mysql -uroot  -e "load data local infile '/path/to/your/file/2' into table tablename2 files terminated by ';'" databasename
...
6.将上面的命令拷贝到terminal执行
