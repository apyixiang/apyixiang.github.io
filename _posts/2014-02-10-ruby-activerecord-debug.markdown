---
layout: post
title: "activerecord debug方法"
date: 2014-02-10 03:15
comments: true
categories: dev
tags: [ruby,activerecord,rails]
---


```ruby
ActiveRecord::Base.logger = Logger.new(STDOUT)
```

或者

```ruby
ActiveRecord::Base.logger = Logger.new('/var/log/xxx.log')
```