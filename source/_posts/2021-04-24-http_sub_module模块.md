---
title: http_sub_module模块
tags: 
    - nginx
    - 运维
cover: https://coderhch.oss-cn-shanghai.aliyuncs.com/blog/2021-04-24/nginx%E4%B9%8Bsub_module%E6%A8%A1%E5%9D%97/3.jpg
date: 2021-04-24
categories: nginx
---
#	http_sub_module模块

该`ngx_http_sub_module`模块是一个过滤器，可通过将一个指定的字符串替换为另一个指定的字符串来修改响应。

## 配置示例

1. 准备好文件放在`/opt/add/code/`目录下

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
  </style>
</head>

<body>
  <span>dylan</span>
  <span>live</span>
  <span>shanghai</span>
  <span>dylan</span>
</body>

</html>
```

2. 编辑`/etc/nginx/conf.d/default.conf 	`文件

> `vim /etc/nginx/conf.d/default.conf`

```
location / {
    root   /opt/app/code;
    sub_filter '<span>dylan' '<span>Dylan';
}
```

3. 检查语法是否正确

> `nginx -tc /etc/nginx/nginx.conf`

4. 启动nginx服务

> `nginx -c /etc/nginx/nginx.conf`

5. 访问`http://ip.com`

<img src="https://coderhch.oss-cn-shanghai.aliyuncs.com/blog/2021-04-24/nginx%E4%B9%8Bsub_module%E6%A8%A1%E5%9D%97/1.jpg" style="zoom:50%;" />

可以看到**dylan**替换成**DYLAN**了，但是最后一个没有变。想全部都替换只需要添加一项配置

6. 修改`/etc/nginx/conf.d/default.conf 	`配置文件

> `vim /etc/nginx/conf.d/default.conf 	` 

```
location / {
    root   /opt/app/code;
    sub_filter '<span>dylan' '<span>DYLAN';
    sub_filter_once off;
}
```

7. 重启服务

> nginx -s stop
> nginx -c /etc/nginx/nginx.conf

8. 访问`http://ip.com`

<img src="https://coderhch.oss-cn-shanghai.aliyuncs.com/blog/2021-04-24/nginx%E4%B9%8Bsub_module%E6%A8%A1%E5%9D%97/2.jpg" style="zoom:50%;" />

现在可以看到已经全局修改了

## 指令

> Syntax:	sub_filter string replacement;
> Default:	—
> Context:	http, server, location

> Syntax:	sub_filter_once on | off;
> Default:	sub_filter_once on;
> Context:	http, server, location