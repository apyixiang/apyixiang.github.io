---
layout: post
title: "ruby读mongodb简单方法"
date: 2014-02-10 03:18
comments: true
categories: dev
tags: [ruby,mongodb]
---


```ruby
require 'mongo'
db = Mongo::Connection.new('localhost').db("friendlinks")
city = db.collection('elong_hotel_city')
city.find.each do |line|
  p line
end

```