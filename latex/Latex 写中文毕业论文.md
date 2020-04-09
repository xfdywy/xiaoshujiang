---
title:  Latex 写中文毕业论文
date: 2019-3-
tags:
    -   Latex
    -   中文
categories: coding
---


最近疫情在家写毕业论文，前期折腾了一下latex模版的相关事情，算是搞的比较清楚了，所以后期论文写起来也比较顺利，遇到问题也可以随时解决。现在论文也搞得差不多了，准备记录一下

主要分成下面几个部分来总结一下latex写中文毕业论文的相关问题

1. latex安装与编辑器的使用
2. 模版与编译器
3. 论文中会遇到的一些问题及解决办法


# latex安装与编辑器的使用


## 下载与安装
肯定有很多人 ~~（包括我自己）~~还在使用甚至还在推荐别人使用CTeX套装，注意我的用词不要引起歧义哈。我说的这个ctex套装指的是那个下载下来安装好就又有latex可以用，又帮你按了一个winedit的那个套装，一般是在下面这个网址下载的

> http://www.ctex.org/HomePage

但是我想说的是，除非有什么上古代码必须要这个，**尽量还是别安装这个了**。
原因有两点

1. 太旧了，很久都没人维护了
2. 安装有风险，很多人报告有某种位置情况下会覆盖系统的Path变量

那么去哪里下载什么呢，我建议下载最新的texlive，原因是：

>我看网上说还挺好用，然后我自己试了一下确实没出啥问题

下载地址在这里：https://www.tug.org/texlive/

嫌弃官网慢的话，清华大学镜像也是挺不错的， 这里下载 https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/Images/texlive2019.iso

下载下来，挂载好镜像文件（这个就不写了哈，大家可以自己搜啥叫挂载镜像文件，或者来[这里看](https://buhuibaidu.me/?s=windows%E6%8C%82%E8%BD%BDios%E9%95%9C%E5%83%8F)），就可以安装了。
没记错的话里面有一个 install-tl-windows.bat 文件，双击就可以安装了。

安装大约需要1个小时（都不一定够）安装好以后，可以把安装的路径加入系统变量Path里面，以便后面说的编辑器调用。安装路径指的是类似下面这样的路径，最后一定是bin\win32,因为这个文件夹里面才有各种exe程序。

> C:\texlive\2019\bin\win32


## 写论文用到的编辑器
这个话题有点引战。。我就说我咋写的吧，我本人主要用texstudio，偶尔用vscode+latex workshop插件。


texstudio官网下载就好，http://www.texstudio.org/ ， 简单易用，几乎0配置，界面也友好。



# 模版与编译器
我是北京交通大学的，我们学校没有官方latex模版，但是有大佬们做了一个非官方的，还是与word版本有些不同，我自己又改了改，终于算是几乎一模一样了。

模版基本就是一个.cls文件，在里面定义了论文的各个章节模块的格式。

这个模版需要用xelatex进行编译，别忘了在编辑器里面把编译工具换成xelatex，texstudio默认的话好像是pdflatex。 

.


# 遇到的问题

## xelatex在windows 10系统上（至少在win10上）太慢了
解决方法：在安装目录下找到xelatex.exe，就刚刚添加到Path里面的那个文件夹下面，然后

1. 右击
2. 属性
3. 兼容性
4. 以兼容模式运行这个程序
5. windows7

知乎上这个问题下面的回答大家也可以试试 https://www.zhihu.com/question/53981204 。

反正我昨晚以后速度就还能接受了。不编译很多图片的情况下，100页左右的论文也就不到一分钟。


## 图标标题如何中英文两行，中文在上，英文在下

使用 \usepackage{bicaption} 这个包

然后在论文开始之前设置如下

``` markdown
\captionsetup[figure][bi-first]{name=图}
\captionsetup[figure][bi-second]{name=Figure}

\captionsetup[table][bi-first]{name=表}
\captionsetup[table][bi-second]{name=Table}
```


## 如何在用了不标号的公式环境中单独标号一行

``` tex
\newcommand\numberthis{\addtocounter{equation}{1}\tag{\theequation}}
```
之后如果在align* 这样的环境中，想给某一行单独标号，可以在那一行最后用这个命令 \numberthis

## 算法框中文

``` tex
\usepackage[ruled,linesnumbered]{algorithm2e}
\renewcommand{\algorithmcfname}{算法}
\SetKwInput{KwIn}{输入}
\SetKwInput{KwOut}{输出}
```

.

