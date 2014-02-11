---
layout: post
title: "ruby 利用savon进行SOAP通信"
date: 2014-02-11 17:13
comments: true
categories: dev
tags: [ruby,savon,soap]
---


```ruby
#!/usr/bin/env ruby

require 'savon'
require 'pp'

## baidu fengchao  api
client = Savon.client(

  log: false,
  wsdl: "https://api.baidu.com/sem/sms/v3/AccountService?wsdl",
  namespace: "http://api.baidu.com/sem/common/v2",
  soap_header: {
    "tns:AuthHeader" => {
      "tns:username" => "username",
      "tns:password" => "password",
      "tns:token"  => "token",
    }
  },
)
pp client.operations
response = client.call(:get_account_info)
pp response.body[:get_account_info_response][:account_info_type]
```