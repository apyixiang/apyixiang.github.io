---
layout: post
title: "ruby map小技巧"
date: 2014-02-10 03:10
comments: true
categories: dev
tags: [ruby]
---

```ruby
threads.map(&:join)
#等同于
threads.map{|thread|thread.join}
```