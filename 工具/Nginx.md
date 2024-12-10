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

1. 提取`nginx.conf.default`文件中的非空行和非注释到`nginx.conf`

   ```bash
   grep -Ev '#|^$' nginx.conf.default(修改的文件) > nginx.conf(需要覆盖的文件)
   ```

2. nginx文件的最小配置（重启nginx`systemctl restart nginx`）

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
       server {
       # 给网站做部署配置
           listen       80;
           # nginx的端口
           server_name  localhost;
           
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

