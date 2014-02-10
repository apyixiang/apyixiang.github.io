---
layout: post
title: "rvm 提速"
date: 2014-02-10 03:17
comments: true
categories: dev
tags: [ruby,rvm,speedup]
---


FOR MAC

```bash
$ sed -i .bak 's!cache.ruby-lang.org/pub/ruby!ruby.taobao.org/mirrors/ruby!' $rvm_path/config/db
```

FOR LINUX

```bash
$ sed -i 's!cache.ruby-lang.org/pub/ruby!ruby.taobao.org/mirrors/ruby!' $rvm_path/config/db
```