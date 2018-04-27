---
title:  Jupyter lab 安装及多kernel配置
date: 2018-4-27
tags:
    -   
categories:  
---


 Jupyter lab 是Jupyter notebook 的升级版，是ipython notebook的升级版。
 大体来说就是用浏览器作为IDE，编写代码边运行，并且保留结果。形成像notebook一样的一份文档。
 
 Jupyter lab 的安装很简单，假定已经安装了anaconda了。那么已经有了Jupyter notebook了，这个时候安装只需要一句命令：
 

``` 
pip install jupyterlab
或者
conda install -c conda-forge jupyterlab
```

安装好了启动也是非常简单，在命令行输入

``` bash
jupyter lab
```
就ok了。当然也可以进行一些配置, 与jupyternotebook 的配置完全一致。你可以输入```jupyter lab -h``` 来进行查看。例如

``` bash
jupyter lab --port='8080' --ip='*' --notebook-dir='d:/'
```
就是指运行在8080端口，可以从任意ip访问（可以远程机器直接连过来），工作路径为d盘根目录。

看到一连串输出后就可以打开浏览器访问了，ip:port 就可以了。如果在本机就是localhost:8080(一般会弹出浏览器)。
这里需要配置一下密码登录，如果你不配置密码登录。你就需要输入一个token，显示在命令行里面，我觉得有点麻烦，还是设置一个密码比较好
进去之后就是这样了
![enter description here](https://img-1253424161.cos.ap-shanghai.myqcloud.com/xsj/2018/4/1524829854782.jpg)

下一个问题就是如何配置多个kernel了。
# 配置python2 python3 r的kernel
 ## R kernel