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
   # 查看当前系统的yum仓库有哪些软件包
   yum repolist
   # 安装yum的扩展包
   yum install epel-release -y
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

4. 压缩包安装

   ```bash
   # 下载依赖
   yum install pcre pcre-devel
   yum install zlib zlib-devel
   # 查看安装
   yum list installed | grep pcre-devel
   # 解压下载的Nginx源代码包：
   tar -zxvf nginx-1.20.2.tar.gz
   编译和安装进入解压后的Nginx目录并进行编译和安装：
   # 切换到 Nginx 解压目录
   cd nginx-1.24.0
   # 编译前的配置和依赖检查
   ./configure
   # 编译安装
   make && make install
   
   # 配置 Nginx 服务文件
   vi /etc/systemd/system/nginx.service
   # 在打开的文件中，添加以下内容：
   [Unit]
   Description=Nginx HTTP Server
   After=network.target
   
   [Service]
   Type=forking
   ExecStart=/usr/local/nginx/sbin/nginx
   ExecReload=/usr/local/nginx/sbin/nginx -s reload
   ExecStop=/usr/local/nginx/sbin/nginx -s stop
   PrivateTmp=true
   
   [Install]
   WantedBy=multi-user.target
   # 执行以下命令重新加载 systemd 配置文件：
   systemctl daemon-reload
   # 执行以下命令启动 Nginx 服务：
   systemctl start nginx
   # 设置开机自启动
   systemctl enable nginx
   # 检查 Nginx 状态
   systemctl status nginx
   
   
   # 卸载
   systemctl stop nginx停止服务
   systemctl disable nginx.service禁止nginx开机自启
   rm -rf /usr/local/nginx删除安装目录
   rm -rf /export/server/nginx-1.20.2删除可执行文件
   rm -rf /etc/nginx删除配置文件
   rm -rf /var/log/nginx删除日志文件
   rm -rf /usr/share/nginx删除静态文件
   rm -f /etc/systemd/system/nginx.service删除系统服务
   systemctl daemon-reload从新加载系统服务
   清理环境变量
   ps aux | grep nginx验证卸载
   ```

5. 启动

   ```bash
   # nginx自动注册了systemctl系统服务
   systemctl start nginx		# 启动
   systemctl stop nginx		# 停止
   systemctl restart nginx		#重启
   systemctl status nginx		# 运行状态
   systemctl enable nginx		# 开机自启
   systemctl disable nginx		# 关闭开机自启
   ps -ef|grep nginx
   ```

6. 配置防火墙

   ==nginx默认绑定80端口，需要关闭防火墙或放行80端口==

   ```bash
   # 方式1，关闭防火墙
   systemctl stop firewalld		# 关闭
   systemctl disable firewalld		# 关闭开机自启
    
   # 方式2，放行80端口
   firewall-cmd --add-port=80/tcp --permanent		# 放行tcp规则下的80端口，永久生效
   firewall-cmd --reload							# 重新加载防火墙规则
   ```

7. 启动浏览器访问

   ```
   # 查看哪些端口在使用
   netstat -lntup
   80端口是访问网站的默认端口，所以后面无需跟随端口号
   显示的指定端口也是可以的比如：
   http://192.168.31.98:80
   http://centos:80
   ```

8. 卸载nginx

   ```bash
   # 查找系统中所有名为 nginx 的文件和目录
   find  /  -name nginx
   # 停止服务
   systemctl stop nginx 或者对于较旧的系统版本 service nginx stop
   # 卸载nginx
   yum remove nginx 对于使用 dnf 的系统 dnf remove nginx
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
   # 清理缓存
   yum clean all
   rm -rf /etc/yum.repos.d/nginx.repo
   ```

您提到的两种安装 Nginx 的方式——通过 YUM 包管理器安装和从源代码编译安装——有显著的区别。以下是它们的主要差异：

### 1. **安装方式**

- **YUM 安装**：
  - **包管理器**：使用 YUM（或 DNF）包管理器从官方仓库或第三方仓库（如 Nginx 官方仓库）安装 Nginx。
  - **命令**：`sudo yum install nginx`
  - **优点**：
    - **简单快捷**：只需一条命令即可完成安装，包管理器会自动处理依赖项。
    - **维护方便**：可以通过包管理器轻松更新、卸载或回滚到之前的版本。
    - **系统集成**：通常会自动配置为系统服务，支持 `systemctl` 管理，并且会创建必要的用户和组。
    - **安全更新**：仓库中的包通常会定期更新，包含安全补丁和修复。
  - **缺点**：
    - **版本限制**：您只能安装仓库中提供的版本，可能不是最新的稳定版或特定版本。
    - **定制性较低**：无法选择编译时的模块或优化选项。

- **源代码编译安装**：
  - **手动编译**：从 Nginx 官方网站下载源代码压缩包（如 `nginx-1.26.2.tar.gz`），解压后手动配置、编译和安装。
  - **命令**：`./configure && make && make install`
  - **优点**：
    - **完全控制**：可以自定义编译选项，选择启用或禁用特定模块，甚至可以静态链接某些库（如 PCRE、Zlib、OpenSSL 等）。
    - **性能优化**：可以根据您的硬件和需求进行优化编译，例如启用特定的 CPU 指令集或调整线程数。
    - **最新版本**：可以安装最新版本的 Nginx，甚至可以从 Git 仓库获取开发版。
  - **缺点**：
    - **复杂度高**：需要手动处理依赖项、配置编译选项，并且容易出错。
    - **维护困难**：后续更新或卸载需要手动操作，无法通过包管理器自动管理。
    - **系统集成差**：默认不会创建系统服务或用户组，需要手动配置。

### 2. **安装路径**

- **YUM 安装**：
  - **默认路径**：Nginx 通常会被安装在 `/usr/sbin/nginx`，配置文件位于 `/etc/nginx/`，日志文件位于 `/var/log/nginx/`，静态文件位于 `/usr/share/nginx/`。
  - **系统服务**：会自动创建 `nginx.service` 文件，支持 `systemctl` 管理。

- **源代码编译安装**：
  - **默认路径**：通常安装在 `/usr/local/nginx`，但可以通过 `--prefix` 选项指定其他安装路径。
  
  - **系统服务**：不会自动创建 `nginx.service` 文件，需要手动配置。
  
    ```
    3. **依赖项处理**
    
    - **YUM 安装**：
      - **自动处理**：包管理器会自动安装所有必要的依赖项（如 PCRE、Zlib、OpenSSL 等），并且会确保这些依赖项是经过测试和兼容的。
    
    - **源代码编译安装**：
      - **手动处理**：您需要手动安装所有依赖项，并确保它们的版本与 Nginx 兼容。如果缺少依赖项，编译过程会失败。
    
    4. **模块支持**
    
    - **YUM 安装**：
      - **预编译模块**：通常会包含常见的模块（如 `http_ssl_module`、`http_gzip_module` 等），但可能不包含一些较新的或实验性的模块。
      - **动态加载模块**：某些版本的 Nginx 支持动态加载模块，但需要额外配置。
    
    - **源代码编译安装**：
      - **自定义模块**：您可以根据需要选择启用或禁用特定模块，甚至可以添加第三方模块。
      - **静态链接**：可以将模块静态链接到 Nginx 可执行文件中，避免运行时加载模块的开销。
    
    5. **更新和维护**
    
    - **YUM 安装**：
      - **自动更新**：可以通过 `yum update nginx` 命令轻松更新到最新版本，包管理器会处理所有依赖项和配置文件的备份。
      - **回滚**：如果更新出现问题，可以使用 `yum history` 回滚到之前的版本。
    
    - **源代码编译安装**：
      - **手动更新**：需要手动下载新版本的源代码，重新编译并安装。更新过程中可能会丢失自定义配置，需要手动备份和恢复。
      - **回滚**：没有自动回滚机制，需要手动恢复旧版本的二进制文件和配置。
    
    6. **安全性**
    
    - **YUM 安装**：
      - **安全更新**：仓库中的包通常会定期更新，包含安全补丁和修复。您可以使用 `yum update` 来应用这些补丁。
      - **签名验证**：包管理器会验证包的数字签名，确保安装的是官方发布的版本。
    
    - **源代码编译安装**：
      - **手动更新**：需要手动检查并应用安全补丁，可能会遗漏重要的安全更新。
      - **无签名验证**：编译后的二进制文件不会经过包管理器的签名验证，安全性依赖于您下载的源代码是否可信。
    
    **总结**
    
    - **YUM 安装**：适合大多数用户，特别是那些希望快速安装、易于维护和自动更新的用户。它提供了良好的系统集成和安全性，但定制性较低。
    
    - **源代码编译安装**：适合需要高度定制化、最新版本或特定模块的用户。虽然提供了更多的灵活性和性能优化，但安装和维护更加复杂。
    ```

