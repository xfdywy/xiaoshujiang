--
title:  Effective Python 59 specific ways 读书笔记 第一章 
date: 2018-03-27
tags:
    -  python
    -  effective

categories: python
idx: 2

--  

今天开始学习这本书，准备用自己的博客做点笔记。
我自己计划着，笔记的内容会会随着自己的理解而变化，在想到好的组织方式之前，我选择“抄书”吧。预计一章一篇博客。总共8章。
今天开始第一章

# 第1条： 确认自己用的python版本
这个不用多说了，py2和py3 还是有一定 的兼容性问题的，但是大部分都不成问题，跑代码前一定要先确认好自己的python版本。

``` python
python --version
```
这个是系统命令版本

``` python
import sys
sys.version_info
sys.version
```
# 第2条： 遵循PEP8 风格指南
PEP8 全称 Python Enhancement Proposal #8.下面是比较重要的几点：
## 空白
-  用space 而不是 tab
-  每一层缩进都用4个space
-  每行字符不超过79个
-  函数与类之间应该用两个空行隔开
-  同一个类不同方法用一个空行隔开
-  下标不要添加空格，同理还有给参数赋值
-  变量赋值的时候左右各写一个空格

## 命名
- 函数，变量和属性应该用小写，并且各个单词之间用下划线连接
- 类与异常，单词首字母大写
- 受保护的实例属性，应该以下划线开头

## 表达式和语句
- `if a is not b` 而不是 `if not a is b`
- 不要用检测长度的方法来判断是否为空
- 不要编写单行的 `if， for，while`
- import 总是放在开头
- import语句要按照 标准库模块，第三方模块，自用模块来分成三块，并且按照字母序排列

# 第3条：了解bytes，str和unicode的区别。

Unicode 是「字符集」
UTF-8 是「编码规则」gbk等也是

python3有两种表示字符序列的类型：bytes和str
python2有三种表示字符序列的类型： str和unicode

python3中的str相当于py2的unicode
python3中的str只能encode
python3中str可以被encode成bytes，例如gbk utf-8等

python2中unicode是一种最基本的数据类型。需要加u在前面表示。`u 'abc'`. unicode可以被encode成str（如gbk，utf-8等）
python2中str是指utf8 gbk这样的编码过的对象，可以被decode成unicode。默认字符串是str.它本身存储的就是字节码（bytes）。


# 第4条： 用辅助函数来取代复杂表达式
不要过度运用python的语法特性，写那些特别复杂且难以理解的表达式，特别是如果要反复利用的话，更要包装一下成函数。

# 第5条： 了解切割序列的办法
起始元素包含，结束元素不包含
``` python
a[:4]
a[-4:]
a[3:-3]
```
slice列表时，start越界也不会出问题，但是访问单个元素的时候会报错
slice列表是一份拷贝，不是引用

# 第6条： 单次切片操作内，不要同时使用start， end， stride
python提供了`list[start:end:stride]`的操作
stride 为负数表示反过来取
``` python
x[::-1]
```


