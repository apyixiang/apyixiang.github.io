---
layout: post
title: "ruby activerecord 常见使用方法(不使用rails)"
date: 2014-02-10 01:55
comments: true
categories: ruby
tags: [ruby,activerecord]
---

```ruby
dbconfig = {
  :adapter  => 'mysql2',
  :username => '',
  :password => '',
  :database => '',
  :host     => ''
}

ActiveRecord::Base.logger = Logger.new(STDOUT) #将SQL调试信息打印到标准输出
ActiveRecord::Base.establish_connection(dbconfig) #建立数据库链接,lazy模式,不使用则不主动连接

class TableNameExample < ActiveRecord::Base
  self.table_name = 'table_name_example' #此行不用写,自动生成
end

p TableNameExample.take #自然顺序第一条记录
p TableNameExample.first #按主键排序后第一条记录

tne = TableNameExample.new
tne.key1 = 'value1'
tne.key2 = 'value2'
tne.save #insert

tne = TableNameExample.find(10) #查找主键=10的记录
tne.key1 = 'value1'
tne.save #update

```