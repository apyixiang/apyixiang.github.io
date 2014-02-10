---
layout: post
title: "ruby写shell命令的helper"
date: 2014-02-10 03:20
comments: true
categories: dev
tags: [ruby,shell,helper]
---


```ruby
OptionParser.new do |o|
  o.banner = "USAGE: #{$0} [options] [url]"

  o.on("-f",
       "--format [FORMAT]",
       "Output format to use instead of pretty-print ruby: " +
       "plain, json or xml") do |f|
    opts[:output_format] = f.downcase.to_sym
  end

  o.on("-a",
       "--action [ACTION]",
       "HTTP action: get (default), post, put, delete, head, or options") do |a|
    opts[:action] = a.downcase.to_sym
  end

  o.on("-d",
       "--data [BODY]",
       "Data to put in request body (prefix with '@' for file)") do |d|
    if d =~ /^@/
      opts[:body] = open(d[1..-1]).read
    else
      opts[:body] = d
    end
  end

  o.on("-H", "--header [NAME:VALUE]", "Additional HTTP headers in NAME:VALUE form") do |h|
    abort "Invalid header specification, should be Name:Value" unless h =~ /.+:.+/
    name, value = h.split(':')
    opts[:headers][name.strip] = value.strip
  end

  o.on("-v", "--verbose", "If set, print verbose output") do |v|
    opts[:verbose] = true
  end

  o.on("-u", "--user [CREDS]", "Use basic authentication. Value should be user:password") do |u|
    abort "Invalid credentials format. Must be user:password" unless u =~ /.*:.+/
    user, password = u.split(':')
    opts[:basic_auth] = { :username => user, :password => password }
  end

  o.on("-r", "--response-code", "Command fails if response code >= 400") do
    opts[:response_code] = true
  end

  o.on("-h", "--help", "Show help documentation") do |h|
    puts o
    exit
  end
end.parse!
```

https://github.com/jnunemaker/httparty/blob/master/bin/httparty