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
   vim /etc/yum.repo.d/nginx.repo
   
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
   yum install -y nginx
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

## nginx配置和配置说明

## http协议简单介绍

## Nginx多端口部署多站点

## Nginx多ip部署多站点

## Nginx多域名部署多站点

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

