---
layout: post
title: "Android Uri的用途"
data: 2014-02-10 15:35
comments: true
categories: dev
tags: [android]
---

Android Uri位于android.net包下
1，调web浏览器  
Uri myBlogUri = Uri.parse(" http://xxxxx.com ");  
returnIt = new Intent(Intent.ACTION_VIEW, myBlogUri);  
2，地图  
Uri mapUri = Uri.parse("geo:38.899533,-77.036476");  
returnIt = new Intent(Intent.ACTION_VIEW, mapUri);  
3，调拨打电话界面  
Uri telUri = Uri.parse("tel:100861");  
returnIt = new Intent(Intent.ACTION_DIAL, telUri);  
4，直接拨打电话  
Uri callUri = Uri.parse("tel:100861");  
returnIt = new Intent(Intent.ACTION_CALL, callUri);  
5，卸载  
Uri uninstallUri = Uri.fromParts("package", "xxx", null);  
returnIt = new Intent(Intent.ACTION_DELETE, uninstallUri);  
6，安装  
Uri installUri = Uri.fromParts("package", "xxx", null);  
returnIt = new Intent(Intent.ACTION_PACKAGE_ADDED, installUri);  
7，播放  
Uri playUri = Uri.parse("file:///sdcard/download/everything.mp3");  
returnIt = new Intent(Intent.ACTION_VIEW, playUri);  
8，调用发邮件  
Uri emailUri = Uri.parse("mailto:xxxx@gmail.com");  
returnIt = new Intent(Intent.ACTION_SENDTO, emailUri);  
9，发邮件  
returnIt = new Intent(Intent.ACTION_SEND);  
String[] tos = { "xxxx@gmail.com" };  
String[] ccs = { "xxxx@gmail.com" };  
returnIt.putExtra(Intent.EXTRA_EMAIL, tos);  
returnIt.putExtra(Intent.EXTRA_CC, ccs);  
returnIt.putExtra(Intent.EXTRA_TEXT, "body");  
returnIt.putExtra(Intent.EXTRA_SUBJECT, "subject");  
returnIt.setType("message/rfc882");  
Intent.createChooser(returnIt, "Choose Email Client");  
10，发短信  
Uri smsUri = Uri.parse("tel:100861");  
returnIt = new Intent(Intent.ACTION_VIEW, smsUri);  
returnIt.putExtra("sms_body", "yyyy");  
returnIt.setType("vnd.android-dir/mms-sms");  
11，直接发邮件  
Uri smsToUri = Uri.parse("smsto://100861");  
returnIt = new Intent(Intent.ACTION_SENDTO, smsToUri);  
returnIt.putExtra("sms_body", "yyyy");  
12，发彩信  
Uri mmsUri = Uri.parse("content://media/external/images/media/23");  
returnIt = new Intent(Intent.ACTION_SEND);  
returnIt.putExtra("sms_body", "yyyy");  
returnIt.putExtra(Intent.EXTRA_STREAM, mmsUri);  
returnIt.setType("image/png"); 
