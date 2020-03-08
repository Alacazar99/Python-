## nginx 介绍

###  1 什么是nginx
Nginx是一款高性能的http 服务器/反向代理服务器及电子邮件（IMAP/POP3）代理服务器。

由俄罗斯的程序设计师Igor Sysoev所开发，官方测试nginx能够支支撑5万并发链接，

并且cpu、内存等资源消耗却非常低，运行非常稳定。

 

### 2 应用场景
- 1、http服务器。Nginx是一个http服务可以独立提供http服务。可以做网页静态服务器。

- 2、虚拟主机。可以实现在一台服务器虚拟出多个网站。例如个人网站使用的虚拟主机。

- 3、反向代理，负载均衡。当网站的访问量达到一定程度后，单台服务器不能满足用户的请求时，需要用多台服务器集群可以使用nginx做反向代理。并且多台服务器可以平均分担负载，不会因为某台服务器负载高宕机而某台服务器闲置的情况。

 ##  安装 Nginx
 首先以root 用户 登录 CentOS 主机，按照下面的步骤安装Nginx

```
先执行命令 yum install gcc 确保gcc编译器安装好

先 安装Nginx依赖包 ，执行命令 yum -y install pcre-devel openssl openssl-devel

下载、编译、安装 Nginx

执行命令 wget http://nginx.org/download/nginx-1.15.5.tar.gz 下载Nginx代码包；

执行命令 tar zxvf nginx-1.15.5.tar.gz 解压 代码包

执行命令 cd nginx-1.15.5 进入到代码目录

执行命令 ./configure --prefix=/usr/local/nginx --with-http_ssl_module 配置编译安装选项

执行命令 make && make install 编译安装

```
## 配置Nginx

安装上面的安装方式，Nginx的配置文件路径是：/usr/local/nginx/conf/nginx.conf

> 建议大家使用 winscp 连接 Linux主机并且，配置用notepad++远程打开。因为这样看起来更清楚，特别是配置文件中如果有中文，vi看起来可能会比较乱。

打开 Nginx 配置文件 /usr/local/nginx/conf/nginx.conf ，修改其中的配置项，以满足你的网站需求。

下面是一个Nginx配置示例，列出了其中核心的配置
```
user  alacazar;          # 用alacazar用户运行Nginx进程
worker_processes  2;     # 启动两个Nginx worker 进程

events {
    # 每个工作进程 可以同时接收 1024 个连接
    worker_connections  1024; 
}

# 配置 Nginx worker 进程 最大允许 2000个网络连接
worker_rlimit_nofile 2000;

http {
    include       mime.types;
    default_type  application/octet-stream;

    sendfile        on;

    keepalive_timeout  30;

    gzip  on;
    
    # 配置 动态服务器（比如Gunicorn/Django）
    # 主要配置 名称（这里是apiserver） 地址和端口    
    upstream apiserver  {

        # maintain a maximum of 20 idle connections to each upstream server
        keepalive 20;

        server 127.0.0.1:8000; # 地址和端口
    }
   
    # 配置 HTTP 服务器信息
    server {
        # 配置网站的域名
        server_name  www.alacazar.com;  

        # 配置访问静态文件的根目录，        
        root /home/alacazar/alacazar_frontend;
        
        # 配置动态数据请求怎么处理
        # 下面这个配置项说明了，当 HTTP 请求 URL以 /api/ 开头，
        # 则转发给 apiserver 服务器进程去处理  
        
        location /api/      {
            proxy_pass         http://apiserver;
            proxy_set_header   Host $host;
        }
    }

}

```

## 启动 Nginx

启动Nginx，必须以root用户执行。

```
执行命令 /usr/local/nginx/sbin/nginx ，即可启动Nginx服务。
```

如果启动报错，你需要查看日志文件，可以打开 /usr/local/nginx/logs/error.log 查看错误日志文件。

```
如果你修改了配置文件，需要重启Nginx，可以执行如下命令

/usr/local/nginx/sbin/nginx -s reload


如果需要关闭Nginx服务，可以执行如下命令

/usr/local/nginx/sbin/nginx -s stop
```





