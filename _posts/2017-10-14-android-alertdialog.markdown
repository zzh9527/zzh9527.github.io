---
layout: post
title: "Android中的AlertDialog"
subtitle: "AlertDialog"
date: 2017-10-14 21:08:00
author: "ZZH"
header-img: "img/in-post/post-eleme-pwa/eleme-at-io.jpg"
header-mask: 0.3
catalog: true
tags:
  - android
---


>   Android学习中遇到的小问题
 


## 创建对话框

在练习使用alertdialog创建对话框时，想在里面添加几个常用按钮，于是按照书上的方法添加代码，但setbutton里面的new OnClickListener()总报错，代码如下： alert.setButton(DialogInterface.BUTTON_NEGATIVE, "确认",  new OnClickListener(){··· 错误原因是不识别OnClickListener()这个类型；后来在网上发现，原来应改为 new  DialogInterface.OnClickListener() 原来是导入的包不同，应该多导入一个包import android.view.DialogInterface.OnClickListener; 
## 用户注册信息

两个Activity中，最后需要显示用户注册信息界面的用户名，密码，email从EditText中获取数据。
