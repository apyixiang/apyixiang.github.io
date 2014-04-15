---
layout: post
title: "如何做SEO"
date: 2012-03-30 18:46
comments: true
categories: seo
tags: [SEO]
---

[这只是一个草稿,还需要细化.上个月去了上海参加一个搜索引擎营销会议,听了SEO部分才发现业内的水平如此之低,也许是故意放水吧.故有兴趣整理一份个人能想到的相对全面的SEO文档,以告诉大家什么是真正的SEO]


  如何做seo(以下搜索引擎运行原理,纯属个人感受,真实信息请参考权威论文或书刊)


  A.几点疑问

  为什么做搜索引擎?

  让用户找到符合他需求的内容


  为什么做SEO?

  便于搜索引擎分析和收录网站页面,从而实现前一点


  我的xxx页面怎么才能排第一?

  我的xxx页面怎么才能得到高PR值?

  我的xxx页面怎么才能被收录?

  我的xxx页面怎么才能被抓取?

  我的网站怎么才能提高整体流量?

  我的网站怎么才能提高整体有效流量?(什么是无效流量?)

  我的网站怎么才能提高整体收录量?

  我的网站怎么才能提高整体有效收录量?(什么是无效收录?)

  我的网站怎么才能提高整体抓取量?

  我的网站怎么才能提高整体有效抓取量?(什么是无效抓取?)

  抓取之后怎么才能搜到我的页面?

  搜索引擎的索引页面的原理?

  怎么提高xxx页面关键词的排名?

  怎么提高xxx页面有效关键词的排名?

  怎么帮助搜索引擎找到xxx页面的关键词?


  B.理解搜索引擎的运行方式,理解搜索引擎的难处.


  工作时间:

  我方的:页面尺寸,cpu性能,内存数,程序性能,网络带宽

  百度的:程序性能,cpu性能,内存数,磁盘读写速度,带宽

  与百度之间的网络节点数

  工作难度(影响了工作时间):

  网页主要内容提取(去掉广告,top10,导航等无关信息)

  中文分词

  找出关键词

  计算每个关键词的相关度(频率x视觉权重系数)

  对于每个关键词的主要内容提取(显示在结果页)

  动态地址处理

  计算链接相关性

  累计链接的加分


  为了说明工作难度,按我理解的抓取原理

  1.针对某一个host(假设是bcd.abc.com)

  2.下载bcd.abc.com/robots.txt,拿到$array_disallow(“禁止下载的uri列表”.请注意,只能得到此域名内的,不负责其他域名的)

  3.从$array_uri_fetch(“uri下载队列”)中取得一个uri(假设是bcd.abc.com/test/test.php?param=test,
  或bcd.abc.com/test/test.html)

  4.解析uri得到$host,$path,$hash_get_param

  5.发出http请求,下载页面

  6.将uri放到”已抓列表中”,排重

  7.提取这个页面&lt;a&gt;&lt;area&gt;中没有写rel=”nofollow”的href属性,并变成绝对地址

  8.排除”${self_uri}#”,排重,得到本页href干货

  9.若符合uri规则,并且在已抓列表中不存在,则放到$array_uri_fetch中,排重

  10. 从1循环


  为了说明工作难度,按我理解的保存方式(建立$uri到$content的映射)

  静态uri的保存方式.

  $uri =&gt;

  $uri_md5 =&gt;

  $uri_path =

  {

  [0] =&gt; uri_md5[0-4]

  [1] =&gt; uri_md5[5-10]

  [2] =&gt; uri_md5[11-32]

  }

  举例:

  $host

  ├── 12345 (uri_md5[0-4])

  │   └── D01E4 (uri_md5[5-10])

  │   └── 375397E87BF9CFF5C9B472 (uri_md5[11-32])

  ├── 67890

  │   └── 97E87

  │   └── D9D822F7858F8A6F940E90

  ├── ABCDE

  └── F1234


  为了说明工作难度,按我理解的动态uri的保存方式

  (由于动态uri,参数换位置不影响结果,情况会有些复杂,因此需要额外计算量)


  多参数动态uri的保存策略.

  $uri =&gt;

  {

  $hash_queries =

  {

  $param2 = $value2

  $param3 = $value3

  $param1 = $value1

  …

  } =&gt;

  $hash_queries=order($hash_queries) =&gt;

  $hash_queries_in_order =

  {

  $param1 = $value1

  $param2 = $value2

  $param3 = $value3

  …

  } =&gt;

  $uri_in_order =&gt;

  $uri_in_order =&gt;

  $uri_in_order_md5 =&gt;

  $uri_in_order_store_dir =

  {

  [0] =&gt; uri_in_order_md5[0-4]

  [1] =&gt; uri_in_order_md5[5-10]

  [2] =&gt; uri_in_order_md5[11-32]

  }


  举例:

  $host

  ├── 12345 (uri_in_order_md5[0-4])

  │   └── D01E4 (uri_in_order_md5[5-10])

  │   └── 375397E87BF9CFF5C9B472 (uri_in_order_md5[11-32])

  ├── 67890

  │   └── 97E87

  │   └── D9D822F7858F8A6F940E90

  ├── ABCDE

  └── F1234


  为了说明工作难度,按我理解的识别重复页面的方式:

  (识别重复页面的复杂度,计算量,出错风险过高,因此,除非网站主动声明,搜索引擎无法对重复内容归类)

  方式1: 通过md5建立$uri到$content_md5的映射

  $uri =&gt;

  $uri_md5 =&gt;

  $content =&gt;

  $content_md5 =&gt;

  $content_path =

  {

  $content_md5[0-4]

  $content_md5[5-10]

  $content_md5[11-32]

  } –&gt;

  {$uri_md5}


  举例:

  $host

  ├── 23456

  │   └── 5E0AE

  │   └── 9D354B9762C15AA4C19B7E –&gt; {12345-D01E4-375397E87BF9CFF5C9B472,67890-97E87-D9D822F7858F8A6F940E90}

  ├── 7890A

  ├── BCDEF

  └── 01234


  方式2: 建立$uri到$array_keywords的映射 和 $content到$array_keywords 的映射

  $content =&gt;

  对正文的分词 将&lt;META KEYWORDS&gt;, 对&lt;title&gt;的分词, 放入$array_keywords =&gt;

  统计正文中出现的频率 =&gt;

  按频率倒排序取前N个 =

  $array_keywords

  {

  ‘key1′=&gt;number1

  ‘key2′=&gt;number2

  ‘keyN’=&gt;numberN

  }

  $uri =&gt; $content =&gt;


  辅助方式: 建立$uri到$title_md5的映射,并且对这些$uri优先检测


  C.产品统一规范

  uri唯一性,核心内容变了,uri必须改变,同样的内容,不允许出现第2个uri

  每一系列uri必须映射到同一个正则表达式,标明对应的意义

  uri归属关系

  同一个host包含同一领域内容(例如news.domain.com,shop.domain.com)

  反过来也一样,同一领域内容应规划到同一个host(例如${username}.blog.domain.com 应统一规划到blog.domain.com/${username});

  子目录附属于父目录(product.domain.com/${product_name}/price.html 不应该是price.product.domain.com/${product_name}/)

  页面公用部分规范:广告,全站通用导航,通用侧边栏等,使用iframe

  所有页面必须有meta keywords

  每次重大调整按域名归类。例如改版、title变化、大量站外推广、新产品上线。为了与效果监控数据对比观察.

  C-补充

  uri不规范的害处

  缺乏外链:

  当uri参数过多,造成超长时,有可能出现不可点击的情况(被截断)

  当参数变化较多时,外链带来的权重无法积累到同一个uri

  影响用户分享:当我方uri参数过多,竞争对手uri简洁的时候,同时展示出两个地址时,用户会倾向简洁地址(猜测)


  D.seo最佳建议

  多版本网页的地址管理最佳建议

  最佳建议:

  最新稳定版: xxx.com/download/

  最新测试版: xxx.com/download/beta.html

  最新开发版: xxx.com/download/dev.html(可无)

  历史版本: xxx.com/downlowd/all.html

  反面教材:

  1.0版: xxx.com/1.0

  1.2版: xxx.com/1.2/

  2.2版: xxx.com/path/2.2

  3.0版测试版: xxx.com/path/3.0test.html

  3.0版正式版: xxx.com/path/3.0normal.html

  4.0版: xxx.com/4.0new.html

  最新版: xxx.com/


  ajax页面的处理最佳建议

  ajax适用情况:

  点击后页面核心内容无变化,只有小部分页面内容变化(例如投票后的前端数字变化,注册时显示用户名是否被占用);

  后台应用.

  网页内容禁止用户通过其他渠道(im软件,sns,微博)分享

  ajax不适用的情况:前台页面内容多于一屏幕时的翻页按钮.


  统计用户行为的最佳建议

  首先,不论用任何变法,应定期抽样统计,而无需持续统计

  其次,统计方式有: http referer,js+cookie, js发送日志,uri参数,uri参数+redirect

  http referer只能满足初级需求(一维数组),只能知道用户从哪个页面点过来的

  其他方式,只要多一个变量就多一维数组,可以划分区域和子区域

  唯一有问题是纯uri参数,造成上述[uri不规范的害处]

  过渡的解决办法

  在程序中识别统计用的uri参数,并在response中返回301,跳转到统一的uri.

  在页面中增加js函数,链接全部使用静态uri,当用户点击时,将静态地址替换为带统计参数的uri

  完全的解决办法就是改换成其他统计方式


  统计搜索引擎爬虫来源的最佳建议

  cookie,js,http referer在这个需求中都不起作用,因为都是浏览器的功能.所以只能在uri中增加参数,最后统计日志.

  例如,www.domain.com/path/?src=product.domain.com 并且这类uri做301跳转=&gt;www.domain.com/path/.建议在服务器中寻求解决方案,跳转的同时增加?src=product.domain.com的访问日志.否则只能在www.domain.com/path/对应的程序中处理了.


  防止搜索引擎收录注入最佳建议

  概念:当网站开放搜索结果页的收录时,很可能被垃圾营销团队盯上,导入大量垃圾广告的搜索地址,例如,开放了http://www.xxx.com/search?q=${keyword},垃圾营销团队可能会把${keyword}替换成”www点domain点com”

  解决方法:等百度支持 &lt;meta name=”robots” content=”noindex”&gt;后可以尝试使用这个标签;目前只能将http response
  code改成404,并保证页面内容不变;


  提高搜索引擎抓取效率最佳建议

  将最近1个月的访问日志过滤出来，只要user-agent是Baiduspider和Googlebot的.国内用户可以只看Baiduspider的.

  使用linux系统,把这些日志文件都放到某一个文件夹下,不要建子文件夹

  进入放日志的目录,输入:

  cat * | awk ‘{print $7}’| sort |uniq -c|sort -n|tac &gt;/tmp/result

  这个列表是按照搜索引擎抓取次数排序,找到抓取量过大,但又不是关键节点的uri,屏蔽站内入口,或限制散播


  交换友链最佳建议(如果不考虑流量因素)

  选择内容相关性强的网站,或uri

  优先交换目标,不应选择网站内容相关,但本身内容不相关的uri

  pagerank密度,根据pagerank分值/(&lt;a&gt;标签数+&lt;area&gt;标签数)计算,平等交换


  sitemap最佳建议

  /${path}/sitemap.txt

  ├── sitemap_${name}_${number}.txt

  └── sitemap_${name}_${number}.txt

  ├── http://abc.com/1.html

  └── http://abc.com/1.html


  降低页面尺寸最佳建议

  针对桌面浏览器的网页,全部采用html5标签定义 &lt;!DOCTYPE html&gt;

  JS,CSS不得出现在&lt;header&gt;中,从外部引用

  合并不同项目之间公用JS,CSS部分

  页面输出之前删除无用空字符，回车，换行，空格，制表符，注释等

  模板中公用include的部分,使用iframe


  seo统计数据最佳建议

  网站有多少$host

  每个$host的robots.txt内容,统计缺失本信息的$host

  每个$host根据产品经理的估算,应该有多少可访问$uri

  每个$host根据程序抓取,实际有多少可访问页面$uri

  每个$host根据搜索引擎信息,大概收录多少$uri

  根据每个页面的&lt;META KEYWORDS&gt;提取$array_keyword,统计$array_keyword空的$uri

  根据每个页面的&lt;META DESCRIPTION&gt;提取$description,统计$description不符合正常字数的$uri

  根据&lt;META KEYWORDS&gt;和页面分词数量计算每个$page对于每个$keyword的密度

  根据&lt;META KEYWORDS&gt;和h1,&lt;strong&gt;等标签的分值,计算权重

  根据每个$page的每个$keyword查询网页排名

  根据分词统计每个页面密度最大的前10个词,计算出相似页面 对于站外推广，友情链接，建立集中管理的系统，所有相关信息必须记录与此。定期检测链接成活率、收录率，是否被惩罚，是否含毒，是否有”no
  follow”，关键词是否吻合，相对位置是否有变化


  监控每次动作后1个月的收录量，平均排名量的变化。

  根据这些对uri归一:$hash_keyword_density一致的页面

  &lt;META DESCRIPTION&gt;重复的页面; &lt;title&gt;重复的页面;


  seo知识最佳建议

  能理解搜索引擎大体工作原理,可以找一些搜索引擎原理的书籍

  有编程背景,脚本语言足矣

  能看懂简单的http协议(推荐http developer’s handbook)

  能用chrome简单调试web页面

  使用linux系统,掌握find,awk,sed,grep

  掌握一种高效文本编辑器,推荐vim


  seo数据调查的工具

  查大体收录量使用搜索引擎命(google,baidu)令:

  site:${host}

  site:abc.com

  site:any.abc.com


  查导入链接页面使用搜索引擎命令(只能用来找问题)

  link:abc.com (google)

  domain:abc.com (baidu)


  提交sitemap,观察网站表现情况

  zhanzhang.baidu.com

  webmaster.google.com


  查页面包含的链接

  lynx -dump(for linux)


  反例:

  http://auto.163.com/05/0920/20/1U4BS84P000816I1.html 链接问题

  http://auto.163.com/special/00082KFS/Mazda2_sdn.html 链接问题

  http://auto.163.com/10/0129/08/5U6CTJ4K00081GDM.html title问题

  http://auto.163.com/special/0008362H/pingce_10.html 分页问题
