---
layout: post
title: "ruby redis 简单用法"
date: 2014-02-10 03:12
comments: true
categories: dev
tags: [ruby,redis]
---


```ruby
require 'redis'
r = Redis.new
r.set('key','value123')
r.get('key') # 'value123'
r.del('key') # 1
r.del('key') # 0
```

http://redis.io/topics/quickstart