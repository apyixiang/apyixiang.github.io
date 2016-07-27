---
layout: post
title: "Android自定义控件-EditText(可用于登陆界面)"
date: 2015-12-19 18:59
comments: true
categories: dev
tags: [android,view]
---

----------
**最近在研究前辈写的代码，看到了有关于登陆界面的用户名和密码，使用的是自定义EditText的，所以写两篇相关文章来记录。**
----------

其实用户名和密码使用的EditText控件非常相似，拿用户名处使用的控件为例，它包括如下功能：

 - 在没内容的时候，不显示清除按钮，在有内容的时候，显示清除按钮
 - 在有内容的时候，点击清除按钮可以删除EditText中的内容

而在密码处使用的控件，包括如下功能：

 - 在没内容的时候，密码可见按钮不可用，在有内容的时候，显示密码可见按钮
 - 在有内容的时候，点击密码可见按钮即可显示密码

话不多说，开始写代码。

**1.首先继承EditText，添加三个构造函数，如下：**

```java
public DIYEditText(Context context) {
		super(context);
}

public DIYEditText(Context context, AttributeSet attrs) {
		super(context, attrs, android.R.attr.editTextStyle);
}

public DIYEditText(Context context, AttributeSet attrs, int defStyle){
		super(context, attrs, defStyle);
}
```
**2.为你自定义的EditText设置一些简单属性**

如背景图片或者是背景颜色，

![设置背景图片](http://upload-images.jianshu.io/upload_images/1346485-a67e76b08a8283e8?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

设置控件左侧图片，

![设置左侧图片](http://upload-images.jianshu.io/upload_images/1346485-b60fa2dbc3a8c4ac?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

看到此处的`getCompoundDrawables()[0]`，有人会比较疑惑，那么让我们来看一下这个东西到底是什么鬼，F3跳入函数，下面代码，

![函数](http://upload-images.jianshu.io/upload_images/1346485-16849d496076aa16?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

原来EditText是TextView的子类，而在TextView的上下左右设置4张图片，我们可以通过`getCompoundDrawables()`函数来获取这四张图片，然后再给它们通过`setCompoundDrawables()`来赋值，就可以显示我们想要的图片了。

**3.右侧删除按钮监听事件的设置**

首先我们得在控件没内容的时候，不显示清除按钮，有内容的时候才显示清除按钮，所以我们可以根据内容的长短来实现这一功能，并且继承TextWatcher，实现其中的三个函数，在`onTextChanged`中调用如下函数，才能实现

```java
    // 设置删除图片
	private void setClearDrawable() {
		if (length() < 1)
			setClearIconVisible(false);
		else
			setClearIconVisible(true);
	}
	/**
	 * 设置清除图标的显示与隐藏，调用setCompoundDrawables为EditText绘制上去
	 * 
	 * @param visible
	 */
	protected void setClearIconVisible(boolean visible) {
		setCompoundDrawables(getCompoundDrawables()[0],
				getCompoundDrawables()[1], visible ? mClearDrawable : null,
				getCompoundDrawables()[3]);
	}
```

删除按钮的点击事件，可以利用onTouchEvent函数来实现，

```java
    /**
	 * 点击删除按钮，清理内容
	 */
	@SuppressLint("ClickableViewAccessibility")
	@Override
	public boolean onTouchEvent(MotionEvent event) {
		if (event.getAction() == MotionEvent.ACTION_UP) {
			if (getCompoundDrawables()[2] != null) {
				boolean touchable = event.getX() > (getWidth() - getTotalPaddingRight())
						&& (event.getX() < ((getWidth() - getPaddingRight())));

				if (touchable) {
					this.setText("");
				}
			}
			this.setFocusable(true);
			this.setFocusableInTouchMode(true);
			this.requestFocus();
		}
		return super.onTouchEvent(event);
	}
```

**4.密码所用的EditText与上述的大同小异**

这里主要讲解一下，密码是否可见的设置，
首先必须有两个Drawable，一个是密码可见时显示的图片，另外一个是密码不可见时显示的图片，

```java
		mCloseDrawable = getCompoundDrawables()[2];
		mCloseDrawable = getResources().getDrawable(R.drawable.pwd_close);
		mCloseDrawable.setBounds(0, 0,
				(int) (mCloseDrawable.getIntrinsicWidth() * 0.65),
				(int) (mCloseDrawable.getIntrinsicHeight() * 0.65));
		
		mOpenDrawable = getCompoundDrawables()[2];
		mOpenDrawable = getResources().getDrawable(R.drawable.pwd_open);
		mOpenDrawable.setBounds(0, 0,
				(int) (mCloseDrawable.getIntrinsicWidth() * 0.65),
				(int) (mCloseDrawable.getIntrinsicHeight() * 0.65));
```

随后设置图片的点击事件，获取当前是否处于可见状态，代码如下：

```java
/**
	 * 设置密码是否可见图标
	 */
	private void setPwdDrawable(boolean visiable) {
		Drawable right = visiable ? mOpenDrawable : mCloseDrawable;
		setCompoundDrawables(getCompoundDrawables()[0],
				getCompoundDrawables()[1], right, getCompoundDrawables()[3]);
	}

	@Override
	public boolean onTouchEvent(MotionEvent event) {
		if (event.getAction() == MotionEvent.ACTION_UP) {
			if (getCompoundDrawables()[2] != null) {
				boolean touchable = event.getX() > (getWidth() - getTotalPaddingRight())
						&& (event.getX() < ((getWidth() - getPaddingRight())));

				if (touchable) {
					if (this.getInputType() == InputType.TYPE_TEXT_VARIATION_PASSWORD) {
						this.setInputType(InputType.TYPE_CLASS_TEXT
								| InputType.TYPE_TEXT_VARIATION_PASSWORD);
						Editable etable = this.getText();
						Selection.setSelection(etable, etable.length()); // 隐藏
						setPwdDrawable(false);
					} else {
						this.setInputType(InputType.TYPE_TEXT_VARIATION_PASSWORD);
						Editable etable = this.getText();
						Selection.setSelection(etable, etable.length()); // 显示
						setPwdDrawable(true);
						this.invalidate();
					}
				}
			}
		}
		return super.onTouchEvent(event);
	}
```

**整个自定义控件核心代码如上，有何不足请各位多多指教。**

代码地址：由于CSDN上传有问题，只能暂时放百度云了。

http://pan.baidu.com/s/1jGXZeiq 密码：brrn