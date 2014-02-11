---
layout: post
title: "activerecord 序列化"
date: 2014-02-10 01:55
comments: true
categories: ruby
tags: [ruby,activerecord,serialization]
---

序列化:

```ruby
product = Product.first
json = product.as_json
```

用于更新时:

```ruby
row = {"id"=>12345, "name"=>"名称","updated_at"=>'2014-01-15 07:56:24 UTC'}
job = TableModel.allocate
job.init_with('attributes'=>row)
job.name = 'new name'
job.save #update
```

用于插入时:

```ruby
task = Task.new(JSON.parse(task_json)).save #insert
```