## nginx配置和配置说明

### Nginx 默认配置文件结构

1. yum安装目录（etc/nginx）

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

2. 编译安装（/usr/local/nginx/conf）

   ```
   -rw-r--r--. 1 root root 1077 Dec  9 05:57 fastcgi.conf
   -rw-r--r--. 1 root root 1077 Dec  9 05:57 fastcgi.conf.default
   -rw-r--r--. 1 root root 1007 Dec  9 05:57 fastcgi_params
   -rw-r--r--. 1 root root 1007 Dec  9 05:57 fastcgi_params.default
   -rw-r--r--. 1 root root 2837 Dec  9 05:57 koi-utf
   -rw-r--r--. 1 root root 2223 Dec  9 05:57 koi-win
   -rw-r--r--. 1 root root 5349 Dec  9 05:57 mime.types
   -rw-r--r--. 1 root root 5349 Dec  9 05:57 mime.types.default
   -rw-r--r--. 1 root root 2656 Dec  9 05:57 nginx.conf
   -rw-r--r--. 1 root root 2656 Dec  9 05:57 nginx.conf.default
   -rw-r--r--. 1 root root  636 Dec  9 05:57 scgi_params
   -rw-r--r--. 1 root root  636 Dec  9 05:57 scgi_params.default
   -rw-r--r--. 1 root root  664 Dec  9 05:57 uwsgi_params
   -rw-r--r--. 1 root root  664 Dec  9 05:57 uwsgi_params.default
   -rw-r--r--. 1 root root 3610 Dec  9 05:57 win-utf
   ```

   * `.default`都是备份文件
   * `nginx.conf`nginx的主配置文件，每次nginx启动都会加载它

3. 提取`nginx.conf.default`文件中的非空行和非注释到`nginx.conf`

   ```bash
   grep -Ev '#|^$' nginx.conf.default(修改的文件) > nginx.conf(需要覆盖的文件)
   ```

4. nginx文件的最小配置（重启nginx`systemctl restart nginx`）

   ```bash
   worker_processes  1;
   # 启动nginx的worker_process进程数、aout和cpu核数一致，1表示只启动一个worker_process进程，一般与cpu核数一致
   events {
       worker_connections  1024;
       # 能同时处理的请求数，一个worker_process能同时处理1024个请求
   }
   http {
       include       mime.types;
       # nginx能够识别的文件类型，存与mime.types文件下；yungin.conf同级目录下
       default_type  application/octet-stream;
       # 在mime.types里面没有的类型会以application/octet-stream（八进制数据流）的形式导出到浏览器
       charset utf-8;# 设置字符集
       server {
       # 给网站做部署配置、复制多个server就可以部署多个网站只需要listen端口值不一样
           listen       80;
           # nginx的端口
           server_name  localhost;
           # 部署网站域名
           location / { # 站点所在目录，这里表示根目录
               root   html;
               # 这些root后面跟的是相对路径、也可以放网站所在绝对路径;也就是代码存放路径
               index  index.html index.htm;
               # 访问对应nginx服务器首先打开页面
           }
       }
   }
   ```

   * `nginx -t`：查看更改的配置是否有问题：syntax is ok表示没有问题
   * `mv 文件夹/* .`：将下级目录的所有文件，放到现在这个目录

5. 所有配置

   ```bash
   # 设置Nginx的用户，这里设置为nobody，表示Nginx进程将以nobody用户的身份运行
   user  nobody;
   
   # 定义工作进程的数量，通常设置为CPU核心数
   worker_processes  1;
   
   # 指定错误日志的位置和记录级别（可以是debug, info, notice, warn, error, crit）
   #error_log  logs/error.log;
   #error_log  logs/error.log  notice;
   #error_log  logs/error.log  info;
   
   # 指定Nginx主进程的PID存放位置(进程标识)
   #pid        logs/nginx.pid;
   
   # 配置事件模块参数，这里是epoll模型下的最大连接数
   events {
       worker_connections  1024;  # 每个工作进程的最大并发连接数
   }
   
   # 配置HTTP服务器
   http {
       # 包含MIME类型定义文件，用于根据文件扩展名确定内容类型
       include       mime.types;
   
       # 当无法确定内容类型时，默认使用二进制流格式
       default_type  application/octet-stream;
   
       # 日志格式定义，此处被注释掉，可以取消注释并根据需要修改
       log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                         '$status $body_bytes_sent "$http_referer" '
                         '"$http_user_agent" "$http_x_forwarded_for"';
   
       # 访问日志路径及格式，此行被注释，取消注释后将启用访问日志
       access_log  logs/access.log  main;
   
       # 开启高效文件传输模式，sendfile会直接从磁盘读取文件到socket，减少内存拷贝
       sendfile        on;
   
       # 关闭Nagle算法，减少延迟，但可能增加网络包数量（此行被注释）
       tcp_nopush     on;
   
       # 禁用keepalive连接（此行被注释）
       keepalive_timeout  0;
   
       # 设置长连接超时时间，单位为秒
       keepalive_timeout  65;
   
       # 开启Gzip压缩（此行被注释）
       gzip  on;
   
       # 定义一个server块，代表一个虚拟主机
       server {
           # 监听80端口，处理HTTP请求
           listen       80;
   
           # 该虚拟主机的域名，localhost表示本机
           server_name  localhost;
   
           # 设置字符集（此行被注释）
           charset koi8-r;
   
           # 访问日志路径及格式（此行被注释）
           access_log  logs/host.access.log  main;
   
           # 定义location /，即根目录的处理规则
           location / {
               # 设置网站根目录，相对路径相对于Nginx安装目录
               root   html;
   
               # 设置默认索引文件，当访问目录时，Nginx会尝试加载这些文件
               index  index.html index.htm;
           }
   
           # 自定义错误页面，将500, 502, 503, 504错误重定向到/50x.html
           error_page   500 502 503 504  /50x.html;
   
           # 定义/50x.html的处理规则
           location = /50x.html {
               root   html;  # 设置/50x.html文件所在的目录
           }
   
           # 将PHP脚本代理给Apache处理（此段被注释）
           location ~ \.php$ {
               proxy_pass   http://127.0.0.1;
           }
   
           # 将PHP脚本交给FastCGI服务器处理（此段被注释）
           location ~ \.php$ {
               root           html;
               fastcgi_pass   127.0.0.1:9000;
               fastcgi_index  index.php;
               fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
               include        fastcgi_params;
           }
   
           # 禁止访问.htaccess文件，防止泄露Apache配置信息（此段被注释）
           location ~ /\.ht {
               deny  all;
           }
       }
   
       # 定义另一个虚拟主机，可以基于IP、名称或端口进行配置（此段被注释）
       server {
           listen       8000;
           # 只监听名为somename的主机名对应的IP地址上的8080端口
           listen       somename:8080;
           server_name  somename  alias  another.alias;
   
           location / {
               root   html;
               index  index.html index.htm;
           }
       }
   
       # HTTPS服务器配置（此段被注释）
       server {
           listen       443 ssl;  # 监听443端口，并启用SSL/TLS加密
           server_name  localhost;
   
           # SSL证书文件路径
           ssl_certificate      cert.pem;
   
           # SSL私钥文件路径
           ssl_certificate_key  cert.key;
   
           # SSL会话缓存设置
           ssl_session_cache    shared:SSL:1m;
   
           # SSL会话超时时间
           ssl_session_timeout  5m;
   
           # 启用的SSL加密套件，选择高强度加密算法
           ssl_ciphers  HIGH:!aNULL:!MD5;
   
           # 优先使用服务器端的加密套件
           ssl_prefer_server_ciphers  on;
   
           location / {
               root   html;
               index  index.html index.htm;
           }
       }
   }
   ```

