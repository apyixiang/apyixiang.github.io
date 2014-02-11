---
layout: post
title: "coursera视频课程批量下载"
date: 2014-02-11 13:21
comments: true
categories: dev
tags: [ssl,openssl,certificate]
---

首先安装 python以及 pip

然后继续安装 coursera-dl

```bash
pip install coursera-dl
```

使用方法

```bash
coursera-dl -u username -p password classname
```

比如

```bash
coursera-dl -u MYUSERNAME -p MYPASSWORD -d MYPATH algo-2012-001 ml-2012-002
```

https://github.com/dgorissen/coursera-dl