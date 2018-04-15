---
title: 折腾linux服务器 
date: 2018-4-15  
tags:
    -   linux
    -   web
    -   nginx
categories:  linux
---
学校里有一台服务器，最近又起了折腾之心。于是就修修补补，在服务器上装上了docker，nginx，架了一个网盘服务nextcloud。下面记录一下遇到的坑，还有解决办法。
 
 注明一下，一下所有操作都是在centos6.9 ，内核版本2.6.32-696.3.2.el6.x86_64 上做的。
 查看内核版本和 发行版本号的命令：
 ```
 cat /etc/issue (此命令可用于docker内系统版本号查询)
 uname -a
 lsb_release -a
 ```
# yum 换阿里云的源
这一步不是必须的，但是换上之后速度太爽了
1. 备份 
```
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
```
2. 下载新的CentOS-Base.repo 到/etc/yum.repos.d/

``` stylus
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo
```

3. 将不需要的repo关掉（这一步不是必须的）

``` stylus
vim xxx.repo
```
改成 enabled=0



4. 更新

``` 
yum clean all
yum makecache
```


# docker
docker 官网上已经只支持centos7 内核版本号3.10  以上。所以我只能安装非官方版了
## 安装
用以下命令：
```
yum install docker-io
service docker start
```
事实证明也是能用的。就是有的时候需要高版本的docker 就瞎了。。。不过还好，这种情况也不是经常遇到
查看log 的话
```
vim /var/log/docker
```
## 使用
1. 下载一个image 命令为：
```
docker pull ubuntu
```
2. 从一个image启动一个container 命令为：
``` stylus
docker run -v localdir:containerport -p localport:containerport -it  ubuntu:wy
 ```
3. 查看所有container：
```
docker ps -a
```

4. 启动一个关闭了的container：
```
docker start id
```
5. 交互连接一个启动了的contaner
```
docker attach id
```
6. 后台运行一个attach中的container 按ctrl p q

7. 查看所有 image
```
docker images
```
8. 关闭一个container
```
docker stop id
```
9. 删除container
```
docker rm id
或
docker rm $(docker ps -a -q)
删除所有container
```

10. 删除 image
```
docker rmi image_id
```
## 遇到的坑
docker in docker 坑太大，放弃




# nginx
这个是个非常给力的反向代理和web服务器。这里既然说是和，就是说他有两个功能，这里重点放在前者，反向代理。
web服务器就有点类似apache，大概是个同层次的概念吧。
反向代理意思就是，部署在服务器端，nginx 作为服务器上的代理人，当用户请求的时候，先经过nginx，再由nginx跟真正的服务器上的资源交流。

先说说为什么要搞nginx，因为服务器对外网就开放了一个端口，比如是80吧，那么如果我要有很多服务，比如我架了个blog在81端口，又架了个网盘在82 端口，又架了个别的什么在83端口，就很麻烦了，因为只有一个端口可以外网访问。有了nginx，我们都先请求到nginx，例如都请求到 服务器ip:80 , 然后再由nginx来判断应该把这个请求发送到那个真正的端口上。判断的标准就是用户使用什么url来访问，例如blog.test.com 就解析到81端口，pan.test.com就解析到82端口。由于80端口是开放的，所以我们设置dns服务器，让这三个url都解析到服务器ip:80 之后的工作就可以交给nginx了。

## 安装
nginx的安装也很简单

``` 
vim /etc/yum.repos.d/nginx.repo
```
添加以下内容
```
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/$releasever/$basearch/
gpgcheck=0
enabled=1
```
之后
```
yum install nginx -y
```
启动服务

``` stylus
service nginx start
```
查看状态

``` stylus
service nginx status
```
一些文件地址：

``` stylus
#Nginx服务器的配置文件
/etc/nginx/nginx.conf 

#Nginx虚拟机文件夹，定义的虚拟机放在此目录下
/etc/nginx/conf.d 
 
/etc/nginx/conf.d/default.conf

# Nginx log
/var/log/nginx

```
## 配置
下面是我自己的配置，通过这个配置，可以实现， 用户 用aaa.com 访问的时候，实际上访问的是 http://xx.xx.xx.xx:60001  ，用bbb.com访问的时候，实际访问的是 http://xx.xx.xx.xx:10080 
只需要在dns解析的时候设置 aaa.com 和 bbb.com 都解析到 你的服务器ip:80 就ok了。


``` bash

server {
    listen       80 default_server;
    listen       [::]:80  default_server;
    server_name  aaa.com;

    root         /var/www/html/;

    include /etc/nginx/default.d/*.conf;

        location / {
            proxy_pass http://xx.xx.xx.xx:60001;
            proxy_redirect default;
            }

error_page 404 /404.html;
    location = /40x.html {
        }

error_page 500 502 503 504 /50x.html;
    location = /50x.html {
        }
}

server {

    listen 8080 ;
    server_name bbb.com;
    location / {
    proxy_pass http://xx.xx.xx.xx:10080;
    }
}

```


## 遇到的坑
如果出现
```
nginx:connect() to 127.0.0.1:5601 failed (13: Permission denied) while connecting to upstream
```
请查看
```
# getenforce
Enforcing
```
如果是上面这个结果,一般都是selinux权限的问题。selinux 的坑比较多。一般如果配置都配置好了，还算是出现错误的话，可以往附近考虑。一般都是访问权限的问题。可以有两种解决办法，一种是直接把selinux 给关了。一种是把文件的权限设置一下。参selinux考
> http://cn.linux.vbird.org/linux_basic/0440processcontrol_5.php


第一种做法

``` stylus
setenforce 0
sed -i 's/enforcing$/disabled/g' /etc/selinux/config
```
第二种做法

``` stylus
#chcon -R -t httpd_sys_content_t /your/file/paht
 
```








