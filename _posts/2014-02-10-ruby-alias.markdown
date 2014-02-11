---
layout: post
title: "ruby别名"
date: 2014-02-10 04:49
comments: true
categories: dev
tags: [ruby,alias]
---


定义类方法别名

```ruby

class Foo
  class << self
    def bar
      puts 'bar'
    end
  end
end

Foo.bar #output: 'bar'

```

方法别名

```ruby
class Foo
  def bar
    puts 'bar'
  end
  alias :bar2 :bar
end

Foo.bar2 #outpu: 'bar'
```