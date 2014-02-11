---
layout: post
title: "Ruby 用httparty做 HTTP POST 的简易方法"
date: 2014-02-10 04:27
comments: true
categories: dev
tags: [ruby,httparty,http,post]
---

```ruby
require 'httparty'
class PZ
  include HTTParty
  debug_output $stderr #开启debug模式, 平时可注释掉

  def run
    self.class.post("https://",
      :body=> {
        "param1" => "value1",
        "param2" => "value2"
    )
  end
end

Pin.new.run
```