## http协议

HTTP（HyperText Transfer Protocol，超文本传输协议）是用于在Web浏览器和Web服务器之间传输网页的协议。它是应用层协议，基于客户端-服务器模型工作。HTTP 是无状态的，这意味着每个请求都是独立的，服务器不会保留之前请求的状态信息。

### HTTP 的基本概念

1. **请求与响应**：
   - **请求**：客户端（通常是浏览器）向服务器发送一个请求，这个请求包含请求行、请求头和请求体。
   - **响应**：服务器处理请求后返回一个响应，这个响应也包含状态行、响应头和响应体。

2. **方法（Methods）**：
   HTTP 定义了多种请求方法，最常见的包括：
   - **GET**：请求指定的资源。通常用于获取数据，不应有副作用。
   - **POST**：向指定资源提交数据，通常用于提交表单或上传文件。
   - **PUT**：上传一个资源到指定位置，通常用于更新现有资源或创建新资源。
   - **DELETE**：请求服务器删除指定的资源。
   - **HEAD**：类似于 GET 请求，但不返回资源主体，只返回头部信息。
   - **OPTIONS**：请求关于目标资源所支持的通信选项。
   - **PATCH**：对资源进行部分修改。

3. **状态码（Status Codes）**：
   服务器在响应中会返回一个状态码，用来表示请求的结果。常见的状态码分类如下：
   - **1xx (信息性响应)**：请求已被接收，继续处理。
   - **2xx (成功)**：请求已成功接收、理解和处理。
     - 200 OK：请求成功。
     - 201 Created：请求成功并且服务器创建了新的资源。
   - **3xx (重定向)**：需要进一步操作以完成请求。
     - 301 Moved Permanently：请求的资源已被永久移动到新位置。
     - 302 Found：请求的资源临时从不同的 URI 响应请求。
   - **4xx (客户端错误)**：请求包含语法错误或无法完成。
     - 400 Bad Request：服务器无法理解请求的格式。
     - 401 Unauthorized：请求要求用户的身份认证。
     - 403 Forbidden：服务器理解请求，但是拒绝执行。
     - 404 Not Found：请求的资源在服务器上未找到。
   - **5xx (服务器错误)**：服务器在处理请求时发生错误。
     - 500 Internal Server Error：服务器遇到意外情况，无法完成请求。
     - 502 Bad Gateway：作为网关或者代理工作的服务器尝试执行请求时，从上游服务器收到无效响应。
     - 503 Service Unavailable：服务器暂时无法处理请求，可能是过载或维护中。

4. **头部（Headers）**：
   请求和响应都包含头部信息，这些信息提供了关于请求或响应的元数据。例如：
   - `Content-Type`：指明实体的媒体类型。
   - `Content-Length`：指明实体主体的大小。
   - `Authorization`：包含访问资源所需的认证信息。
   - `Cache-Control`：控制缓存的行为。
   - `Set-Cookie`：由服务器发送，告诉客户端存储 cookie。

5. **消息体（Body）**：
   请求体通常包含要发送给服务器的数据，如表单数据或上传的文件。响应体则包含服务器返回的内容，如 HTML 页面、JSON 数据等。

6. **无状态性（Statelessness）**：
   HTTP 是无状态的，这意味着每次请求都是独立的，服务器不会记住之前的请求。为了实现会话管理，通常使用 cookie 或者在 URL 中传递会话标识符。

7. **持久连接（Persistent Connections）**：
   HTTP/1.1 引入了持久连接的概念，允许在一个 TCP 连接上发送多个请求和响应，从而减少了建立和关闭连接的开销。

8. **版本（Versioning）**：
   HTTP 协议有不同的版本，最常见的是 HTTP/1.1 和 HTTP/2。HTTP/2 提供了多路复用、头部压缩等特性，提高了性能。

9. **安全性（Security）**：
   HTTPS 是 HTTP 的安全版本，通过 SSL/TLS 加密来保护数据传输的安全性，防止中间人攻击。

### HTTP 请求示例

**GET 请求**

```http
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0
Accept: text/html
```

**POST 请求**

```http
POST /submit_form HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 27

name=John+Doe&email=john@example.com
```

### HTTP 响应示例

**成功响应**

```http
HTTP/1.1 200 OK
Date: Tue, 12 Dec 2023 12:00:00 GMT
Server: Apache/2.4.41 (Ubuntu)
Content-Type: text/html; charset=UTF-8
Content-Length: 612

<html>
<head><title>Example Page</title></head>
<body>
  <h1>Welcome to Example.com!</h1>
  <!-- More HTML content -->
</body>
</html>
```

**错误响应**

```http
HTTP/1.1 404 Not Found
Date: Tue, 12 Dec 2023 12:00:00 GMT
Server: Apache/2.4.41 (Ubuntu)
Content-Type: text/html; charset=UTF-8
Content-Length: 205

<html>
<head><title>404 Not Found</title></head>
<body>
  <h1>Not Found</h1>
  <p>The requested URL was not found on this server.</p>
</body>
</html>
```

HTTP 是 Web 应用程序中最常用的协议之一，它定义了客户端和服务器之间如何交换数据。理解 HTTP 的基本概念、请求和响应结构、常用方法和状态码对于开发和调试 Web 应用程序至关重要。如果你有更多具体的问题或需要深入了解某个方面，请随时告诉我！

## 部署多站点

==一个 nginx上可以运行多个网站==

* `http:// + ip/域名 + 端口 + URL`
* 其中：ip/域名变了，那么网站入口就变了，端口变了，网站入口也变了

### Nginx多端口部署多站点

```bash
worker_processes  1;
events {
    worker_connections  1024;
}
http {
    include       mime.types;
    default_type  application/octet-stream;
    sendfile        on;
    keepalive_timeout  65;
    charset utf-8;# 设置字符集
    # 第一个战点
    server {
        listen       80;
        server_name  localhost;
        location / {
            root   html/zhandian1;
            index  index.html index.htm;
        }
    }
    # 第二个站点
    server {
        listen       81;# 端口
        server_name  localhost;
        location / {
            root   html/zhandian2;
            index  index.html index.htm;
        }
}
```

### Nginx多ip部署多站点

* 修改linux网卡配置信息`vi /etc/sysconfig/network-scripts/ifcfg-ens160`

   ```
   IPADDR1=192.168.31.98
   IPADDR2=192.168.31.98
   IPADDR3=192.168.31.98
   NETMASK=255.255.255.0
   GATEWAY=192.168.31.1
   ```

* 重启网络服务

* 修改nginx.conf文件`listen       ip:80;`，ip与配置的ip地址

   ```
   worker_processes  1;
   events {
       worker_connections  1024;
   }
   http {
       include       mime.types;
       default_type  application/octet-stream;
       sendfile        on;
       keepalive_timeout  65;
       charset utf-8;# 设置字符集
       # 第一个战点
       server {
           listen       ip:80;
           server_name  localhost;
           location / {
               root   html/zhandian1;
               index  index.html index.htm;
           }
       }
       # 第二个站点
       server {
           listen       ip:80;# 端口
           server_name  localhost;
           location / {
               root   html/zhandian2;
               index  index.html index.htm;
           }
   }
   ```

### Nginx多域名部署多站点

