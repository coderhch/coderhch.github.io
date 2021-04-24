---
title: Linux之history命令
tags: 
    - linux
    - 运维
    - 命令行
    - shell
cover: https://coderhch.oss-cn-shanghai.aliyuncs.com/blog/2021-04-19/Linux%E4%B9%8Bhistory%E5%91%BD%E4%BB%A4/1.jpg
date: 2021-04-19
---
#	Linux之history命令

history的英文意思是历史，所以history命令用于列出所有执行过的命令行

```shell
[root@iZm5e9aiazlx2ktkg01676Z ~]# history 
```

> ​	1  ifconfig
> ​    2  yum -y install gcc gcc-c++ autocont pcre pcre-devel make automake
> ​    3  ping www.baidu.com
> ​    4  yum list | grep gcc
> ​    5  iptables -L
> ​    6  iptables -F
> ​    7  iptables -t nat -F
> ​    8  getenforce 
>
> ......

可以用!编号这样的格式来重新运行history输出中对应编号的命令

```shell
[root@iZm5e9aiazlx2ktkg01676Z ~]# !41
```

