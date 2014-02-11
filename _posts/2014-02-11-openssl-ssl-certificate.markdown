---
layout: post
title: "通过openssl获取https的证书"
date: 2014-02-11 13:21
comments: true
categories: dev
tags: [ssl,openssl,certificate]
---

```bash
#!/bin/sh
#
# usage: retrieve-cert.sh remote.host.name [port]
#
REMHOST=$1
REMPORT=${2:-443}

echo |\
openssl s_client -connect ${REMHOST}:${REMPORT} 2>&1 |\
sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p'
```

使用方法举例
把上面的代码存成foo.sh
执行命令：

```bash
sh foo.sh api.baidu.com
```

http://www.madboa.com/geek/openssl/#cert-retrieve