* 修改配置文件的`server_name` 域名配置

* 测试：修改windows的host文件，配置ip与域名对应关系，本机优先访问

   ```
   worker_processes  1;
   events {
       worker_connections  1024;
   }
   http {
       include       mime.types;
       default_type  application/octet-stream;
       sendfile        on;
       keepalive_timeout  65;
       charset utf-8;# 设置字符集
       # 第一个战点
       server {
           listen       80;
           server_name  a.a.com;
           location / {
               root   html/zhandian1;
               index  index.html index.htm;
           }
       }
       # 第二个站点
       server {
           listen       80;# 端口
           server_name  b.b.com;
           location / {
               root   html/zhandian2;
               index  index.html index.htm;
           }
   }
   ```

### Nginx的配置文件include配置项

1. **步骤**

   1. 在conf文件夹下新建`conf.d`配置文件夹

   2. 删除nginx.conf文件里面所有server配置项

      ```bash
      server {
         listen       80;# 端口
         server_name  b.b.com;
         location / {
             root   html/zhandian;
             index  index.html index.htm;
             }
      }
      ```

   3. 在nginx.conf文件http大括号下加入include配置`include conf.d/*.conf`

      ```bash
      worker_processes  1;
      events {
          worker_connections  1024;
      }
      http {
          include       mime.types;
          default_type  application/octet-stream;
          charset utf-8;        # 设置字符集
          include conf.d/*.conf # 设置配置文件映射地址
      }
      ```

   4. 将原来的server配置项，每一个单独作为以`.conf`结尾的配置文件，命名方式`站点名.conf`

   5. 在默认站点文件中`listen 80;`配置改为`listen 80 default_server;`表示默认访问站点

      ```bash
      server {
         listen       80 default_server;# 端口
         server_name  b.b.com;
         location / {
             root   html/zhandian;
             index  index.html index.htm;
             }
      }
      ```

2. **注意**

   1. 如果nginx没有配置默认访问网站，那么当当前网站不能访问时，nginx默认访问第一个站点作为默认网站
   2. 所有配置文件的更改都需要重启nginx才能使配置文件生效

## Nginx日志

1. 位置
   * yum安装
      1. `var/log/nginx/`
   * 源码安装（压缩文件）
      1. `usr/local/nginx/logs/`
         * `access.log`：访问日志
         * `error.log`：错误日志
2. 清空日志：`> access.log`

### 访问日志

1. 定制日志格式，在nginx.conf文件中，与server配置平级，在http配置项下面

   ```bash
   # 定制日志记录格式
   log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                     '$status $body_bytes_sent "$http_referer" '
                     '"$http_user_agent" "$http_x_forwarded_for"';
                     
   log_format  格式名字  '客户端地址 - 客户端用户名 当前时间 请求起始行 '
                     '$http状态码 响应资源大小 记录资源的跳转地址 '
                     '"用户的终端信息 gzip的压缩级别';
   192.168.31.71 - - [15/Dec/2024:06:23:48 -0800] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
   main
   # main格式名字，使用这个格式直接使用这个名字
   $remote_addr
   # 含义：客户端的 IP 地址。
   # 说明：这是发起 HTTP 请求的客户端（通常是浏览器或代理服务器）的 IP 地址。如果请求经过了多个代理服务器，这可能是最后一个代理的 IP 地址。
   -
   # 含义：分隔符，通常是一个固定的 - 符号。
   # 说明：这个符号是 Nginx 日志格式中的一个占位符，用于分隔不同的字段。在传统的 Apache 日志格式中，这个位置通常用于记录 RFC 1413 标准的用户身份验证信息（如 identd），但在现代环境中，这个字段通常为空，因此使用 - 作为占位符。
   $remote_user
   # 含义：通过 HTTP 基本认证（Basic Authentication）验证的用户名。
   # 说明：如果启用了 HTTP 基本认证，这里会显示通过认证的用户名。如果没有启用认证或请求未经过认证，这里会显示一个空字符串（即 -）。
   [$time_local]
   # 含义：请求的时间，使用本地时区表示。
   # 说明：这是请求到达 Nginx 服务器的时间，格式为 [day/month/year:hour:minute:second zone]，例如 [15/Dec/2024:22:39:45 +0800]。+0800 表示时区偏移量，这里是东八区（北京时间）。
   "$request"
   # 含义：完整的 HTTP 请求行。
   # 说明：这包括 HTTP 方法、请求的 URI 和 HTTP 版本。例如，"GET /index.html HTTP/1.1"。这可以帮助你了解客户端请求的具体内容。
   $status
   # 含义：HTTP 状态码。
   # 说明：这是 Nginx 返回给客户端的 HTTP 状态码，表示请求的处理结果。常见的状态码包括：
   # 200：请求成功。
   # 301 或 302：重定向。
   # 404：页面未找到。
   # 500：内部服务器错误。
   # 502：网关错误（通常是后端服务器不可用）。
   $body_bytes_sent
   # 含义：发送给客户端的响应体大小（以字节为单位）。
   # 说明：这是 Nginx 发送给客户端的实际响应体大小，不包括 HTTP 头部。如果你需要统计传输的数据量，这个字段非常有用。
   "$http_referer"
   # 含义：HTTP 请求头中的 Referer 字段。
   # 说明：这是客户端从哪个页面链接到当前页面的 URL。例如，如果用户从 https://example.com/page1 点击链接访问 https://example.com/page2，那么 Referer 就是 https://example.com/page1。这个字段可以帮助你分析流量来源。
   "$http_user_agent"
   # 含义：HTTP 请求头中的 User-Agent 字段。
   # 说明：这是客户端使用的浏览器或爬虫的信息。User-Agent 字段通常包含浏览器的名称、版本、操作系统等信息。例如，Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36。这个字段可以帮助你分析用户的浏览器和设备信息。
   "$http_x_forwarded_for"
   # 含义：HTTP 请求头中的 X-Forwarded-For 字段。
   # 说明：当请求经过多个代理服务器时，X-Forwarded-For 头部会包含客户端的真实 IP 地址以及所有中间代理的 IP 地址。格式为 client_ip, proxy1_ip, proxy2_ip, ...。例如，192.168.1.1, 10.0.0.1, 172.16.0.1。这个字段可以帮助你获取客户端的真实 IP 地址，尤其是在使用反向代理（如负载均衡器）的情况下。
   ```

2. 单独为站点配置nginx的访问日志格式，在server配置项里面配置

   ```bash
   access_log  logs/host.access.log  main;
   access_log  存放地址/日志文件每次 日志格式名称
   ```

   1. 存放地址（一般存放与opt目录下）

      ```bash
      makdir nginx # 在opt目录下新建nginx文件夹 
      ```

   2. 给nginx文件夹付权给nginx用户（因为nginx是nginx用户启动的）

      ```
      chown nginx:nginx opt/nginx
      ```

3. favicon.ico

   * 图标：网页前端页面访问的图标

4. 错误日志

   1. 无法更改格式，只能更改存放地址

      ```bash
      error_log 存放地址/日志文件每次 info
      ```

## basic认证

用于在客户端和服务器之间进行用户身份验证。它通过在 HTTP 请求头中传递用户名和密码来实现。尽管基本认证的实现简单，但它并不安全，因为用户名和密码是以 Base64 编码的形式传输的，而不是加密的。因此，建议在使用基本认证时结合 HTTPS 以确保数据的安全性。

### 工作原理

1. **客户端请求**：当客户端（如浏览器）访问一个受保护的资源时，服务器会返回一个 `401 Unauthorized` 状态码，并在响应头中包含 `WWW-Authenticate: Basic realm="some realm"`，告知客户端需要进行基本认证。
2. **客户端响应**：客户端弹出一个用户名和密码输入框，用户输入凭证后，客户端会将这些凭证编码为 Base64 格式，并在后续的 HTTP 请求头中添加 `Authorization: Basic <base64-encoded-credentials>`。
3. **服务器验证**：服务器接收到带有 `Authorization` 头的请求后，解码 Base64 字符串，提取用户名和密码，并验证它们是否正确。如果验证通过，服务器返回请求的资源；否则，返回 `401 Unauthorized`。

