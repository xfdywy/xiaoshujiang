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
这里需要配置一下密码登录，如果你不配置密码登录。你就需要输入一个token，显示在命令行里面，我觉得有点麻烦，还是设置一个密码比较好。

# 配置密码
如果没有config文件(默认在  c:/User/< your user name>/.jupyter/jupyter_notebook_config.py )，执行下面这个
```
jupyter notebook --generate-config
```
然后执行
```
jupyter notebook password
```
输入你的密码，生成对应的hash值，放到config文件的同目录下了（自动）

应该已经可以了。试试在浏览器里面输入localhost:8080 ，如果还是不行，就手动把生成的```jupyter_notebook_config.json```里面的password后面的， 复制到 ```jupyter_notebook_config.py```中
找到下面这行并修改
```
c.NotebookApp.password = u'sha:ce...刚才复制的那个密文'
```
进去之后就是这样了
![enter description here](https://img-1253424161.cos.ap-shanghai.myqcloud.com/xsj/2018/4/1524829854782.jpg)

下一个问题就是如何配置多个kernel了。
# 配置python2 python3 r的kernel
 ## R kernel
 如果你已经安装了r，那么在r的命令行下输入
 

``` r
install.packages(c('pbdZMQ', 'repr', 'devtools')) 
devtools::install_github('IRkernel/IRkernel') 
IRkernel::installspec()
```

## 多个python kernel
如果你的多个python 是安装在多个环境中的，就是用activate < env_name >这样的语句可以进入不同的环境的话，可以这样操作，下面假定python 3.5 安装在py35 的环境里面，

``` bash
acitvate py35   (or source activate py35)
python -m ipykernel install --name py35
deactivate (or source deactivate)
```
其他同理。