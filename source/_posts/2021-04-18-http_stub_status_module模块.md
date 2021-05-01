---
title: http_stub_status_module模块
tags: 
    - nginx
    - 运维
cover: https://coderhch.oss-cn-shanghai.aliyuncs.com/blog/2021-04-18/nginx模块之http_stub_status_module/1.jpg?versionId=CAEQHhiBgIDFusCUxxciIDE3N2ZlNDA0NTk0YjRjZTJiNmUyYWU0NmNkOTk3MWY0
date: 2021-04-18
categories: nginx
---
#	http_stub_status_module模块

该**ngx_http_stub_status_module**模块提供对基本状态信息的访问

##	配置

1. 编辑default.conf文件

```shell
location = /mystatus {
    stub_status;
}
```

2. 检查nginx配置是否正确

```shell
nginx -tc /etc/nginx/nginx.conf  
```

> nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
> nginx: configuration file /etc/nginx/nginx.conf test is successful

配置成功

3. 启动nginx

```shell
nginx -c /etc/nginx/nginx.conf
```

4.访问``http://ip地址/mystatus``

>
> Active connections: 291 
> server accepts handled requests
>  16630948 16630948 31070465 
> Reading: 6 Writing: 179 Waiting: 106 
> 

##	参数说明

1. **Active connections**

当前活动的客户端连接数，包括`Waiting`连接数

2. **accepts**

接受的客户端连接总数

3. **handled**

已处理的连接总数。通常，参数值与`accepts` 相同

4. **requests**

客户请求总数

5. **Reading**

nginx正在读取请求标头的当前连接数

6. **Writing**

nginx正在将响应写回到客户端的当前连接数

7. **Waiting**

当前等待请求的空闲客户端连接数