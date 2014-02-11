---
layout: post
title: "面向对象的Mix-in方法"
date: 2014-02-10 03:23
comments: true
categories: dev
tags: [ruby,mix-in,object]
---

```ruby
module Kkk
  def table_name
    "#{@name1}_#{@name2}_#{@name3}"
  end
end

class Abc < ActiveRecord::Base
  @name1 = 'aaa'
  @name2 = 'bbb'
  @name3 = 'ccc'
  extend Kkk
end

class Xyz < ActiveRecord::Base
  @name1 = 'ddd'
  @name2 = 'bbb'
  @name3 = 'ccc'
  extend Kkk
end

p Abc.take
p Xyz.take

```