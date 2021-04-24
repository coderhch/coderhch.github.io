#	nginx之sub_module模块

该`ngx_http_sub_module`模块是一个过滤器，可通过将一个指定的字符串替换为另一个指定的字符串来修改响应。



```
location / {
    root   /opt/app/code;
    sub_filter '<span>dylan' '<span>Dylan'
}

```

