---
title:  支持Python3的腾讯云 对象存储 cos python3 sdk 
date: 2018-4-9  
tags:
    - py2to3
    - 腾讯云cos
    - qcloud_cos_py3
categories: python 
---


今天填了一天的坑。成果是 qcloud_cos_py3.
腾讯云的cos python sdk cos-python-sdk-v5 只支持python2.7， 而我的qt项目要 python3.* .

于是就自己动手写了一个Python 3.* 的sdk。

其实也就是在2.7版本的基础上，修改了所有不兼容的函数和用法。
这里先贴一个地址，如果有需要的可以自取，我自己试用了基本功能，没发现bug。并且大部分都是与源代码保持一致，有bug的可能性很小。

下载文件就可以直接import的：
 https://github.com/xfdywy/qcloud_cos_py3
 
 可以像官方那样安装后直接import的：
 https://github.com/xfdywy/cos-python-sdk-v5
 
 有问题请留言或者去github提issue。
 
 后续会把心得（填坑过程）贴出来。一周内把。督促一下自己。
