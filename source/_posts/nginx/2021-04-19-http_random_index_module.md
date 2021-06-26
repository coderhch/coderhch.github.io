---
title: http_random_index_module模块
tags: 
    - nginx
    - 运维
cover: https://coderhch.oss-cn-shanghai.aliyuncs.com/blog/2021-04-19/nginx%E6%A8%A1%E5%9D%97%E4%B9%8Bhttp_random_index_module/1.jpg
date: 2021-04-19
categories: nginx
---
# http_random_index_module模块

该`ngx_http_random_index_module`模块处理以斜杠字符（' `/`'）结尾的请求，并在目录中选择一个随机文件作为索引文件

##	配置示例

1. 装备好3和html文件

1.html=>红色，2.html=>绿色，3.html=蓝色

2. 编辑default.conf文件`vim /etc/nginx/conf.d/default.conf `

> location / {
>         root   /opt/app/code/;
>         random_index on;
>     }

3. 检查语法是否正确`nginx -tc /etc/nginx/nginx.conf`

> nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
> nginx: configuration file /etc/nginx/nginx.conf test is successful

4. 启动nginx服务`nginx -c /etc/nginx/nginx.conf`
5. 访问`http://ip.com`时就从配置的页面中随机挑选一个页面显示

## 指令

> Syntax:	random_index on | off;
> Default: random_index off;
> Context:	location