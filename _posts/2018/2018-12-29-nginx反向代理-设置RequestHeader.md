---
layout: post
title: nginx反向代理-设置RequestHeader
category: tools
tags: [nginx]
excerpt: nginx反向代理-设置RequestHeader !
keywords: nginx
---

# 1、问题描述

## 问题
问题描述：IE8无法传递header,需要通过nginx反向代理动态设置header;

## 目标
实际请求：http://10.120.113.72:8083/mdm-customer-bpportal-bff/v2/customers/0101542015613182?appkey=17CFCFE82A824259A81D7D945E8225D7&authkey=302839345e127977.1545287395360

nginx转发：https://api-dev.unifiedcloud.lenovo.com/mdm-customer-bpportal-bff/v2/customers/0101542015613182?appkey=17CFCFE82A824259A81D7D945E8225D7&authkey=302839345e127977.1545287395360



# 2、解决方案
## nginx完整配置如下：

```
server{
        listen  8083;
        server_name  localhost;
        client_max_body_size 10m;

        location / {
        #       root   html;
        #       index  index.html index.htm;
                        proxy_pass   https://api-dev.unifiedcloud.lenovo.com;
                        proxy_set_header   Host   $host;
                        proxy_set_header   X-Real-IP   $remote_addr;
                        proxy_set_header   tenantId   27;
                        proxy_set_header   MSP-AppKey $arg_appkey;
                        proxy_set_header   MSP-AuthKey $arg_authkey;
                        proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;
                        proxy_connect_timeout 1800;
                        proxy_send_timeout 1800;
                        proxy_read_timeout 1800;
        }

        location ~ ^/(WEB-INF)/ {
                        deny all;
        }

        error_page   500 502 503 504  /50x.html;
                        location = /50x.html {
                        root   /var/www/html/;
        }
}
```

## 核心配置点：
```
proxy_set_header   tenantId   27;
proxy_set_header   MSP-AppKey $arg_appkey;
proxy_set_header   MSP-AuthKey $arg_authkey;
```

