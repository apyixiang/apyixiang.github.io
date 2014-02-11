---
layout: post
title: "ruby用pry做断点调试"
date: 2014-02-10 04:35
comments: true
categories: dev
tags: [ruby,debug,breakpoint]
---


```ruby
require 'pry'

class A
  def hello() puts "hello world!" end
end

a = A.new

# set x to 10
x = 10
y = rand

# start a REPL session
binding.pry#在这设置断点,然后打印上边的各种变量


# program resumes here (after pry session)
puts "program resumes here. Value of x is: #{x},and Y is #{y}."

```

https://github.com/pry/pry/wiki/User-Input
http://pryrepl.org