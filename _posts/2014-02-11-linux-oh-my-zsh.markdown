---
layout: post
title: "Android 进程重要性等级"
date: 2015-08-28 11:25
comments: true
categories: dev
tags: [android,process]
---
##Android 进程重要性

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
```java 
/**
         * Constant for {@link #importance}: this process is running the
         * foreground UI.
         * 处在UI界面最前面的process的importance值为100
         */
        public static final int IMPORTANCE_FOREGROUND = 100;

        /**
         * Constant for {@link #importance}: this process is running something
         * that is actively visible to the user, though not in the immediate
         * foreground.
         * 正在运行的App，处于用户可见的importance的值为200，
         */
        public static final int IMPORTANCE_VISIBLE = 200;

        /**
         * Constant for {@link #importance}: this process is running something
         * that is considered to be actively perceptible to the user.  An
         * example would be an application performing background music playback.
         */
        public static final int IMPORTANCE_PERCEPTIBLE = 130;

        /**
         * Constant for {@link #importance}: this process is running an
         * application that can not save its state, and thus can't be killed
         * while in the background.
         *
         * @hide
         */
        public static final int IMPORTANCE_CANT_SAVE_STATE = 170;

        /**
         * Constant for {@link #importance}: this process is contains services
         * that should remain running.
         */
        public static final int IMPORTANCE_SERVICE = 300;

        /**
         * Constant for {@link #importance}: this process process contains
         * background code that is expendable.
         */
        public static final int IMPORTANCE_BACKGROUND = 400;

        /**
         * Constant for {@link #importance}: this process is empty of any
         * actively running code.
         */
        public static final int IMPORTANCE_EMPTY = 500;

        /**
         * Constant for {@link #importance}: this process does not exist.
         */
        public static final int IMPORTANCE_GONE = 1000;
```
