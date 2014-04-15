---
layout: post
title: "ruby常用方法"
date: 2014-02-11 14:06
comments: true
categories: dev
tags: [ruby]
---

格式化小数
==============
```ruby
format("%.2f",'123.456')
```

gem install 加速
===============

```bash
gem install gem-fast
```


数组求平均值
===============

http://stackoverflow.com/questions/1341271/average-from-a-ruby-array


ruby 正则测试
===============

http://rubular.com/


rails activerecord 常用方法
===============

官方手册 http://guides.rubyonrails.org/active_record_querying.html

基本用法
---------------

  Client.take #SELECT * FROM clients LIMIT 1
  Client.first #SELECT * FROM clients ORDER BY clients.id ASC LIMIT 1
  Client.last #SELECT * FROM clients ORDER BY clients.id DESC LIMIT 1
  Client.find(10) #select * SELECT * FROM clients WHERE (clients.id = 10) LIMIT 1

批量插入
----------------

```ruby
Client.create(array_of_new_rows)
Array.each_slice(50) do |batch|
new_rows = []
batch.each do |url|
seg ,id = URI(url).path.split('||')
new_rows << {:seg=>seg,:id=>id}
end
Client.create(new_rows)
end
```

debug
----------------

```ruby
require 'logger'
ActiveRecord::Base.logger = Logger.new(STDOUT)
```

MD5摘要
=============

```ruby
Digest::MD5.hexdigest("string")
```




如何创建一个GEM
===============

http://rakeroutes.com/blog/lets-write-a-gem-part-one/


批量插入
==============

activerecord-import

```ruby
books = []
10.times do |i|
  books << Book.new(:name => "book #{i}")
end
Book.import books
```


ruby操作SQL Server的注意事项
==============
使用with nolock
```ruby
  class ElongKeywordDetail < ActiveRecord::Base
      establish_connection $dbconfig['web']
      self.table_name = "Keyword"
      scope :lock, -> {'WITH (NOLOCK)'}
    end
```

tidy_tds可能会遇到character buffer overflow的问题，是由于sqlserver数据库中包含全角字符引起的，需要在sql语句中通过replace替换掉。


ruby使用send灵活调用方法
=============

一般的写法：

```ruby
ta.rank0 = ranks[0]
ta.rank1 = ranks[1]
ta.rank2 = ranks[2]
ta.rank3 = ranks[3]
ta.rank4 = ranks[4]
```

灵活的写法:

```ruby
ranks.each_with_index do |rank,index|
  ta.send(:"rank#{index}=",rank)
end
```

用\uFFFF的形式打印字符串
===================

```ruby
string.unpack('U*').map{ |i| "\\u" + i.to_s(16).rjust(4, '0') }.join
```


在home目录总安装gem
===============

```bash
gem install xx.gem --user-install
```

进制转换
==============

10进制

```ruby
"%u" % 1000 #1000
```

16进制

```ruby
"%x" % 1000 #3e8
```

Enumerable
=================
# Sum some numbers
(5..10).reduce(:+)                            #=> 45
# Same using a block and inject
(5..10).inject {|sum, n| sum + n }            #=> 45
# Multiply some numbers
(5..10).reduce(1, :*)                         #=> 151200
# Same using a block
(5..10).inject(1) {|product, n| product * n } #=> 151200
# find the longest word
longest = %w{ cat sheep bear }.inject do |memo,word|
   memo.length > word.length ? memo : word
end
longest                                       #=> "sheep"