---
layout: post
title: "用ruby写一个简单的socket通信"
date: 2012-03-31 04:53
comments: true
categories: ruby
tags: [ruby,socket]
---
服务器端

s = TCPServer.open(19890722)
while sock = s.accept
Thread.new sock do |client| #多线程
while str = client.gets #得到客户端信息
client.puts str #输出给客户端
puts str
end
end
end

客户端

require 'socket'
s = TCPSocket.open('localhost', 19890722)
s.puts 'test' #输出到服务器端
puts s.readline #得到服务器信息
s.close


调试的时候可以开多个窗口telnet localhost 19890722,然后分别输入一些字符串,看每个窗口得到的信息
