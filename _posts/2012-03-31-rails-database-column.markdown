---
layout: post
title: "rails取表一列的方法"
date: 2012-03-31 05:21
comments: true
categories: ruby
---

请把column替换成你要的列名，把Model替换成你的model名
Model.find(:all, :select => "column").map{|x| x.column}
可以在Model里加一个方法
class Model < ActiveRecord::Base
  def self.names
      find(:all, :select => "column").map{|x| x.column}
    end
end

转自：http://snippets.dzone.com/posts/show/3901>
