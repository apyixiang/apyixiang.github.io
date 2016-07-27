---
layout: post
title: "Android shape的使用详解"
date: 2015-12-21 11:10
comments: true
categories: dev
tags: [android,shape]
---

----------

写在最前：不管在什么系统中，如果你应用的图片资源比较多的话，会导致安装包较大，比如四角有弧度的长方形、圆形、正方形等等简单图形，完全没有比较实用图片，在Android中如何优雅的避免这个问题呢，就是使用shape了。

----------
**1.新建文件**

首先在你的项目下新建drawable文件夹，你的shape xml文件就放到这个地下，然后新建Android xml文件，如图：

![新建xml文件](http://upload-images.jianshu.io/upload_images/1346485-29e95d718b71bbe4?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**2.下面来介绍一下shape的属性**

![属性](http://upload-images.jianshu.io/upload_images/1346485-df3dfa92c5dc554c?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

如图，shape有6个属性，分别为：

 - corners：设置圆角，即四个角的弧度
 - gradient：颜色渐变
 - padding：间隔，xml里经常用到，不比多解释
 - size：长宽
 - solid：填充物，只有一个属性 -> 颜色
 - stroke：设置图片边缘颜色

来看一下官方给我的详细解释：

```xml
<?xml version="1.0" encoding="utf-8"?>
<shape
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape=["rectangle" | "oval" | "line" | "ring"] >
    <corners
        android:radius="integer"
        android:topLeftRadius="integer"
        android:topRightRadius="integer"
        android:bottomLeftRadius="integer"
        android:bottomRightRadius="integer" />
    <gradient
        android:angle="integer"
        android:centerX="integer"
        android:centerY="integer"
        android:centerColor="integer"
        android:endColor="color"
        android:gradientRadius="integer"
        android:startColor="color"
        android:type=["linear" | "radial" | "sweep"]
        android:useLevel=["true" | "false"] />
    <padding
        android:left="integer"
        android:top="integer"
        android:right="integer"
        android:bottom="integer" />
    <size
        android:width="integer"
        android:height="integer" />
    <solid
        android:color="color" />
    <stroke
        android:width="integer"
        android:color="color"
        android:dashWidth="integer"
        android:dashGap="integer" />
</shape>
```

形状的属性，只有这6种，下面详细介绍一下6种属性下的各个属性的意义，

**1）.corners：Creates rounded corners for the shape. Applies only when the shape is a rectangle.创建圆角的形状。仅适用于当其形状是一个长方形

```
android:radius="20dp"  为角的弧度，值越大角越圆。
android:topRightRadius="20dp"  右上角
android:bottomLeftRadius="20dp"   右下角
android:topLeftRadius="1dp"   左上角
android:bottomRightRadius="0dp"   左下角
```

> **一个提示：bottomLeftRadius  是右下角，而不是左下角，谨记谨记，其实记反了也没有多大影响。**


**2）.gradient：Specifies a gradient color for the shape.指定一个渐变颜色的形状。**
```
android:startColor  起始颜色
android:endColor  结束颜色
android:centerColor  中心颜色
android:angle  渐变角度，必须为45的整数倍。
android:type  渐变模式默认为linear，即线性渐变，可以指定渐变为径向渐变，android:type="radial"
android:gradientRadius="50"  径向渐变需要指定半径
android:useLevel 值为true或false，至今不知道有什么作用
```

**3）padding ： 定义内容离边界的距离**

```
android:bottom="2dp"
android:left="2dp"
android:right="2dp"
android:top="2dp"
```
略

**4）size：The size of the shape.形状的长宽**

```
android:height="100dp"
android:width="100dp"
```
略

**5）solid ：A solid color to fill the shape.填充颜色**

```
android:color  指定填充的颜色
```

**6）stroke：A stroke line for the shape.图形边缘画线**

```
android:width="2dp"  描边的宽度
android:color="#FFFFFF"  描边的颜色
android:dashWidth  虚线中这样一个'-'横线的宽度
android:dashGap  两个'-'之间的距离
```