### 开启认证

1. 生成htpassword文件，存放到自定义目录下，一般存放与安装目录下conf文件内

   ```bash
   vim htpassword 用户名:密码 # 用户名密码一般由网页生产
   ```

2. 生成htpassword方式

   1. windows网页生产：随便找一个网页生成，复制粘贴

   2. linux软件生成

      1. 安装htpassword工具

         ```bash
         # centos
         yum install httpd-tools
         # ubuntu
         apt-get install apache2-utils
         ```

      2. 使用 `htpasswd` 创建一个密码文件，并添加用户。例如，创建一个名为 `htpasswd` 的文件并添加用户 `admin`：

         ```bash
         sudo htpasswd -c /etc/nginx/.htpasswd admin
         ```

3. 修改nginx.conf配置文件server选项

   ```bash
   auth_basic "" # 开启basic认证,""双引号中为备注信息
   auth_basic_user_file /htpssword存放htpassword文件的地址 # 加载用户名密码文件
   ```

## SSL认证

1. http协议传输为明文传输所以不安全，配置`SSL`证书，成为`htpts`：==https==等于==http==加==ssl==

**申请ssl证书**

1. 流程
   * 进入云服务器申请域名
   * ICP备案
   * 然后申请ssl证书
   * 将ssl证书压缩包下载到本地
2. 将证书上传到nginx的安装目录下ssl文件夹内

**在nginx下配置**

1. 在server配置项里面配置

   ```bash
   server {
       # 监听443端口以处理HTTPS流量
       listen 443 ssl;
   
       # 指定服务器的域名或IP地址
       server_name yourdomain.com;
   
       # 指定SSL证书文件的位置
       ssl_certificate /etc/nginx/ssl/yourdomain.com.crt;
   
       # 指定SSL私钥文件的位置
       ssl_certificate_key /etc/nginx/ssl/yourdomain.com.key;
   
       # 指定支持的TLS版本，这里仅允许TLSv1.2和TLSv1.3，更安全
       ssl_protocols TLSv1.2 TLSv1.3;
   
       # 优先使用服务器配置的加密套件，而不是客户端的偏好
       ssl_prefer_server_ciphers on;
   
       # 设置使用的加密套件，选择更安全的组合
       ssl_ciphers "ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256";
   
       # 设置SSL会话的超时时间，1天
       ssl_session_timeout 1d;
   
       # 设置共享的SSL会话缓存，大小为10MB，可以存储大约40000个会话
       ssl_session_cache shared:MozSSL:10m;
   
       # 禁用SSL会话票据（session tickets），以提高前向安全性
       ssl_session_tickets off;
   
       # 启用HTTP严格传输安全（HSTS），强制浏览器仅通过HTTPS访问，并包括所有子域
       add_header Strict-Transport-Security "max-age=15768000; includeSubDomains" always;
   
       # 启用OCSP装订（OCSP Stapling），让Nginx代替客户端从CA获取最新的OCSP响应
       ssl_stapling on;
   
       # 启用OCSP装订验证，确保OCSP响应是有效的
       ssl_stapling_verify on;
   
       # 指定DNS解析器用于OCSP装订，使用Google的公共DNS服务
       resolver 8.8.8.8 8.8.4.4 valid=300s;
   
       # 设置DNS解析器的超时时间
       resolver_timeout 5s;
   
       # 如果请求协议是HTTP，则重定向到HTTPS
       if ($scheme = http) {
           return 301 https://$host$request_uri;
       }
   
       # 定义处理所有其他请求的location块
       location / {
           # 在这里放置您的应用程序配置，例如代理设置、静态文件服务等
       }
   }
   ```

2. 必要配置

   ```bash
   server {
       # 监听443端口以处理HTTPS流量
       listen 443 ssl;
       # 指定服务器的域名或IP地址
       server_name yourdomain.com;
       # 指定SSL证书文件的位置
       ssl_certificate /etc/nginx/ssl/yourdomain.com.crt;
       # 指定SSL私钥文件的位置
       ssl_certificate_key /etc/nginx/ssl/yourdomain.com.key;
       # 指定支持的TLS版本，这里仅允许TLSv1.2和TLSv1.3，更安全
       ssl_protocols TLSv1.2 TLSv1.3;
       # 优先使用服务器配置的加密套件，而不是客户端的偏好
       ssl_prefer_server_ciphers on;
       # 设置使用的加密套件，选择更安全的组合
       ssl_ciphers "ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256";
       # 定义处理所有其他请求的location块
       location / {
           # 在这里放置您的应用程序配置，例如代理设置、静态文件服务等
       }
   }
   # 重定向
   server{
       listen 80;
       server_name yourdomain.com;
       location / {
           return 302 https://yourdomain.com;$request_uri;
       }
   }
   ```

## Nginx跳转

### return

==如果请求协议是HTTP，则重定向到HTTPS==

1. 配置在server配置项里面的location配置项下面
2. 一个server配置文件中可用配置多个server配置项

```bash
server{
    listen 80
    server_name
    location / {
        return 302 https://yourdomain.com$request_uri;
    }
}
# $request_uri：下级目录访问路径
```

### rewrite

```bash
server{
    listen 80
    server_name yourdomain.com;
    location / {
        rewrite ^/(.*) https://yourdomain.com/$1 redirect;
        # rewrite ^/(.*) https://yourdomain.com/$1 permanent;
    }
}
```

1. `redirect`：代表状态302，零时跳转
2. `permanent`：代表状态301，永久跳转
3. `^`：代表网址
4. `/(.*)`：匹配uri
5. `$1`：表示匹配括号中的内容，也就是`.*`

### 不能上网的原因

==我们配首了静态 ip 的涞个 NAT 樘式餉虚拟不能上网是因为被 NetworkManager 给干忧了，关闭一下它即可==

```bash
# 在 centOS 中有 NetworkManager 和 network 两种管理工具，如果这两个服务都工作时会产生冲突进而导机器无法联网
systemctl stop NetworkManager
systemctl disable NetworkManager
# 重启网卡
systemctl restart network
# 查看网关
route -n
```

## Nginx gzip压缩

1. 压缩：省流量、加快传输速度。服务的流量都是要花钱的。尢具是要做加速的网站，比如 CDN 加速，都是要收取流量费的。

   ```bash
   [root@localhost ~]# ll
   total 8
   -rw-------. 1 root root 2813 Nov 22 11:46 anaconda-ks.cfg
   -rw-------. 1 root root 2131 Nov 22 11:46 original-ks.cfg
   [root@localhost ~]# gzip anaconda-ks.cfg
   [root@localhost ~]# ll
   total 8
   -rw-------. 1 root root 1221 Nov 22 11:46 anaconda-ks.cfg.gz
   -rw-------. 1 root root 2131 Nov 22 11:46 original-ks.cfg
   ```

