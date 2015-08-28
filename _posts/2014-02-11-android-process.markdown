---
layout: post
title: "Android 进程重要性等级"
date: 2015-08-28 11:25
comments: true
categories: dev
tags: [android,process]
---

前言『Android进程中有许多需要学习的地方，在这里简单介绍一下进程重要性等级的一些知识』
下面是关于进程属性importance的介绍

```java
        /**
         * The relative importance level that the system places on this
         * process.  May be one of {@link #IMPORTANCE_FOREGROUND},
         * {@link #IMPORTANCE_VISIBLE}, {@link #IMPORTANCE_SERVICE},
         * {@link #IMPORTANCE_BACKGROUND}, or {@link #IMPORTANCE_EMPTY}.  These
         * constants are numbered so that "more important" values are always
         * smaller than "less important" values.
         */
        public int importance;
```

其意思概括来说就是，进行重要性是相对来说的，重要性等级分为5种，前台进程，可见进程，服务进程，后台进程和空进程。并且这个值越小，它的重要程度越大。下面来简单介绍一些这5种进程：

1.前台进程：

```java 
        /**
         * Constant for {@link #importance}: this process is running the
         * foreground UI.
         * 处在UI界面最前面的process的importance值为100
         */
        public static final int IMPORTANCE_FOREGROUND = 100;
```
屏幕上显示的进程。我们最不希望结束的进行就是前台进行，所以它的importance最小。

2.可见进程：

```java 
        /**
         * Constant for {@link #importance}: this process is running something
         * that is actively visible to the user, though not in the immediate
         * foreground.
         * 正在运行的App，处于用户可见的importance的值为200，
         */
        public static final int IMPORTANCE_VISIBLE = 200;
```
可见进程是一些不在前台，但用户依然可见的进程，举个例来说：widget、输入法等，都属于visible。这部分进程虽然不在前台，但与我们的使用也密切相关，我们也不希望它们被终止（你肯定不希望时钟、天气，新闻等widget被终止，那它们将无法同步，你也不希望输入法被终止，否则你每次输入时都需要重新启动输入法）

3.服务进程：分为主要服务、次要服务
```java 
        /**
         * Constant for {@link #importance}: this process is contains services
         * that should remain running.
         */
        public static final int IMPORTANCE_SERVICE = 300;
```
目前正在运行的一些服务（主要服务，如拨号等，是不可能被进程管理终止的，故这里只谈次要服务），举例来说：谷歌企业套件，Gmail内部存储，联系人内部存储等。这部分服务虽然属于次要服务，但很一些系统功能依然息息相关，我们时常需要用到它们，所以也太希望他们被终止。

4.后台服务：
```java 
        /**
         * Constant for {@link #importance}: this process process contains
         * background code that is expendable.
         */
        public static final int IMPORTANCE_BACKGROUND = 400;
```
就是我们通常意义上理解的启动后被切换到后台的进程，如浏览器，阅读器等。当程序显示在屏幕上时，他所运行的进程即为前台进程（foreground），一旦我们按home返回主界面（注意是按home，不是按back），程序就驻留在后台，成为后台进程（background）。

后台进程的管理策略有多种：有较为积极的方式，一旦程序到达后台立即终止，这种方式会提高程序的运行速度，但无法加速程序的再次启动；也有较消极的方式，尽可能多的保留后台程序，虽然可能会影响到单个程序的运行速度，但在再次启动已启动的程序时，速度会有所提升。这里就需要用户根据自己的使用习惯找到一个平衡点

5.空进程：
```java 
        /**
         * Constant for {@link #importance}: this process is empty of any
         * actively running code.
         */
        public static final int IMPORTANCE_EMPTY = 500;
```
没有任何东西在内运行的进程，有些程序，比如BTE，在程序退出后，依然会在进程中驻留一个空进程，这个进程里没有任何数据在运行，作用往往是提高该程序下次的启动速度或者记录程序的一些历史信息。 这部分进程无疑是应该最先终止的。

6.在官方文档中还给出了三种进行的importance值，分别为：可触摸到的、可保存状态和不存在的进程(搞不懂这个是用来干什么的)

```java 
        /**
         * Constant for {@link #importance}: this process is running something
         * that is considered to be actively perceptible to the user.  An
         * example would be an application performing background music playback.
         */
        public static final int IMPORTANCE_PERCEPTIBLE = 130;
```
```java 
        /**
         * Constant for {@link #importance}: this process is running an
         * application that can not save its state, and thus can't be killed
         * while in the background.
         *
         * @hide
         */
        public static final int IMPORTANCE_CANT_SAVE_STATE = 170;
```
```java 
        /**
         * Constant for {@link #importance}: this process does not exist.
         */
        public static final int IMPORTANCE_GONE = 1000;
```
在这里就不具体介绍他们是用来干什么的了。
