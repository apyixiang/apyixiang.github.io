---
layout: post
title: "拿到服务器http Cookie的方法"
date: 2014-02-10 03:21
comments: true
categories: dev
tags: [ruby,http,cookie]
---


```ruby
response = HTTParty.get("http://www.baidu.com")
puts response.headers["set-cookie"][0]
```