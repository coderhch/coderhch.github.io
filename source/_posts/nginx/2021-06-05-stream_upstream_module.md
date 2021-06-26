---
title: stream_upstream_module
tags:
  - nginx
  - 运维
cover: https://coderhch.oss-cn-shanghai.aliyuncs.com/blog/2021-06-05/stream_upstream_module/62322952_p0_master1200.jpg
date: 2021-06-05
categories: nginx
---

# ngx_stream_upstream_module 模块

负载均衡模块

## upstream

定义一组反向代理服务器，服务器可以侦听不同的端口

1. 指令

> Syntax: upstream name { ... }
> Default: —
> Context: stream

2. 示例

```
upstream backend {
    server backend1.example.com:12345;
    server 127.0.0.1:12345;
    server unix:/tmp/backend2;
    server backend3.example.com:12345;
    server backup1.example.com:12345;
}
```

## server

定义 服务器的`*address*`和其他`*parameters*`

1. 指令

> Syntax: server address [parameters];
> Default: —
> Context: upstream

2. 示例

```
upstream backend {
    hash $remote_addr consistent;

    server backend1.example.com:12345  weight=5;
    server backend2.example.com:12345;
    server unix:/tmp/backend3;

    server backup1.example.com:12345   backup;
    server backup2.example.com:12345   backup;
}

server {
    listen 12346;
    proxy_pass backend;
}
```

## weight

设置服务器权重，默认为 1。权重越大访问的机率越大

1. 指令

   `weight=number`

2. 示例

```
upstream backend {
    server backend1.example.com:12345 weight=5;
    server 127.0.0.1:12345  weight=1;
    server unix:/tmp/backend2  weight=10;
}
```

## max_conns

限制指定数量到代理服务器的最大同时连接数。默认值为零，表示没有限制

1. 指令

   `max_conns=number`

2. 示例

```
upstream backend {
    server backend1.example.com:12345 max_conns=2;
    server 127.0.0.1:12345  max_conns=2;
    server unix:/tmp/backend2  max_conns=2;
}
```

## max_fails 与 fail_timeout

**max_fails**指定最大失败次数，如果服务器达到了指定失败次数，就认为当台服务器宕机了。

**fail_tomeout**当达到最大失败次数后，服务器宕机的时间，时间到了后会尝试重新发送请求

1. 指令

   `max_fails=number`

   `fail_timeout=time`

2. 示例

```
upstream tomcats {
        server 192.168.1.173:8080 max_fails=2 fail_timeout=15s ;
        server 192.168.1.174:8080 max_fails=2 fail_timeout=15s ;
        server 192.168.1.175:8080 max_fails=2 fail_timeout=15s ;
}
```

## backup

将服务器标记为备份服务器。当主服务器不可用时，将传递与备份服务器的连接

1. 示例

```
upstream tomcats {
        server 192.168.1.173:8080 backup;
        server 192.168.1.174:8080 weight=1;
        server 192.168.1.175:8080 weight=1;
}
```

## down

将服务器标记为永久不可用

1. 示例

```
upstream tomcats {
        server 192.168.1.173:8080 down;
        server 192.168.1.174:8080 weight=1;
        server 192.168.1.175:8080 weight=1;
}
```
