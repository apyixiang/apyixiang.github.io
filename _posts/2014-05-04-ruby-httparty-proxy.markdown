---
layout: post
title: "Ruby用HTTParty调用proxy的方法"
date: 2014-05-04 14:27
comments: true
categories: dev
tags: [ruby,httparty,http,proxy]
---

```ruby
class Twitter
  include HTTParty
  http_proxy 'http://myProxy', 1080
end
```