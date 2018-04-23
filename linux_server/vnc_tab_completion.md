---
title:  
date: 2018-3-29 00:00:19
tags:
    -   
categories:  
---

vnc 连接服务器 使用 Xfce desktop tab 键不能自动补全
这是因为tab键被系统默认为是 switch window的快捷键了，修改了就好了

> Application Menu > Settings > Window Manager 
> 选择 Keyboard 标签 清除 Switch
> window  的快捷键设置

vnc 连接服务器 使用xfce desktop  系统时间，桌面切换等图标没有靠右，类似于windows右下键的时间状态栏等，看起来很难受。设置方法为：
> 面板空白处右击 > panel > panel preferences > items
> 点右边的加号，新建一个separator（分隔符），选中新建的separator，用上下按钮调整位置，分隔符后面的都靠右
> 双击 separator，保证 设置成expand
> 完成， 最终设置大概是这样
> ![vnc panel](https://img-1253424161.cos.ap-shanghai.myqcloud.com/xsj/2018/4/1523849612319.jpg)
