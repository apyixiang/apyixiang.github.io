---
layout: post
title: "SEO原则"
date: 2012-03-31 05:18
comments: true
categories: seo
---
<div id="page" lang="zh" dir="ltr">
<div id="content" lang="zh" dir="ltr">
<h1 id="head-03092529171871d780f310ee67c225ef4de1fb0f">总原则</h1>
简洁，规范，统一，减少维护成本，优先考虑UE，避免重复，避免歧义，避免盲目抄袭。若以下策略违反总原则，请纠正
<h1 id="head-5a6f99bd742e67da7b711e417666968da7266c78">链接规范</h1>
<ol type="1">
	<li>屏蔽方法
<ul>
	<li>对站内链接，增加属性rel="nofollow"</li>
	<li>对站外链接，增加属性rel="external nofollow"</li>
</ul>
</li>
	<li>2次或2次以上出现同一个URL时，只保留一个URL，其他均屏蔽</li>
	<li>站外链接，非特别声明，均屏蔽。</li>
	<li>屏蔽以下各种站内链接
<ul>
	<li>”换肤”，“登陆”，“关于公司”，“联系方式",“填写问卷”等无价值但被频繁链接的页面</li>
	<li>本页面链接指向页面主题不相关</li>
</ul>
</li>
	<li>进制&lt;a&gt;做为按钮使用，请使用其他标签(例如&lt;div&gt;).最极端的办法是将无价值链接也替换成&lt;div&gt;并用js和css将其伪装成&lt;a&gt;</li>
	<li>面包屑以频道首页开始，而不是网站首页开始.例如，网易首页&gt;网易汽车&gt;某频道&gt;某文章，应改为:网易汽车&gt;某频道&gt;文章汇总页&gt;某文章</li>
	<li>面包屑最后一项指向本页面时，不加链接,并且使用&lt;strong&gt;</li>
	<li>对同一地址的链接锚文字保持一致，若考虑UE/排版缘故，可在title属性中使用统一锚文字</li>
</ol>
&nbsp;
<h1 id="head-8a42a9286ea112ac5b09b1d9f84f7abcf2513710">链接统一</h1>
<ol type="1">
	<li>当URL做伪静态化后，将页面中动态的URL统统替换为静态化URL</li>
	<li>统一header/footer，以各自产品首页的header/footer为准
<ul>
	<li>header中应包含到本产品首页的链接(网页 图片 热闻 购物 音乐 视频 词典 翻译 更多)</li>
</ul>
</li>
	<li>当URL中出现统计代码时，在&lt;head&gt;标签中添加&lt;link rel="canonical" href="${不带任何统计参数，和无效参数的URL}"&gt;</li>
	<li>URI规范, 当http://auto.163.com/bj/ 和 <a href="http://auto.163.com/bj">http://auto.163.com/bj</a> 都可以访问时,统一使用前者,如果用浏览器打开后跳转,则使用跳转后的地址</li>
	<li>URI规范, 当http://dict.youdao.com/map/index.html和http://dict.youdao.com/map/ 都可以访问时,统一使用前者(考虑前端服务器rewrite规则冲突问题)</li>
</ol>
&nbsp;
<h1 id="head-78cb38bf6cb9608e108066744d5010e3d578c418">页面尺寸</h1>
<ul>
	<li>JS,CSS代码尽量不出现在&lt;header&gt;中，从外部引用，不同项目之间公用部分尽量合并</li>
	<li>页面输出之前删除无用空字符，回车，换行，空格，制表符，无用注释等</li>
	<li>全部采用html5标签定义 &lt;!DOCTYPE html&gt;</li>
</ul>
&nbsp;
<h1 id="head-c45f41d04352ad20acf9c49a16b643ef17ff76a6">隐藏内容</h1>
<ol type="1">
	<li>除tab切换等必要情况，禁止以任何形式故意隐藏大篇文字</li>
	<li>尽量不将大段文字放到图片中,若必须,请把文字复制到对应图片的alt=""中,css截取的图除外</li>
	<li>使用ajax方式显示内容应保证更换的内容不能超过10%,如果更换的内容超过50%应该使用普通超链接.</li>
</ol>
&nbsp;
<h1 id="head-081b21a814357b6124bc9bfc185661c051d1976d">程序</h1>
<ol type="1">
	<li>http GET参数造成页面无法正常返回内容时一定返回Respond Code 404。404页面最好能增加对应的推荐链接，对用户产生正向引导</li>
