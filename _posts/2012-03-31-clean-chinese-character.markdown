---
layout: post
title: "清理非中文字符的方法"
date: 2012-03-31 04:51
comments: true
categories: dev
tags: [ruby,unicode,utf8]
---
总之就是用正则替换，察看utf-8编码范围

其中cjk是chinese japan korean的意思，其中ideographs是“象形文字”的意思

因此我就取其中u4E00 - u9FFF 这个范围(CJK unified ideographs: Han characters used in China, Japan, Korea, Taiwan, and Vietnam)

ruby的代码这样写

```ruby
puts line.gsub(/[^\u4E00-\u9FFF]/,'')
```

注意如果还需要保留英文和数字,记得排除掉:

```ruby
puts line.gsub(/[^\w0-9\u4E00-\u9FFF]/,'')
```

其他语言也差不多吧

完整的编码范围描述：

```
u0000 - u1FFF,Alphabets
u0020 - u007F,Basic Latin
u0080 - u00FF,Latin-1 supplement
u0100 - u017F,Latin extended-A
u0180 - u024F,Latin extended-B
u0250 - u02AF,IPA extensions
u02B0 - u02FF,Spacing modifier letters
u0300 - u036F,Combining diacritical marks
u0370 - u03FF,Greek
u0400 - u04FF,Cyrillic
u0530 - u058F,Armenian
u0590 - u05FF,Hebrew
u0600 - u06FF,Arabic
u0900 - u097F,Devanagari
u0980 - u09FF,Bengali
u0A00 - u0A7F,Gurmukhi
u0A80 - u0AFF,Gujarati
u0B00 - u0B7F,Oriya
u0B80 - u0BFF,Tamil
u0C00 - u0C7F,Telugu
u0C80 - u0CFF,Kannada
u0D00 - u0D7F,Malayalam
u0E00 - u0E7F,Thai
u0E80 - u0EFF,Lao
u0F00 - u0FBF,Tibetan
u10A0 - u10FF,Georgian
u1100 - u11FF,Hangul Jamo
u1E00 - u1EFF,Latin extended additional
u1F00 - u1FFF,Greek extended
u2000 - u2FFF,Symbols and punctuation
u2000 - u206F,General punctuation
u2070 - u209F,Superscripts and subscripts
u20A0 - u20CF,Currency symbols
u20D0 - u20FF,Combining diacritical marks for symbols
u2100 - u214F,Letterlike symbols
u2150 - u218F,Number forms
u2190 - u21FF,Arrows
u2200 - u22FF,Mathematical operators
u2300 - u23FF,Miscellaneous technical
u2400 - u243F,Control pictures
u2440 - u245F,Optical character recognition
u2460 - u24FF,Enclosed alphanumerics
u2500 - u257F,Box drawing
u2580 - u259F,Block elements
u25A0 - u25FF,Geometric shapes
u2600 - u26FF,Miscellaneous symbols
u2700 - u27BF,Dingbats
u3000 - u33FF,CJK auxiliary
u3000 - u303F,CJK symbols and punctuation
u3040 - u309F,Hiragana
u30A0 - u30FF,Katakana
u3100 - u312F,Bopomofo
u3130 - u318F,Hangul compatibility Jamo
u3190 - u319F,Kanbun
u3200 - u32FF,Enclosed CJK letters and months
u3300 - u33FF,CJK compatibility
u4E00 - u9FFF,CJK unified ideographs: Han characters used in China, Japan, Korea, Taiwan, and Vietnam
uAC00 - uD7A3,Hangul syllables
uD800 - uDFFF,Surrogates
uD800 - uDB7F,High surrogates
uDB80 - uDBFF,High private use surrogates
uDC00 - uDFFF,Low surrogates
uE000 - uF8FF,Private use
uF900 - uFFFF,Miscellaneous
uF900 - uFAFF,CJK compatibility ideographs
uFB00 - uFB4F,Alphabetic presentation forms
uFB50 - uFDFF,Arabic presentation forms-A
uFE20 - uFE2F,Combing half marks
uFE30 - uFE4F,CJK compatibility forms
uFE50 - uFE6F,Small form variants
uFE70 - uFEFE,Arabic presentation forms-B
uFF00 - uFFEF,Halfwidth and fullwidth forms
uFFF0 - uFFFF,Special
```