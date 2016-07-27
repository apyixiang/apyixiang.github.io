---
layout: post
title: "[Android]ImageView的scaleType与adjustViewBounds属性"
date: 2016-01-13 14:27
comments: true
categories: dev
tags: [android,view]
---

ImageView的Scaletype决定了图片在View上显示时的样子，如进行何种比例的缩放，及显示图片的整体还是部分，等等。
设置的方式包括：

1. 在layout xml中定义android:scaleType="CENTER"
2. 或在代码中调用imageView.setScaleType(ImageView.ScaleType.CENTER);

**scaleType属性如下：**
- android:scaleType="matrix"不改变原图的大小，从ImageView的左上角开始绘制原图，原图超过ImageView的部分作裁剪处理。

- android:scaleType="center"按图片的原来size居中显示，当图片长/宽超过View的长/宽，则截取图片的居中部分显示

- android:scaleType="centerCrop"; 按比例扩大图片的size居中显示，使得图片长(宽)等于或大于View的长(宽) 

- android:scaleType="centerInside"将图片的内容完整居中显示，通过按比例缩小或原来的size使得图片长/宽等于或小于View的长/宽 

- android:scaleType="fitCenter"把图片按比例扩大/缩小到View的宽度，居中显示

- android:scaleType="fitStart", android:scaleType="fitEnd"在图片缩放效果上与FIT_CENTER一样，只是显示的位置不同，FIT_START是置于顶部，FIT_CENTER居中，FIT_END置于底部。

- android:scaleType="fitXY"，不按比例缩放图片，目标是把图片塞满整个View。
*效果图如下：*

![效果图](http://upload-images.jianshu.io/upload_images/1346485-07cf0fcce37636fa.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

ImageView的android:adjustViewBounds属性为是否保持原图的长宽比，单独设置不起作用，需要配合maxWidth或maxHeight一起使用。