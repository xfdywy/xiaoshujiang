---
title:制作并上传pip 包
tags: python
grammar_cjkRuby: true
---


制作并上传pip package

## 1 注册账号

去下面这个网址注册一个账号
https://pypi.org/

## 安装依赖的包

``` bash
pip install twine  virtualenv setuptools
```


## 制作准备需要上传的包

这里我们准备一个包，这个包的功能是可以通过命令行命令调用跟你说hello。 

第一步，我们创建一个虚拟环境并激活它。

先创建一个文件夹，hello_wy， 这个文件夹叫什么名都可以，我们以后所有的工作都在这个文件夹里面来操作，

进入这个文件夹

``` bash
cd hello_wy
```

创建一个虚拟环境，一个项目用一个虚拟环境是一个好习惯，防止不同项目的依赖互相冲突

``` bash
virtualenv venv_hwy
```


激活虚拟环境（windows下）

``` bash
venv_hwy\Scripts\activate.bat
```


现在新建一个文件夹  hwy， 我们包里面的所有程序文件都放到这个文件夹里面去


在hwy文件夹里面创建两个文件  空的 \_\_init\_\_.py  和 main.py， 其中hellowy.py 写入如下内容：

``` python
import sys
def balaba():
    if len(sys.argv) > 2:
        name = sys.argv
    elif len(sys.argv)==2:
        name = sys.argv[1]
    elif len(sys.argv)==1:
        name = 'wy'


    print("hello {}!".format(name))

```

在hwy的外面，也就是在hello_wy文件夹下面，创建两个文件，一个是readme.md， 一个是setup.py


``` python
from setuptools import find_packages, setup

with open('README.md') as f:
    long_description = f.read()

setup(
    name='hwy',
    version="0.0.1",
    description='print hello wy',
    long_description=long_description,
    long_description_content_type='text/markdown',
    author='wy',
    url='',
    author_email='',
    license='MIT', 
    packages=find_packages(),
    scripts = ['hwy/hellowy.py'],
    entry_points={
        'console_scripts': 'hwy = hwy.hellowy:balaba'
    },
    classifiers=[
        "Programming Language :: Python :: 3.5",
        "Programming Language :: Python :: 3.6",
        "Programming Language :: Python :: 3.7",
        "License :: OSI Approved :: MIT License"
    ]
)

```


现在目录应该是这样的

 - hello_wy
     - hwy
         - \_\_init__.py
         - hellowy.py
     - setup.py
     - readme.md

 

之后在hello_wy 目录下用命令生成包

python setup.py sdist

之后可以看到在hello_wy 下面会生成一个dist文件夹，接下来就可以上传啦

### 上传

twine upload dist \*

输入第一步注册的用户名和密码就ok啦。
如果多次上传，如更新的版本，需要在setup.py 里面修改版本号，并且重新用命令生成包，记得把之前生成的包删掉

### 下载使用
可以试试pip install hwy， 安装刚刚传上去的包。安装好之后在命令行下敲hwy试试。 hwy后面可以跟自己的名字哦 

``` bash
hwy
hwy bob
```