1. 配置nginx的gzip压缩，`gzip`相关的配置项可以放置在不同的上下文（context）中，具体取决于你希望对哪些请求启用Gzip压缩。

   ```shell
   gzip on;
   gzip_min_length 1k;
   gzip_buffers 4 32k;
   gzip_http_version 1.1;
   gzip_comp_level 9;
   gzip_types text/html text/css text/xml application/javascript;
   gzip_proxied on;
   gzip_vary on;
   gzip_disable "MSIE [1-7]\";
   
   # 启用或禁用 Gzip 压缩。
   # "on" 表示启用压缩，"off" 表示禁用压缩。
   gzip on;
   # 设置允许压缩的页面最小字节数。
   # 只有当响应体大小超过这个值时才会被压缩。设置为 1k (1024 字节)。
   gzip_min_length 1k;
   # 设置系统获取几个单位的缓存用于存储 gzip 的压缩结果数据流。
   # 每个单位为32k，默认情况下会分配4个这样的单位，即总共128k的缓冲区。
   gzip_buffers 4 32k;
   # 设置压缩HTTP响应的最低版本。
   # 这里设置为 "1.1"，意味着只有当客户端支持HTTP/1.1或更高版本时才进行压缩。
   gzip_http_version 1.1;
   # 设置Gzip模块压缩等级。
   # 数值范围从 1 到 9，1 表示最快但压缩率最低，9 表示最慢但压缩率最高。
   gzip_comp_level 9;
   # 设置需要压缩的MIME类型。
   # 默认只压缩文本文件（如HTML、CSS、XML）和JavaScript文件。
   gzip_types text/html text/css text/xml application/javascript;
   # 控制是否在响应头中添加 Vary: Accept-Encoding。
   # 当设置为 "on" 时，Nginx 会在响应头中添加 Vary: Accept-Encoding，
   # 以确保不同客户端（支持或不支持Gzip）获得正确的缓存内容。
   gzip_vary on;
   # 启用或禁用对代理请求的压缩。
   # "on" 表示启用，"off" 表示禁用。这里启用了对代理请求的压缩。
   gzip_proxied on;
   # 禁用指定浏览器的压缩。
   # 在这里，对于Internet Explorer 1到7版本的浏览器，不使用Gzip压缩。
   # 使用正则表达式匹配浏览器标识字符串来决定是否禁用压缩。
   gzip_disable "MSIE [1-7]\.";
   ```

   **注释说明**

   - **`gzip on;`**：此配置项用于开启或关闭Gzip压缩功能。在高流量网站中，启用Gzip可以显著减少传输的数据量，提高页面加载速度，但也会增加服务器的CPU负载。
   - **`gzip_min_length 1k;`**：规定了只有当响应内容长度大于等于1KB时，才会对其进行压缩。较小的文件压缩后可能不会带来明显的好处，反而可能因为压缩和解压的过程而增加了延迟。
   - **`gzip_buffers 4 32k;`**：定义了用于存储压缩结果的缓冲区数量和大小。根据你的服务器性能和预期处理的文件大小调整这些值可以优化压缩效率。
   - **`gzip_http_version 1.1;`**：指定了支持压缩的最低HTTP协议版本。大多数现代浏览器都支持HTTP/1.1及以上版本，因此这是一个合理的默认值。
   - **`gzip_comp_level 9;`**：设定了压缩级别。较高的数值意味着更好的压缩比，但也意味着更高的CPU消耗。通常建议使用5或6作为平衡点，除非你有特别的需求。
   - **`gzip_types ...;`**：列出了所有应该被压缩的内容类型。你可以根据自己的网站需求添加更多的MIME类型，比如JSON、字体文件等。
   - **`gzip_proxied on;`**：确定是否对通过代理服务器传来的请求启用压缩。如果你的网站经常通过代理访问，确保这项设置正确是非常重要的。
   - **`gzip_disable "MSIE [1-7]\.";`**：用于排除特定的老版本浏览器（例如Internet Explorer 1-7），因为这些浏览器可能存在与Gzip压缩相关的兼容性问题。随着旧版IE用户的减少，这条规则在现代环境中变得越来越不重要。
   
   **配置位置**
   
   * `http`：这是最外层的上下文，适用于所有服务器和位置。如果你希望对整个Nginx服务器的所有响应启用Gzip压缩，那么你应该在这里设置。
   
   * `server`：这个上下文适用于特定的虚拟主机。如果你想只为一个特定的域名或IP地址启用Gzip压缩，应该在这个上下文中配置。
   
   * `location`：这个上下文适用于特定的URL路径。如果只希望对某些特定的资源启用Gzip压缩，例如静态文件或者API响应，那么可以在相应的`location`块中进行配置。
   
      ```shell
      http {
          # 在 http 上下文中配置 Gzip
          gzip on;
          gzip_types text/plain application/xml;
      
          server {
              listen 80;
              server_name example.com;
      
              # 在 server 上下文中覆盖 Gzip 设置
              gzip off;
      
              location /static/ {
                  # 在 location 上下文中覆盖 Gzip 设置
                  gzip on;
                  gzip_min_length 1000;
                  gzip_buffers 16 8k;
                  gzip_http_version 1.1;
                  gzip_comp_level 6;
                  gzip_proxied any;
                  gzip_vary on;
                  gzip_types text/css application/javascript;
              }
      
              location /api/ {
                  # 可以为 API 响应单独配置 Gzip
                  gzip on;
                  gzip_types application/json;
              }
          }
      }
      ```

## Nginx目录浏览

### 开启目录浏览功能

1. 在server配置项里面配置

   ```shell
   autoindex on;# 开启目录浏览
   autoindex_exact_size off;# 显示文件大小的时候带单位
   ```

2. 目录下不能有index.html文件

## Nginx访问控制

* 访问控制行为两种，允许（加白）和禁止（加黑）
* 访问控制有两个方式，一种是在 OSI 模型的四层传输层，一种是在第七层应用层。主机防火墙就是在四层控制， nginx 就是在七层控制。
* 访问控制需要开启防火墙
* nginx是基于第七层的访问控制

### 基于OSI四层

1. 防火墙直接禁用IP

2. 开启防火墙

   ```bash
   # 开启
   systemctl start firewalld.service
   # 关闭
   systemctl stop firewalld.service
   ```

3. 拉黑某些ip地址

   ```bash
   firewall-cmd --add-rich-rule='rule family=ipv4 source address="121.123.11.0/24" drop'
   firewall-cmd --add-rich-rule='rule family=ipv4 source address="121.123.11.98" drop'
   ```

4. 查看当前系统远程链接了那些ip地址`# w`

### 基于OSI七层

* 拉黑的，叫做加入黑名单，被禁止访问的

* 加白的，叫做加入自名单，是允许访问的

* allow(允许)

* deny（拒绝）

   1. 在server配置项下面的location配置项下面配置

      ```bash
      deny  ip地址 # 禁止的IP地址
      allow ip地址 # 允许的ip地址
      allow 0.0.0.0/0 # 允许所有的ip地址
      ```

   2. 一定是deny在allow上面，nginx先访问禁止，在允许

## Nginx 的location优先级

* location，可用配置多个配置项，支持多级配置

* location，可用控制优先级（支持正侧表达式）

   * 没有符号，代表模糊匹配，不支持正则 location /te 可以匹配 te 开头的目录和文件
   * `~`  表示执行一个正则匹配，区分大小与
   * `~*`表示执行一个正则匹配，不区分大小写
   * `=`  针对的是文件，精准匹配，不支持正则
      * 格式：`location 匹配符 正侧表达式 地址{}`

   ```shell
   Server {
       listen 80 default_server;
       server_name www.we.com;
       access—log /opt/nginx/.log jaden;
       autoirdex on ；
       autoindex_exact_size Off;
       location / {
           root /web/three;
           index index.html index.htm;
       }
   #下面正则的意思是，只要用户访问 txt 文件，都返回 404 状态码。那么就可以做到各类文件的保护，或者各种路径访问的控制
       location ~* ^.*\.txt$ {
           return 404;
       }
   }
   ```

   **匹配符号优先级**

   ==`=` 大于 `~` 大于 `~*` 大于 无符号==

   ```shell
   touch jpg
   location = /jpg {
       return 501;
   }
   location ~ /jpg {
       return 501;
   }
   location ~* /Jpg {
       return 501;
   }
   location /Jpg {
       return 501;
   }
   ```

## Nginx常用变量

