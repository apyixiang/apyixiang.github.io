---
layout: post
title: "利用hadoop做日志分析的实例"
date: 2014-02-11 14:42
comments: true
categories: dev
tags: [hadoop,analytics,log]
---

run.sh样本
==================
```bash
#!/bin/bash

HADOOP_HOME=/usr/lib/hadoop
HADOOP_STREAMING=/usr/lib/hadoop-0.20-mapreduce

orderfromid='12345'
srcid='semid1'


DATETIME=`date -d last-day +%Y%m%d`
DATETIME='{20131202,20131203,20131204,20131205,20131206,20131207,20131208}'
input='/data/logs/webserver/website/hotel/'$DATETIME
output='/homedir/username/keyword_convertion/'$srcid'/'$DATETIME
mapper_file='./mapper.py'
reducer_file='./reducer.py'

$HADOOP_HOME/bin/hadoop jar $HADOOP_STREAMING/contrib/streaming/hadoop-streaming.jar \
    -D mapred.text.key.partitioner.options=-k1,1 \
    -D map.output.key.field.separator=' ' \
    -D mapred.output.key.comparator.class=org.apache.hadoop.mapred.lib.KeyFieldBasedComparator \
    -input $input \
    -output $output \
    -mapper $mapper_file \
    -file $mapper_file \
    -reducer $reducer_file \
    -file $reducer_file \
    -cmdenv srcid="$srcid" \
    -cmdenv orderfromid="$orderfromid" \
    -numReduceTasks 0
```

mapper样本
==================

```python
#!/usr/bin/python
import sys
import re
import urllib2
import os
from urlparse import parse_qs,urlparse

orderfromid = os.environ['orderfromid']
srcid = os.environ['srcid']

for line in sys.stdin:
  line = line.strip()
  if line[:1] == '#':
    continue

  try:
    date,time,sitename,computername,s_ip,method,uri_stem,uri_query,port,username,c_ip,cs_version,ua,c_cookies,referer,cs_host,sc_status,sc_substatus,sc_win32_status,sc_bytes,cs_bytes,time_taken = line.split(' ')
  except ValueError:
    continue

  query_pairs = parse_qs(uri_query)

  if 'TableName' in query_pairs:
    TableName = query_pairs['TableName'][0]
    cookies={}
    for cookie in c_cookies.split(';+'):
      kv = cookie.split('=')
      if len(kv) != 2:
        continue
      k,v = kv
      cookies[k]=v

    if 'CookieGuid' not in cookies:
      continue
    CookieGuid = cookies['CookieGuid']
    key = CookieGuid+' '+date+' '+time
    if TableName == 'FlowStatiOrder':
      if 'OrderFrom' not in query_pairs or query_pairs['OrderFrom'][0] != orderfromid:
        continue
      value = "type=o&orderid="+query_pairs['OrderId'][0]
    elif TableName == 'FlowStatiData':
      referer_pairs = urlparse(referer)
      referer_query_pairs = parse_qs(referer_pairs.query)
      if 'srcid' not in referer_query_pairs or 'uuid' not in referer_query_pairs or referer_query_pairs['srcid'][0] != srcid:
        continue
      value = "type=d&uuid="+referer_query_pairs['uuid'][0]
    else:
      continue
  else:
    uri_query_pairs = parse_qs(uri_query)
    if 'srcid' not in uri_query_pairs or 'uuid' not in uri_query_pairs or uri_query_pairs['srcid'][0] != srcid:
      continue
    value = "type=d&uuid="+uri_query_pairs['uuid'][0]
  if 'key' in locals():
    print key+"\t"+value
```

reducer样本
==============
```python
#!/usr/bin/python
import sys
import re
import urllib2
from urlparse import parse_qs
last_line = None

for line in sys.stdin:
  cookie_date_time,value = line.split("\t")
  cookie,date,time = cookie_date_time.split(" ")
  value_pairs = parse_qs(value)

  if last_line:
    last_cookie_date_time,last_value = last_line.split("\t")
    last_cookie, last_date,last_time = last_cookie_date_time.split(' ')
    last_value_pairs  = parse_qs(last_value)
    if 'uuid' in last_value_pairs:
      last_value_uuid = last_value_pairs['uuid'][0].strip()
    else:
      last_value_uuid = 'xxxxxxxxxxx'

    if 'type' in value_pairs and value_pairs['type'][0].strip() == 'o':
      if last_cookie == cookie:
        print last_value_uuid+"\t"+"1"
      else:
        print last_value_uuid+"\t"+"0"
    else:
      print last_value_uuid+"\t"+"0"

  last_line = line
```