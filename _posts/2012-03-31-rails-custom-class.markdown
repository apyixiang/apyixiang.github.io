---
layout: post
title: "在rails项目中使用自定义类(自定义方法，自定义class)"
date: 2012-03-31 05:20
comments: true
categories: seo
---

一直用rake跑后台程序，发现很多rake文件的代码都是重复的，明显应该调用一个公用的方法了，查了半天，原来就这么简单
1.在/lib/目录建立ruby文件/lib/testclass.rb
2.编辑testclass.rb
class Testclass
  def testmsg
      "testmsg"
        end
        end

        3.在项目中调用testclass

        require 'testclass'
        t = Testclass.new
        puts t.testmsg

        BTW,rails最新版不建议使用RAILS_ROOT常量，而建议使用Rails.root.to_s