| 变量名称                    | 描述                                         | 示例值示例                        |
| --------------------------- | -------------------------------------------- | --------------------------------- |
| `$args`                     | 请求中的参数字符串（查询字符串）             | `key1=value1&key2=value2`         |
| `$content_length`           | 请求头中的 "Content-Length" 值               | `1234`                            |
| `$content_type`             | 请求头中的 "Content-Type" 值                 | `application/json`                |
| `$document_root`            | 当前请求的根路径 (root)                      | `/var/www/html`                   |
| `$host`                     | 请求主机头字段，如果未设置则使用服务器名     | `example.com`                     |
| `$http_user_agent`          | 客户端User-Agent信息                         | `Mozilla/5.0 ...`                 |
| `$http_cookie`              | 请求中的Cookie信息                           | `session=abc123; lang=en`         |
| `$is_args`                  | 如果请求中有参数，则为"?"，否则为空字符串    | `?` 或 空                         |
| `$limit_rate`               | 限制连接速率，单位是字节每秒                 | `1024`                            |
| `$request_method`           | HTTP请求方法 (GET, POST, etc.)               | `GET`                             |
| `$remote_addr`              | 客户端IP地址                                 | `192.168.1.1`                     |
| `$remote_port`              | 客户端端口号                                 | `54321`                           |
| `$remote_user`              | 用户名，用于HTTP基础认证                     | `user`                            |
| `$request_filename`         | 当前请求的文件路径                           | `/var/www/html/index.html`        |
| `$request_uri`              | 完整的原始请求URI，包括参数                  | `/path/to/file?key1=value1`       |
| `$scheme`                   | 协议 (http, https)                           | `http`                            |
| `$server_protocol`          | 请求使用的协议版本                           | `HTTP/1.1`                        |
| `$server_addr`              | 服务器地址，实际处理请求的地址               | `192.168.1.10`                    |
| `$server_name`              | 服务器名称，根据请求的主机头匹配的服务器名称 | `example.com`                     |
| `$server_port`              | 服务器端口                                   | `80`                              |
| `$uri`                      | 当前的URI，不包括参数                        | `/path/to/file`                   |
| `$query_string`             | 请求中的参数字符串，同`$args`                | `key1=value1&key2=value2`         |
| `$status`                   | 当前请求的响应状态码                         | `200`                             |
| `$time_local`               | 访问时间，基于本地时区                       | `17/Dec/2024:16:47:00 +0800`      |
| `$sent_http_content_type`   | 设置响应头 "Content-Type" 的值               | `text/html`                       |
| `$sent_http_content_length` | 设置响应头 "Content-Length" 的值             | `1234`                            |
| `$sent_http_location`       | 设置响应头 "Location" 的值                   | `http://example.com/new-location` |
| `$body_bytes_sent`          | 发送给客户端的字节数，不包括响应头           | `1234`                            |
| `$connection`               | 连接序列号                                   | `123`                             |
| `$connection_requests`      | 当前连接上的请求数                           | `5`                               |
| `$msec`                     | 从Epoch开始的时间，以毫秒为单位              | `1702812420.123`                  |
| `$pipe`                     | 如果请求是通过管道传递的，则为"p"，否则为"." | `.` 或 `p`                        |
| `$ssl_cipher`               | SSL/TLS连接使用的密码套件                    | `ECDHE-RSA-AES128-GCM-SHA256`     |
| `$ssl_client_cert`          | 客户端提供的SSL证书                          | `-----BEGIN CERTIFICATE-----...`  |
| `$ssl_client_verify`        | 客户端证书验证状态                           | `SUCCESS`, `FAILED`               |
| `$ssl_protocol`             | 使用的SSL/TLS协议版本                        | `TLSv1.2`                         |

**百度网盘辅助下载工具：油猴**

```shell
location / {
    if( $host != '192.168.18.25'){
        return 304 https://192.168.18.25/gun.html
    }
}
```

**重点变量**

```shell
host           # http请求头的域名
referer        # 从那个url跳转过来的
user_agent     # 用户的浏览器客户端信息
Connection     # 是否为常链接
remote_addr    # 客户端的ip
status         # http的状态码
```

## Nginx语言配置

* nginx是通过写多个语言版本的网站来进行相互之间的切换

* 写在server项location项里面

   ```shell
   if($http_accept_language ~* ^en){
   root 英文网站
   }
   root中文网站
   ```

## Cookie 和 Session

### **Cookie**

- **设置 Cookie**：
  - Nginx 可以通过 `add_header` 指令在响应头中添加 Cookie。
    ```nginx
    location / {
        add_header Set-Cookie "example_cookie=example_value; Path=/; HttpOnly";
        proxy_pass http://backend;
    }
    ```

- **读取 Cookie**：
  - Nginx 可以通过 `$http_cookie` 变量读取客户端发送的 Cookie。
    ```nginx
    if ($http_cookie ~* "example_cookie=example_value") {
        set $is_example_cookie_set 1;
    }
    ```

- **删除 Cookie**：
  - 通过设置过期时间为过去的时间来删除 Cookie。
    ```nginx
    add_header Set-Cookie "example_cookie=; expires=Thu, 01 Jan 1970 00:00:00 GMT; Path=/";
    ```

### **Session**

- **会话管理**：
  - Nginx 本身不直接处理会话，但可以通过与后端应用程序（如 PHP、Node.js）协作来管理会话。
  - **Sticky Sessions**：在负载均衡时，可以配置 Nginx 使用 `ip_hash` 或 `sticky` 模块确保同一用户的请求总是被转发到同一个后端服务器。
    ```nginx
    upstream backend {
        ip_hash;
        server backend1.example.com;
        server backend2.example.com;
    }
    
    server {
        location / {
            proxy_pass http://backend;
        }
    }
    ```

- **Session 缓存**：
  - 可以使用 Redis 或 Memcached 来存储和共享会话数据，确保多个服务器之间的会话一致性。
  - **PHP-FPM 配置示例**：
    ```php
    session.save_handler = redis
    session.save_path = "tcp://127.0.0.1:6379"
    ```

## 的 LNMP 网站架构

### **LNMP 架构**：Linux + Nginx + MySQL + PHP

- **Linux**：操作系统，提供稳定的基础环境。
- **Nginx**：高性能的 Web 服务器，处理静态文件、反向代理、负载均衡等。
- **MySQL**：关系型数据库管理系统，存储和管理数据。
- **PHP**：服务器端脚本语言，用于开发动态网站和应用。

**配置示例**：

```nginx
server {
    listen 80;
    server_name example.com;

    root /var/www/html;
    index index.php index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }
}
```

## MySQL

- **连接池**：
  
  - Nginx 可以通过 `ngx_http_mysql_module` 或 `ngx_http_postgres_module` 直接查询 MySQL 数据库，但这不是常见的做法。通常，Nginx 作为反向代理或负载均衡器，将请求转发给后端的应用服务器（如 PHP-FPM），由应用服务器处理数据库查询。
  
- **优化**：
  - **缓存机制**：可以通过 Nginx 配置缓存机制（如 FastCGI 缓存、Redis 缓存）来减少对 MySQL 的直接访问，提高性能。
  - **读写分离**：配置 Nginx 进行读写分离，将读操作分发到只读副本，写操作分发到主数据库。
    ```nginx
    upstream mysql_master {
        server 192.168.1.1:3306;
    }
    
    upstream mysql_slave {
        server 192.168.1.2:3306;
        server 192.168.1.3:3306;
    }
    
    location /write {
        proxy_pass http://mysql_master;
    }
    
    location /read {
        proxy_pass http://mysql_slave;
    }
    ```

## WordPress

- **配置示例**：
  ```nginx
  server {
      listen 80;
      server_name example.com;
  
      root /var/www/html;
      index index.php;
  
      location / {
          try_files $uri $uri/ /index.php?$args;
      }
  
      location ~ \.php$ {
          include snippets/fastcgi-php.conf;
          fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
      }
  
      location ~ /\.ht {
          deny all;
      }
  
      # WordPress 伪静态规则
      location /wp-content/uploads/ {
          try_files $uri =404;
      }
  
      location ~* \.(js|css|png|jpg|jpeg|gif|ico)$ {
          expires max;
          log_not_found off;
      }
  }
  ```

