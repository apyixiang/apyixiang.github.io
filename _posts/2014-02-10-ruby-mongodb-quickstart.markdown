---
layout: post
title: "ruby对mongodb的常用操作"
date: 2014-02-10 03:18
comments: true
categories: dev
tags: [ruby,mongodb]
---

读mongodb简单方法
==================
```ruby
require 'mongo'
db = Mongo::Connection.new('localhost').db("friendlinks")
city = db.collection('elong_hotel_city')
city.find.each do |line|
  p line
end

```


ruby 为 mongodb 增加索引
===================

```ruby
require 'mongo'
db = Mongo::Connection.new.db("qunar")
@coll = db.collection('hotels')
@coll.ensure_index({'cityname'=>1,'id'=>1})
```
