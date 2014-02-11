---
layout: post
title: "处理http中压缩内容"
date: 2014-02-10 01:59
comments: true
categories: dev
tags: [ruby,http]
---

{% highlight ruby %}
def handle_deflation
  case last_response["content-encoding"]
  when "gzip", "x-gzip"
    body_io = StringIO.new(last_response.body)
    last_response.body.replace Zlib::GzipReader.new(body_io).read
    last_response.delete('content-encoding')
  when "deflate"
    last_response.body.replace Zlib::Inflate.inflate(last_response.body)
    last_response.delete('content-encoding')
  end
end
{% endhighlight %}