---
layout: post
title: "针对百度将取消referrer关键词显示接受《若兰访谈》"
date: 2015-05-22 12:02
comments: true
categories: seo
tags: [SEO,referrer,baidu]
---

这次事件的影响和意义
----------------------
接受采访前调查了一下大家对这次事件的理解,发现这篇文章写的最好.
http://qiuingseo.com/yejiedongtai/152.html
不再赘述了,就是想强调一下所谓"安全"是针对百度自己,并不是让网站或用户更安全(或者说这部分意义不大).

对于站长们的影响:

1. 对于小站也许没有影响,可以从站长平台上获取足够的数据.但是对于大站无法得知流量的准确来源,缺少了一个重要的线索,也许还要靠广泛抓取排名来补充评估.

2. 区分品牌词流量(感谢ZERO张闻一提供思路).SEO品牌词基本是不用花精力优化的,而且不应该算作SEO的KPI,而是Marketing的KPI.将来无法根据关键词的字符串来区分品牌词流量,那么我的建议是PC端把首页的SEO流量都算品牌词贡献,移动端首页没有其他渠道标识的流量都算作品牌词贡献.

3. 根据referrer自动优化页面.根据用户来源词自动改变页面本身内容,使其与检索词更相关.

4. 有人说还可以从百度统计上看到关键词数据,我觉得是错误的.这类产品的原理是用js从浏览器端额外发请求到百度统计服务器上,如果referrer中的关键词去掉了,百度统计也是无能为力.所以对于站长来说数据接口应该只有站长平台.

如果让我替百度说句话,我觉得即使完全隐藏关键词的数据,也不是没有道理.SEO有些工作确实目的性太强了,眼里只有业绩,没有用户.页面排名上去了,但用户体验并不一定很好.对于SEO从业者来说,大家都是公平的,没做到位的事情还有很多,努力适应一下吧.

referrer事件技术细节
----------------------
取消referrer从技术角度看影响的是web服务器访问日志中的referrer字段,意思是访问来源.

![referrer逻辑展示]({{ site.url }}/images/baidu-referrer.png)
一般情况下它是由用户点击链接的行为触发的,由浏览器实际执行.用户搜索"复仇者联盟"并点击一个A网站(如图上2所示)的搜索结果, 那么A网站的访问日志中一定会新增一条记录,并且referrer是(如图上1所示):

```html
http://www.baidu.com/s?wd=复仇者联盟
```

取消referrer中关键词,目前百度是这样实现的,把所有搜索结果都替换为这样的中间地址,如图上3所示.请注意其中wd这个参数的值是空的.

```html
https://www.baidu.com/link?url=owOnYs_fgWiw5es8PSwApbQFIG9UmJQrDtUrz8kkQKTPv9AyUpl6BV4zxHlSm2xA8Nwow3gbtxSIsmGqX2UXf_&wd=
```

几个月以前这个地址的response code还是301,并且location是结果页的URL,那么原始referrer还能继承传递下去,但是现在来看这个地址response code是200,也就是无法传递下去了.

返回的内容如下:

```html
<meta content="always" name="referrer"><script>try{if(window.opener&&window.opener.bds&&window.opener.bds.pdc&&window.opener.bds.pdc.sendLinkLog){window.opener.bds.pdc.sendLinkLog();}}catch(e) {};window.location.replace("http://bbs.3dmgame.com/thread-1013289-1-1.html")</script>
<noscript><META http-equiv="refresh" content="0;URL='http://bbs.3dmgame.com/thread-1013289-1-1.html'"></noscript>
```

日志中都可以分析哪些字段.如果没有referrer,我们还可以做什么.
----------------------
* date - 日期, 工作日与非工作日的访问量区别.
* time - 时间, 一般用于分析一天当中不同时段的访问量区别.
* ip - ip地址, 一般用于区分用户所在区域.
* host - 主机名, 一般用于区分产品.
* path - URL路径, 是否符合SEO的预期(很重要)
* query - URL参数, 是否有你不希望的参数(很重要)
* User-Agent - 浏览器标识, 暂不展开.
* Cookie - 用户Cookie, 暂不展开.
* response_code - 状态码, 是否符合SEO的预期(很重要)
* bytes - 页面尺寸, 应该有一个合理的范围,超出则报警.
* time-taken - 耗时, 应该有一个合理的范围,超出则报警.

关于路径的分析,可以参考我的这篇博文.目前还是草稿,有待完善.
http://seoaqua.com/seo-specs/

对电商的影响,将来这部分工作基本无法进展:
-------------------------

1.对于某些电商来说流量是次要的,收益是关键的,所以考核的KPI是和收益挂钩,并不简单的是UV. 利用cookie关联订单数据,可以知道每一个关键词的转化情况,以及收益.缺少了这部分数据,会加大SEO完成KPI的难度.

2.landing page的选择.同一个关键词落到不同的landing page,转化率是不一样的.

3.计算每个关键词的投入产出比.有些操作可能是涉及费用的,并与关键词紧密相关的.

百度应该做的改进
--------------------

1. 如果只是想让站长换一个地方拿数据,则应该通过站长平台提供全量数据(下载文件,API均可).

2. 如果不想削弱百度统计的作用,则应该打通统计和站长平台的数据的,平滑过渡.

3. 不管怎么改,最终的目的都应该是互惠互利,提高全行业的工作效率,提高用户体验,一起抵抗app大潮的冲击.堵住了一条路,就应该放开另一条路,否则就是围剿了.有相当一部分用户的查询需求没有被很好满足(也许这部分检索结果前几的评分都很低,但又没有发现更好的内容),百度应该想办法主动告知站长.everybody's happy!

4. 如果最终的结果导致大量网站更倾向于自己抓排名分析,整个行业的运行成本又会继续增高.希望能针对这个需求为站长提供API服务,即使是收费的都可以,当然我不太相信百度会这么做.