</ol>
&nbsp;
<h1 id="head-04f8355cd1566c42b464bbfd1954377dc887681e">关键词运用</h1>
<ol type="1">
	<li>关键词的选取
<ol type="1">
	<li>参考index.baidu.com的数值选取相关数值中平均指数最高者</li>
	<li>参考google adwords关键词工具，选取搜索量最高，竞争度不夸张者</li>
</ol>
</li>
	<li>关键词的放置，在不影响UI/UE的前提下，让关键词出现在
<ol type="1">
	<li>&lt;title&gt; 网页最浓缩的文字，相当于论文标题。每个url只可能有一个&lt;title&gt;，因此相当重要。
<ul>
	<li>不同url的title是不重复的。传统上标题一致的文章有抄袭嫌疑。</li>
	<li>禁止放置宣传性的、与主题不相关的大量文字。</li>
</ul>
</li>
	<li>&lt;h1&gt; heading(或headline)的缩写。本身是文档1级段落概要。现常见用于新闻标题，文章标题，用于介绍本页内容。
<ul>
	<li>禁止将&lt;h1&gt;用于LOGO</li>
</ul>
</li>
	<li>&lt;h2&gt; h1的子级内容概要，常见用户子栏目名称。用于介绍详细内容，软件功能等。</li>
	<li>&lt;strong&gt; 用于强调文字。只在有必要时使用，禁止滥用。</li>
	<li>&lt;a&gt; 相当于论文的“参考”，应当链接到与本页相关的网页。</li>
	<li>&lt;a title=""&gt; 相当于按钮提示，当锚文本与目标页面主题不相关时，需增加title以消除用户疑惑。
<ul>
	<li>&lt;a title="更多关于xxx的内容"&gt;更多&lt;/a&gt;</li>
	<li>&lt;a title="xxx"&gt;下一页&lt;/a&gt;</li>
</ul>
</li>
	<li>&lt;img alt=""&gt; alternation的缩写，当图片加载失败时浏览器使用alt文字替代图片。可用于增加，或稀释关键词密度。</li>
	<li>&lt;img title=""&gt; 对图片的鼠标悬浮注释。可用于增加，或稀释关键词密度</li>
	<li>&lt;meta name="keywords" content=""&gt; 相当于论文的"关键词"，便于论文搜索引擎收录和搜索。禁止增加与文章主题不相关的关键词。便于搜索引擎分词。</li>
	<li>&lt;meta name="keywords" description=""&gt; 相当于论文摘要，用于让读者在10秒钟内了解本文的内容，以便决定是否开始阅读。会展示于搜索引擎结果页面。禁止使用全站统一的宣传性文字，一定要生成有价值信息，以便提高点击率。</li>
	<li>任何视觉强化的文字区域</li>
</ol>
</li>
	<li>尽量保证关键词和其他文字不产生混淆，可使用_ | 《 》 " ' 【 】等符号隔离</li>
	<li>关键词在一段话、一个词组中的摆放、切割一定优先考虑UE和行为引导</li>
</ol>
补充,未整理

1、CSS命名避免使用focus作为名称。

2、页面中不要出现过多strong标签。

3、页面中h1只能唯一，并且指定为页面重要的标题（与项目管理人员确认）。

4、页面中，h2~h6标题要按照等级顺序书写。

5、Img标签中不能缺少alt属性

6、图片标题使用图片作为背景，缩进隐藏文字，使搜索引擎可以抓取关键词。

7、文字使用CSS进行文字截取以符合搜索引擎对文字的抓取（与页面发布工程师确 认）。

8、在不影响用户体验的情况下给链接加title属性

9、在不影响用户体验的情况下给图片加title属性

10、对于产品页，每个细栏目名称必须是文字，建议是&lt;h2&gt;，如果冲突可降级(用 &lt;h3&gt;等等)

11、对于产品页，图片下方必须有文字区域

12、通过外部调用的方式使用JS，如果JS必须放到页面中，建议放到主内容以下的位置

13、对每个详情页正文上方增加面包屑

14、代码符合xhtml标准

&nbsp;

-===============以下来自经纬同学=============
1、dns轮训数量

2、与设定无差异的图片尺寸

3、合并脚本

4、在固定尺寸下可再压缩的图片

5、css是否放在头部

6、同一文件统一的路径

7、静态池的cookies

8、压缩传输

9、压缩css

10、压缩html

11、压缩javascript

12、较少的dom节点（500，1000，1500，&gt;2000）

13、没有404错误

14、较少的并发链接

15、css不适用expression

16、css不适用filter滤镜

17、favicon可缓存

</div>
</div>