- **优化**：
  - **启用缓存**：使用 W3 Total Cache 或 WP Super Cache 插件来缓存页面，减少数据库查询。
  - **CDN**：使用内容分发网络（CDN）加速静态资源的加载。
  - **SSL**：配置 SSL 证书，确保通信的安全性。

## Discuz 论坛

- **配置示例**：
  ```nginx
  server {
      listen 80;
      server_name forum.example.com;
  
      root /var/www/html;
      index index.php;
  
      location / {
          try_files $uri $uri/ /index.php?$query_string;
      }
  
      location ~ \.php$ {
          include snippets/fastcgi-php.conf;
          fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
      }
  
      location ~ /\.ht {
          deny all;
      }
  
      # Discuz 伪静态规则
      location /forum- {
          rewrite ^/forum-(\d+)-(\d+).html$ /forum.php?fid=$1&page=$2 last;
      }
  
      location /thread- {
          rewrite ^/thread-(\d+)-(\d+)-(\d+).html$ /viewthread.php?tid=$1&extra=page%3D$3&page=$2 last;
      }
  }
  ```

- **优化**：
  - **启用缓存**：Discuz 提供了内置的缓存机制，可以在后台启用。
  - **CDN**：使用 CDN 加速静态资源的加载。
  - **SSL**：配置 SSL 证书，确保通信的安全性。

## 伪静态

- **定义**：伪静态是通过 URL 重写技术，将动态页面的 URL 转换为看似静态页面的 URL。
- **实现**：使用 `rewrite` 指令或 `try_files` 指令。
  - **rewrite 示例**：
    ```nginx
    location / {
        rewrite ^/product/([0-9]+)$ /product.php?id=$1 last;
    }
    ```
  - **try_files 示例**：
    ```nginx
    location / {
        try_files $uri $uri/ /index.php?$args;
    }
    ```

- **常见伪静态规则**：
  - **WordPress**：
    ```nginx
    location / {
        try_files $uri $uri/ /index.php?$args;
    }
    ```
  - **Discuz**：
    ```nginx
    location /forum- {
        rewrite ^/forum-(\d+)-(\d+).html$ /forum.php?fid=$1&page=$2 last;
    }
    ```

## 正向代理

- **定义**：正向代理是客户端通过代理服务器访问互联网资源的方式。
- **配置示例**：
  ```nginx
  http {
      server {
          listen 8080;
  
          location / {
              resolver 8.8.8.8;  # DNS 解析服务器
              proxy_pass http://$http_host$request_uri;
          }
      }
  }
  ```

- **应用场景**：
  - **绕过地理限制**：访问受地理限制的网站。
  - **过滤内容**：阻止或允许特定类型的流量。
  - **加速访问**：通过缓存机制加速访问速度。

## 反向代理

- **定义**：反向代理位于服务器端，客户端不知道它正在通过代理服务器访问资源。
- **配置示例**：
  ```nginx
  upstream backend {
      server backend1.example.com;
      server backend2.example.com;
  }
  
  server {
      listen 80;
      server_name example.com;
  
      location / {
          proxy_pass http://backend;
          proxy_set_header Host $host;
          proxy_set_header X-Real-IP $remote_addr;
          proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
          proxy_set_header X-Forwarded-Proto $scheme;
      }
  }
  ```

- **应用场景**：
  - **负载均衡**：将请求分发到多个后端服务器。
  - **SSL 终止**：解密 HTTPS 请求，减轻后端服务器的负担。
  - **缓存**：缓存静态资源，减少后端服务器的压力。

## Nginx 的架构部署

### **高可用性 (HA) 和负载均衡**

- **负载均衡**：
  - **轮询 (Round Robin)**：默认的负载均衡算法，每个请求按顺序分配给不同的后端服务器。
    ```nginx
    upstream backend {
        server backend1.example.com;
        server backend2.example.com;
    }
    ```

  - **加权轮询 (Weighted Round Robin)**：为不同后端服务器分配权重，权重越高的服务器接收到的请求越多。
    ```nginx
    upstream backend {
        server backend1.example.com weight=3;
        server backend2.example.com weight=1;
    }
    ```

  - **IP 哈希 (IP Hash)**：根据客户端 IP 地址的哈希值选择后端服务器，确保同一客户端的请求总是被转发到同一台服务器。
    ```nginx
    upstream backend {
        ip_hash;
        server backend1.example.com;
        server backend2.example.com;
    }
    ```

  - **最少连接 (Least Connections)**：将请求分配给当前连接数最少的后端服务器。
    ```nginx
    upstream backend {
        least_conn;
        server backend1.example.com;
        server backend2.example.com;
    }
    ```

- **健康检查**：
  - **Nginx Plus** 提供了内置的健康检查功能，可以自动检测后端服务器的状态，并在服务器不可用时将其从负载均衡池中移除。
  - **第三方模块**：对于开源版 Nginx，可以使用第三方模块（如 `nginx-upstream-check-module`）来实现健康检查。

### **缓存**

- **FastCGI 缓存**：Nginx 可以缓存 PHP 等动态内容，减少对后端服务器的压力。
  - **配置示例**：
    ```nginx
    fastcgi_cache_path /var/cache/nginx levels=1:2 keys_zone=my_cache:10m max_size=1g inactive=60m use_temp_path=off;
    
    server {
        location ~ \.php$ {
            fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
            fastcgi_cache my_cache;
            fastcgi_cache_valid 200 60m;
            fastcgi_cache_bypass $no_cache;
            fastcgi_no_cache $no_cache;
        }
    }
    ```

- **Redis 缓存**：使用 Redis 存储和共享会话数据，确保多个服务器之间的会话一致性。
  - **PHP-FPM 配置示例**：
    ```php
    session.save_handler = redis
    session.save_path = "tcp://127.0.0.1:6379"
    ```

### **SSL/TLS**

- **Let's Encrypt**：使用 Let's Encrypt 提供的免费 SSL 证书，确保通信的安全性。
  - **Certbot**：Certbot 是一个自动化工具，可以帮助你获取和安装 Let's Encrypt 证书。
    ```bash
    sudo apt-get install certbot python3-certbot-nginx
    sudo certbot --nginx -d example.com -d www.example.com
    ```

- **自动续期**：配置定时任务自动续期 SSL 证书。
  - **crontab 配置**：
    ```bash
    0 0 * * * /usr/bin/certbot renew --quiet
    ```

### **日志和监控**

- **访问日志和错误日志**：配置 Nginx 的访问日志和错误日志，记录服务器的运行情况。
  - **配置示例**：
    ```nginx
    access_log /var/log/nginx/access.log;
    error_log /var/log/nginx/error.log;
    ```

- **监控工具**：使用 Prometheus、Grafana 等监控工具实时监控系统性能。
  - **Prometheus Exporter**：安装 Nginx Exporter 收集 Nginx 的指标数据。
    
    ```bash
    sudo apt-get install prometheus-node-exporter
    ```
  
- **报警系统**：配置报警系统（如 Prometheus Alertmanager、Zabbix）在出现问题时及时通知管理员。

### **自动扩展**

- **容器化**：使用 Docker 和 Kubernetes 实现自动扩展和弹性伸缩。
  - **Docker Compose**：使用 Docker Compose 文件定义和运行多容器应用。
    ```yaml
    version: '3'
    services:
      web:
        image: nginx
        ports:
          - "80:80"
        volumes:
          - ./html:/usr/share/nginx/html
      php:
        image: php:7.4-fpm
        volumes:
          - ./html:/var/www/html
    ```

  - **Kubernetes**：使用 Kubernetes 管理容器化的应用，实现自动扩展和故障恢复。
    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: nginx-deployment
    spec:
      replicas: 3
      selector:
        matchLabels:
          app: nginx
      template:
        metadata:
          labels:
            app: nginx
        spec:
          containers:
          - name: nginx
            image: nginx:1.19
            ports:
            - containerPort: 80
    ```
