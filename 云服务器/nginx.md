# Nginx

centos7.9直接安装使用nginx，也可以在docker中安全使用，docker中使用详情参考docker篇

## 安装nginx

```shell
 yum -y install nginx
```

![image-20240429103542745](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/202404291035843.png)

## 启动Nginx

```shell
systemctl start nginx # 启动服务
systemctl enable nginx # 设置开机自启
systemctl status nginx # 查看启动状态
```

![image-20240429111039515](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/202404291110538.png)

## 配置Nginx

备份默认配置文件

```shell
cp /etc/nginx/nginx.conf /etc/nginx/nginx.conf.bak
```

修改配置文件

```shell
vim /etc/nginx/nginx.conf
```

重启nginx

```shell
systemctl restart nginx
```

测试nginx连接

```shell
nginx -t
```

![image-20240429113023494](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/202404291130515.png)

## 注意事项
在腾讯云的centos中，可能默认安装了nginx，使用`find / -name nginx.conf`命令检查是否已存在nginx的配置文件，如果存在，则无需再安装nginx，对应的修改配置文件也需要再查找出来的nginx中进行配置。

nginx.conf文件可参考

```shell
# For more information on configuration, see:
#   * Official English Documentation: http://nginx.org/en/docs/
#   * Official Russian Documentation: http://nginx.org/ru/docs/

user nginx;
worker_processes auto;
error_log /var/log/nginx/error.log;
pid /run/nginx.pid;

# Load dynamic modules. See /usr/share/doc/nginx/README.dynamic.
include /usr/share/nginx/modules/*.conf;

events {
    worker_connections 1024;
}

http {
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile            on;
    tcp_nopush          on;
    tcp_nodelay         on;
    keepalive_timeout   65;
    types_hash_max_size 4096;

    include             /etc/nginx/mime.types;
    default_type        application/octet-stream;

    # Load modular configuration files from the /etc/nginx/conf.d directory.
    # See http://nginx.org/en/docs/ngx_core_module.html#include
    # for more information.
    include /etc/nginx/conf.d/*.conf;

    server {
        listen       8888;
        listen       [::]:8888;
        server_name  _;
        # root         /var/www/blog;
        # index index.html;

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        location / {
                 root /var/www/blog;
                 index index.html;
                 try_files $uri $uri/ @router;
        }

        location @router {
          rewrite ^ / permanent;
        }
        error_page 404 /404.html;
        location = /404.html {
        }

        error_page 500 502 503 504 /50x.html;
        location = /50x.html {
        }
    }

# Settings for a TLS enabled server.
#
#    server {
#        listen       443 ssl http2;
#        listen       [::]:443 ssl http2;
#        server_name  _;
#        root         /usr/share/nginx/html;
#
#        ssl_certificate "/etc/pki/nginx/server.crt";
#        ssl_certificate_key "/etc/pki/nginx/private/server.key";
#        ssl_session_cache shared:SSL:1m;
#        ssl_session_timeout  10m;
#        ssl_ciphers HIGH:!aNULL:!MD5;
#        ssl_prefer_server_ciphers on;
#
#        # Load configuration files for the default server block.
#        include /etc/nginx/default.d/*.conf;
#
#        error_page 404 /404.html;
#            location = /40x.html {
#        }
#
#        error_page 500 502 503 504 /50x.html;
#            location = /50x.html {
#        }
#    }

}


```

