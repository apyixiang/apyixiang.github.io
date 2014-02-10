---
layout: post
title: "activerecord存储前会自动判断哪些字段有改动"
date: 2014-02-10 03:13
comments: true
categories: dev
tags: [ruby,activerecord,rails]
---


```ruby
product = Product.first
product.changed? #false
product.save #nothing happens
```

http://api.rubyonrails.org/classes/ActiveModel/Dirty.html