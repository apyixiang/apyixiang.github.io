---
layout: post
title: "抓取百度搜索结果(ruby代码)"
date: 2012-03-31 05:24
comments: true
categories: seo
---

xpath解析网页代码很方便，容易维护，找到解决方法之前一直用正则处理
问题的关键关键在于删除下面这个特殊符号：
=============================
▼
Unicode编码：U+25BC
维基百科注释：Black down-pointing triangle
=============================
否则使用nokogiri，Mechanize按xpath语法解析的时候会出bug，请参考下面的代码

a = Mechanize.new {|agent| agent.user_agent_alias = 'Linux Mozilla'}
a.get(url) do |page|
page.body = Iconv.iconv('UTF-16','GBK',page.body).first
page.body.gsub! ("[U0080-U2C77]+",'')
p page.search("//table")
end

更新一下:最近写了一个小的ruby gem,用来抓取百度搜索结果,排名,收录数,地址是

http://rubygems.org/gems/baidu
