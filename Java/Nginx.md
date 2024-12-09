[toc]

# Nginx

Nginx (engine x)是一个高性能的 HTTP和反向代理 web 服务器，同时也提供了IMAP/POP3/SMTP服务。

同 Tomcat —样， Nginx 可以托管用户编写的 WEB 应用程序成为可访问的网页服务，同时也可以作为流量代理服务器，控制流量的中转。

Nginx在WEB开发领域、基本上也是必备组件之一了。

## nginx的安装和启动

安装nginx需要配置额外的yum仓库，才可以使用yum安装（安装nginx需要操作root身份）

1. 安装yum依赖程序

   ```bash
   # root 执行
   yum install -y yum-utils
   # 查看nginx
   nginx -v
   ```

2. 手动添加，nginx的yum仓库==yum 程序使用的仓库配置文件，存放在：` /etc/yum.repos.d` 内。==

   ```bash
   # 在/etc/yum.repos.d文件夹下创建nginx.repo文件
   vim /etc/yum.repos.d/nginx.repo
   
   # 在文件中填入内容，保存退出(nginx官网可以查看)
   [nginx-stable]
   name=nginx stable repo
   baseurl=http://nginx.org/packages/centos/$releasever/$basearch/
   gpgcheck=1
   enabled=1
   gpgkey=https://nginx.org/keys/nginx_signing.key
   module_hotfixes=true
   
   [nginx-mainline]
   name=nginx mainline repo
   baseurl=http://nginx.org/packages/mainline/centos/$releasever/$basearch/
   gpgcheck=1
   enabled=0
   gpgkey=https://nginx.org/keys/nginx_signing.key
   module_hotfixes=true
   ```

3. 通过yum安装最新稳定版nginx

   ```bash
   # 查看nginx可用版本
   yum list available nginx --showduplicates | sort -r
   #安装最新nginx
   yum install -y nginx
   # 安装特定版本的nginx
   yum install -y nginx-1.22.1-1.el7.ngx
   yum install -y nginx-1:1.20.1-1.el8.ngx.x86_64
   ```

4. 启动

   ```bash
   # nginx自动注册了systemctl系统服务
   systemctl start nginx		# 启动
   systemctl stop nginx		# 停止
   systemctl status nginx		# 运行状态
   systemctl enable nginx		# 开机自启
   systemctl disable nginx		# 关闭开机自启
   ```

5. 配置防火墙

   ==nginx默认绑定80端口，需要关闭防火墙或放行80端口==

   ```bash
   # 方式1，关闭防火墙
   systemctl stop firewalld		# 关闭
   systemctl disable firewalld		# 关闭开机自启
    
   # 方式2，放行80端口
   firewall-cmd --add-port=80/tcp --permanent		# 放行tcp规则下的80端口，永久生效
   firewall-cmd --reload							# 重新加载防火墙规则
   ```

6. 启动浏览器访问

   ```
   80端口是访问网站的默认端口，所以后面无需跟随端口号
   显示的指定端口也是可以的比如：
   http://192.168.31.98:80
   http://centos:80
   ```

7. 卸载nginx

   ```bash
   # 查找系统中所有名为 nginx 的文件和目录
   find  /  -name nginx
   # 停止服务
   systemctl stop nginx 或者对于较旧的系统版本 service nginx stop
   # 删除 Nginx 相关文件和目录
   # 删除配置文件
   rm -rf /etc/nginx
   rm -rf /etc/logrotate.d/nginx
   # 删除日志文件
   rm -rf /var/log/nginx
   # 删除缓存文件
   rm -rf /var/cache/nginx
   # 删除可执行文件和库文件
   rm -rf /usr/sbin/nginx
   rm -rf /usr/lib64/nginx
   # 删除静态资源和文档
   rm -rf /usr/share/nginx
   # 删除初始化脚本
   rm -rf /usr/libexec/initscripts/legacy-actions/nginx
   # ...
   rm -rf /etc/nginx
   rm -rf /etc/logrotate.d/nginx
   rm -rf /var/log/nginx
   rm -rf /var/cache/nginx
   rm -rf /usr/sbin/nginx
   rm -rf /usr/lib64/nginx
   rm -rf /usr/share/nginx
   rm -rf /usr/libexec/initscripts/legacy-actions/nginx
   ```

## nginx配置和配置说明

### Nginx 默认配置文件结构

```bash
/etc/nginx/nginx.conf
# 这是 Nginx 的主配置文件，包含了全局设置和 HTTP 或 Stream 块的基本配置。
/etc/nginx/conf.d/
# 这个目录通常用于存放额外的配置文件。每个文件都会被 nginx.conf 包含进来（通过 include conf.d/*.conf; 指令）。您可以在这里添加自定义的服务器块、虚拟主机配置等。
/etc/nginx/fastcgi_params
# 用于 FastCGI 请求的标准参数配置。通常用于 PHP 等脚本语言的处理。
/etc/nginx/mime.types
# 定义了 MIME 类型与文件扩展名的映射关系。Nginx 使用此文件来确定如何处理不同类型的文件。
/etc/nginx/modules
# 这是一个符号链接，指向实际的 Nginx 模块目录（/usr/lib64/nginx/modules）。动态加载模块的配置可以放在这里。
/etc/nginx/scgi_params
# 用于 SCGI 请求的标准参数配置。类似于 fastcgi_params，但用于 SCGI 协议。
/etc/nginx/uwsgi_params
# 用于 uWSGI 请求的标准参数配置。通常用于 Python 应用程序的处理。
```

1. 删除文件中的空行和注释

   ```bash
   grep -Ev '#|^$' nginx.conf.default(修改的文件) > nginx.conf(需要覆盖的文件)
   ```

2. nginx文件的最小配置

   ```bash
   worker_processes  auto;
   events {
       worker_connections  1024;
   }
   http {
       include       /etc/nginx/mime.types;
       default_type  application/octet-stream;
   
       log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                         '$status $body_bytes_sent "$http_referer" '
                         '"$http_user_agent" "$http_x_forwarded_for"';
   
       access_log  /var/log/nginx/access.log  main;
   
       sendfile        on;
       #tcp_nopush     on;
   
       keepalive_timeout  65;
   
       #gzip  on;
   
       include /etc/nginx/conf.d/*.conf;
   }
   ```

3. nginx配置文件

   ```bash
   user  nginx;
   worker_processes  auto;
   
   error_log  /var/log/nginx/error.log notice;
   pid        /var/run/nginx.pid;
   
   
   events {
       worker_connections  1024;
   }
   
   
   http {
       include       /etc/nginx/mime.types;
       default_type  application/octet-stream;
   
       log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                         '$status $body_bytes_sent "$http_referer" '
                         '"$http_user_agent" "$http_x_forwarded_for"';
   
       access_log  /var/log/nginx/access.log  main;
   
       sendfile        on;
       #tcp_nopush     on;
   
       keepalive_timeout  65;
   
       #gzip  on;
   
       include /etc/nginx/conf.d/*.conf;
   }
   ```

   

## http协议简单介绍

## 部署多站点

### Nginx多端口部署多站点

### Nginx多ip部署多站点

### Nginx多域名部署多站点

## Nginx的include配置加载

## Nginx的日志记录

## Nginx开启basic认证

## Nginx的SSL证书配置

## Nginx的return跳转

## Nginx的rewrite跳转和不能上网的原因

## Nginx的gzip压缩

## Nginx开启目录浏览功能

## Nginx的访问控制

## Nginx的location和符号优先级

## Nginx的常用变量

## Nginx根据语言配置不同语言的站点

## Nginx搭建php动态网站

