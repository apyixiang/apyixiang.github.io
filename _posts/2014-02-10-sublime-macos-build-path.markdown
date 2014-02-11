---
layout: post
title: "sublime build problem in Mac, $PATH in Mac"
date: 2014-02-10 19:16
comments: true
categories: dev
tags: [sublime,mac,linux]
---

There is always an error when building ruby scripts in Sublime from "Menu -> Tools -> Build"

The reason is Sublime sticks to the standard $PATH defined by Mac system deafult, while shell is using its own $PATH.

To be specific, zsh refers to ~/.zshrc, and sublime refers to /etc/zshenv which refers to /etc/paths

You can build the ruby scripts in sublime and run them in shell to see the difference

```ruby
puts `which ruby`
puts `which gem`
puts `echo $PATH`
```

My sublime prints the system default ruby2.0 linked from /usr/bin while my zsh prints the brew installed ruby2.1 linked from /usr/local/bin. And it goes the same for gem.


The solution is quite simple: to edit /etc/paths until the paths and order are what you need.