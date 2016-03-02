---
layout: post
title: 关于onSaveInstanceState的一点小误解
category: Android开发经验
tags: Android
keywords: Android,onSaveInstanceState，经验
description: 使用onSaveInstaceState的时候遇到的理解偏差
---
在SearchActivity中，希望加上一个onSaveInstanceState()来保存用户已经输入的数据于是就加了这么一段话

	@Override  
    protected void onSaveInstanceState(Bundle outState){  
        super.onSaveInstanceState(outState);  
        String tempData = editText.getText().toString();  
        outState.putString(EDIT_TEXT_TEMP_STRING, tempData);  
    }  

重写这个函数旨在保留用户暂时输入的内容。
原本以为是在onDestroy是会执行这个函数。onCreate时重拿数据，但发现不是这样
onSaveInstanceState是在这两种情况下执行：

- 按了home键。
- 内存不足被系统意外销毁。

用户自己按back是不会执行的。其实想想也是这个道理，因为用户都按了返回键了，他自然是不想保存输入框中已输入的东西，只有在输入到一半，被其他任务打断的情况下才会去保存这些数据。