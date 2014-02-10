---
layout: post
title: "activerecord 序列化"
date: 2012-02-10 01:55
comments: true
categories: ruby
---

序列化:

```ruby
product = Product.first
json = product.as_json
```

用于更新时:

```ruby
row = {"id"=>327542, "name"=>"北京图书馆附近的宾馆", "account_id"=>2, "se_id"=>1624879042, "max_price"=>6.0, "runtime"=>'2014-01-16 15:45:21 +0800', "min_price"=>0.8, "price"=>4.0, "side"=>1, "position"=>1, "status"=>2, "updated_at"=>'2014-01-15 07:56:24 UTC'}
job = Db::BidJob.product(ELONG_PRODUCT).se(SEARCH_ENGINE).allocate
job.init_with('attributes'=>row)
job.name = 'new name'
job.save #update
```

用于插入时:

```ruby
task = Task.new(JSON.parse(task_json)).save #insert
```
