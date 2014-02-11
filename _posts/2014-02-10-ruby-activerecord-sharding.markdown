---
layout: post
title: "用activerecord处理分表结构"
date: 2014-02-10 03:28
comments: true
categories: dev
tags: [ruby,activerecord,sharding,rails,database]
---


可以自己定义类方法, 改变表名, self.table_name=

```ruby

class Keyword < ActiveRecord::Base
  establish_connection $dbconfig['production_qihu']

  @product = 'hotel'
  @date = Time.now.strftime("%Y%02m")


  def self.product(product)
    @product = product if product and !product.empty?
    self.table_name = "#{@product}_#{@date}_keywords"
    return self
  end

  def self.date(date)
    @date = date if date and date.size == 6
    self.table_name = "#{@product}_#{@date}_keywords"
    return self
  end
end

```

使用实例

```ruby
puts Keyword.product(table_product).date(table_date).take
```
