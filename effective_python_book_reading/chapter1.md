---
title: "Effective Python 59 specific ways 读书笔记 第一章" 
date: 2018-03-27
idx: 2
tags:
    -  python
    -  effective
categories: python
---

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

# 第7条：用列表推导来取代map和filter

```python
a = [1,2,3,4]
squares = [x**2 for x in a]
```
上例就展示了将list里面每个元素都取平方的方法
如果用map来做，需要配合lambda函数，
就变成了

``` python
squares = map(lambda x : x**2 ,a)
```
 
如果需要在循环前加入判断，列表推导需要这么写

``` python
even_squares = [x**2 for x in a if x%2 ==0]
```
map语句的话，需要配合filter函数

``` python
even_squares = map(lambda x:x**2 ,filter(lambda x:x%2 ==0 ,a))
```
**字典与集合也支持推导表达式**

# 第8条：不要使用含有两个以上表达式的列表推导式

# 第9条：用生成器表达式来改写数据量较大的列表推导

列表推导会立即生成一个列表，如果数据量太大，就会导致大量内存消耗。如果返回的是一个迭代器，就非常高效，只需要将方括号改成圆括号就可以。

``` python
iter_squares = (x**2 for x in a)
```

# 第10条： 用enumerate取代range

enumerate的返回值是（下标，元素值）
通常我们在迭代list 的时候需要直接迭代元素值就好，但是有的时候又会需要当前元素在list中的索引。这个时候如果用 `range(len(l))` 就不便于理解，这个时候就需要用enumerate。


# 第11条： 用zip函数同时遍历两个迭代器

``` python
for name, count in zip(names,letters):
    ....
```
**要小心的问题是，如果提供的两个迭代器长度不等，zip函数会提前终止**

# 第12条： 不要在for和while循环后面写else块

for循环后面的else块的意思是：如果for循环提前结束，就不执行else。如果for循环比那里的序列是空的，就会立刻执行else，同理还有while false。


这与 if/else try/except/else 的时候意义相反，这些时候，else都是在前面的条件不满足的时候才执行。

**注意这样的写法不直观，不要写**

# 第13条： 合理利用try/except/else/finally 结构中的每个代码块

try/finally 适用于将异常向上传播同时执行清理工作

try/except/else 可以用else来缩减try中的代码量，因为如果try中的代码发生异常了，就会执行except中的代码，如果没有，就会继续执行else中的。
