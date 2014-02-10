---
layout: post
title: "JSON.parse处理symbol的问题"
date: 2014-02-10 03:09
comments: true
categories: dev
tags: [ruby]
---

```ruby
json = {:key => 'value'}
JSON.parse(json) #{'key' => 'value'}
JSON.parse(json,{:symbolize_names => true}) #{:key => 'value'}
``