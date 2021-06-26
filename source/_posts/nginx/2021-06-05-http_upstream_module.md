---
title: http_upstream_module
tags:
  - nginx
  - 运维
cover: https://coderhch.oss-cn-shanghai.aliyuncs.com/blog/2021-06-05/http_upstream_module/17375069_p0_master1200.jpg
date: 2021-06-05
categories: nginx
---

# http_upstream_module

## keepalive

该`*connections*`参数设置保留在每个工作进程的缓存中的上游服务器的最大空闲保持连接数。超过此数量时，将关闭最近最少使用的连接

1. 指令

   > Syntax: keepalive connections;
   > Default: —
   > Context: upstream

2. 示例

   ```
   upstream memcached_backend {
       server 127.0.0.1:11211;
       server 10.0.0.2:11211;

       keepalive 32;
   }

   server {
       ...

       location /memcached/ {
           set $memcached_key $uri;
           memcached_pass memcached_backend;
       }

   }
   ```

## ip_hash

指定组应使用负载平衡方法，其中根据客户端 IP 地址在服务器之间分配请求。客户端 IPv4 地址或整个 IPv6 地址的前三个八位字节用作散列键。该方法确保来自同一客户端的请求将始终传递到同一服务器，除非该服务器不可用

1. 指令

   > Syntax: ip_hash;
   > Default: —
   > Context: upstream

2. 示例

   ```
   upstream backend {
       ip_hash;

       server backend1.example.com;
       server backend2.example.com;
       server backend3.example.com down;
       server backend4.example.com;
   }
   ```

## least_conn

指定组应使用负载平衡方法，将请求传递到活动连接数最少的服务器，同时考虑服务器的权重。如果有多个这样的服务器，则使用加权循环平衡方法轮流尝试它们

1. 指令

   > Syntax: least_conn;
   > Default: —
   > Context: upstream

2. 示例

   ```
   upstream tomcats {
      	least_conn;
       server 192.168.1.173:8080;
       server 192.168.1.174:8080;
       server 192.168.1.175:8080;
   }
   ```
