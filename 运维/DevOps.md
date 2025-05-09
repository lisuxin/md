[toc]

==devops:开发运维一体化，解决开发与运维之间沟通问题==

![image-20250326132937699](../typoratuxiang/yunwei/cicd.png)

## GitLab

* GitLab是利用Ruby on Rails一个开源的版本管理系统，实现一个自托管的Git项目仓库，可通过Web界面进行访问公开的或者私人项目。与Github类似，GitLab能够浏览源代码，管理缺陷和注释。可以管理团队对仓库的访问，它非常易于浏览提交过的版本并提供一个文件历史库。团队成员可以利用内置的简单聊天程序(Wall)进行交流。它还提供一个代码片段收集功能可以轻松实现代码复用，便于日后有需要的时候进行查找。

### **环境部署**

1. docker镜像部署直接拉取镜像

   1. 拉取镜像`docker pull swr.cn-north-4.myhuaweicloud.com/ddn-k8s/docker.io/twang2218/gitlab-ce-zh:latest`
   2. 编写yml、运行yml`kubectl apply -f gitlab-deployment.yaml`
   
2. 手动部署

   1. 配置yum源

      ```shell
      vim /etc/yum.repos.d/gitlab-ce.repo
      [gitlab-ce]
      name=gitlab-ce
      baseurl=http://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/yum/el6
      Repo_gpgcheck=0
      Enabled=1
      Gpgkey=https://packages.gitlab.com/gpg.key
      # 或者
      curl -s https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash
      ```

   2. 更新本地缓存

      ```shell
      yum makecache
      ```

   3. 安装社区版

      ```shell
      yum install gitlab-ce        #自动安装最新版
      yum install gitlab-ce-x.x.x    #安装指定版本 
      ```

   4. 修改配置文件防止端口冲突

      1. 修改 `gitlab` 配置文件 `/etc/gitlab/gitlab.rb`

         ```shell
         external_url 'ip' -----> external_url 'http://ip:端口'
         ```

      2. `nginx`配置文件`/var/opt/gitlab/nginx/conf/gitlab-http.conf`

         ```shell
         # 将访问转发给对应端口
         listen *:端口;
         ```

      3. 重载配置生效，然后重启服务

         ```shell
         gitlab-ctl reconfigure
         gitlab-ctl restart
         ```

      4. 访问` http://ip:端口`
      
         * 用户名**root**，首次登陆需设定密码，而且密码至少**8**位
      
      5. 常用命令
      
         ```shell
         sudo gitlab-ctl start    # 启动所有 gitlab 组件；
         sudo gitlab-ctl stop        # 停止所有 gitlab 组件；
         sudo gitlab-ctl restart        # 重启所有 gitlab 组件；
         sudo gitlab-ctl status        # 查看服务状态；
         sudo gitlab-ctl reconfigure        # 启动服务；
         sudo vim /etc/gitlab/gitlab.rb        # 修改默认的配置文件；
         gitlab-rake gitlab:check SANITIZE=true --trace    # 检查gitlab；
         sudo gitlab-ctl tail        # 查看日志；
         ```

3. 链接git

   1. 在GitLab的主页中新建一个Project

   2. 添加ssh key导入步骤2中生成的密钥文件内容.

   3. 在linux配置个人使用git

      ```shell
      git config --global user.name "XXX"  
      git config --global user.email "XXX.com" 
      git clone git@ihjlsfhdkfx1gk8v3Z:root/test.git
      ```

### 基本操作

1. 登录：输入地址登录
2. 修改密码：`Profile Settings ------ Password -------修改密码-------Save password`
3. 项目管理
   1. 新建项目`projects-----项目名称-----New project------New project`
      * 创建时可以选择在自己用户下创建或者某个群组内创建
   2. 编辑或删除项目
      * `edit project---------Project`
4. 用户管理（管理员使用，非管理员跳过此步骤）
   1. 新建用户
      * 点击顶端的Admin Area按钮
   2. 编辑和删除用户
5. 组管理（管理员使用，非管理员跳过此步骤）
   1. 新建组
   2. 编辑或删除组
   3. 添加组成员
   4. 修改成员的权限（owner用户操作）
   5. 从组管理添加项目
6. 权限说明
   * Guest(匿名用户) - 创建项目、写留言薄
   * Reporter（报告人）- 创建项目、写留言薄、拉项目、下载项目、创建代码片段
   * Developer（开发者）- 创建项目、写留言薄、拉项目、下载项目、创建代码片段、创建合并请求、创建新分支、推送不受保护的分支、移除不受保护的分支 、创建标签、编写wiki
   * Master（管理者）- 创建项目、写留言薄、拉项目、下载项目、创建代码片段、创建合并请求、创建新分支、推送不受保护的分支、移除不受保护的分支 、创建标签、编写wiki、增加团队成员、推送受保护的分支、移除受保护的分支、编辑项目、添加部署密钥、配置项目钩子
   * Owner（所有者）- 创建项目、写留言薄、拉项目、下载项目、创建代码片段、创建合并请求、创建新分支、推送不受保护的分支、移除不受保护的分支 、创建标签、编写wiki、增加团队成员、推送受保护的分支、移除受保护的分支、编辑项目、添加部署密钥、配置项目钩子、开关公有模式、将项目转移到另一个名称空间、删除项目

## Jenkins

==Jenkins 是一个开源的 **自动化服务器**，主要用于实现软件开发中的 **持续集成（CI）** 和 **持续交付/部署（CD）**（CI/CD）。它通过自动化构建、测试、部署等流程，帮助开发团队快速交付高质量软件。==

* **CI/CD**
  * CI：持续集成
    * 开发————git————（构建）—————Jenkins————Docker镜像————Docker仓库—————测试
    * 自动触发代码提交后的构建和测试，确保代码变更不会破坏现有功能。
  * CD：持续交付
    * kubernetes———滚动更新
    * 将通过测试的代码自动部署到测试环境、预发布环境或生产环境。
* **典型工作流程**
  1. 代码提交：开发者推送代码到 Git 仓库。
  2. 触发构建：Jenkins 检测到代码变更，拉取最新代码。
  3. 构建与测试：执行编译、运行单元测试、代码扫描等。
  4. 生成制品：打包应用（如生成 JAR 文件或 Docker 镜像）。
  5. 部署：根据规则将制品部署到指定环境（测试/生产）。
  6. 通知：通过邮件、Slack 等通知团队构建结果。

### 安装

==全部使用镜像（容器）的方式==

1. 服务器准备（内存最少4G）

   * 本地自己电脑安装`git`
   
   * 在每一个服务器内都安装`docker`，创建k8s集群（master:192.168.31.98；node:31.96）
   
   * 31.96
     
     * 拉取`gitLab`（镜像）到当前节点
     
     * 使用K8s集群`pod-definition.yml`在当前节点上，使用当前宿主机暴露端口进行运行
     
       ```yaml
       apiVersion: apps/v1  # Kubernetes API版本定义
       kind: Deployment     # 资源类型：部署
       metadata:            # 元数据配置
         name: gitlab-ce-zh # 部署名称
         labels:           # 标签列表
           app: gitlab-ce-zh # 应用标签
       spec:               # 规格描述
         replicas: 1       # 副本数设置为1
         selector:         # 标签选择器配置
           matchLabels:    # 匹配带有以下标签的Pod
             app: gitlab-ce-zh
         template:         # Pod模板
           metadata:       # 模板元数据
             labels:       # Pod标签
               app: gitlab-ce-zh
           spec:           # 容器规格
             nodeSelector: # 节点选择器，指定运行该Pod的节点
               kubernetes.io/hostname: k8s-node-96  # 确保节点有此标签
             containers:   # 容器列表
             - name: gitlab  # 容器名
               image: swr.cn-north-4.myhuaweicloud.com/ddn-k8s/docker.io/twang2218/gitlab-ce-zh:latest  # 使用的镜像
               ports:       # 容器端口配置
               - containerPort: 80  # HTTP服务端口
                 name: http
               - containerPort: 443 # HTTPS服务端口
                 name: https
               - containerPort: 22  # SSH服务端口
                 name: ssh
               volumeMounts: # 卷挂载配置
               - mountPath: /etc/gitlab  # GitLab配置目录
                 name: gitlab-config
               - mountPath: /var/opt/gitlab  # GitLab数据目录
                 name: gitlab-data
               - mountPath: /var/log/gitlab  # GitLab日志目录
                 name: gitlab-logs
               resources:    # 资源限制和请求
                 limits:     # 最大资源限制
                   cpu: "2"  # CPU限制
                   memory: 4Gi  # 内存限制
                 requests:   # 请求的资源量
                   cpu: "1"  # CPU请求
                   memory: 2Gi  # 内存请求
             volumes:       # 卷列表
             - name: gitlab-config  # 配置卷名
               hostPath:    # 主机路径配置
                 path: /opt/gitlab/config  # 在主机上的路径
                 type: DirectoryOrCreate  # 如果不存在则创建目录
             - name: gitlab-data
               hostPath:
                 path: /opt/gitlab/data
                 type: DirectoryOrCreate
             - name: gitlab-logs
               hostPath:
                 path: /opt/gitlab/logs
                 type: DirectoryOrCreate
       
       ---
       apiVersion: v1      # Kubernetes API版本定义
       kind: Service       # 资源类型：服务
       metadata:           # 元数据配置
         name: gitlab-service  # 服务名称
       spec:               # 规格描述
         type: NodePort    # 服务类型：节点端口
         selector:         # 标签选择器配置
           app: gitlab-ce-zh  # 与部署匹配的标签
         ports:            # 服务端口配置
           - name: http    # HTTP服务
             port: 80      # 服务暴露端口
             targetPort: 80 # 目标端口（容器端口）
             nodePort: 30080  # 节点端口，范围30000-32767
           - name: https   # HTTPS服务
             port: 443     # 服务暴露端口
             targetPort: 443
           - name: ssh     # SSH服务
             port: 22      # 服务暴露端口
             targetPort: 22
       ```
     
     * 做`gitLab`初始化配置
     
       1. 第一次登录查看密码，进入容器在`/etc/exec/initial_root_password`用户名是`root`
     
          1. 无法找到密码，通过GitLab Rails控制台设置一个新的root密码
     
             * 进入容器`kubectl exec -it gitlab-ce-zh-756d69b6-bzvqc -- /bin/bash`
     
             * 运行`gitlab-rails console -e production`
     
             * 在打开的控制台中输入如下Ruby代码来更改密码：
     
               ```shell
               user = User.where(id: 1).first # 获取ID为1的用户，通常是root用户
               user.password = 'new_password' # 设置新密码
               user.password_confirmation = 'new_password' # 确认新密码
               user.save! # 保存更改
               exit # 退出控制台
               ```
     
       2. 浏览器访问修改密码
     
   * 31.98
     
     * 下载安装`jdk、maven`
     
       1. 下载上传解压`tar -zxvf 要解压的文件 -C`
       2. 修复maven中的配置文件
     
     * 拉取`Jenkins`镜像到当前节点运行容器（使用K8s集群`jenkins-deployment.yml`）
     
       ```yaml
       apiVersion: apps/v1
       kind: Deployment
       metadata:
         name: jenkins-deployment
         labels:
           app: jenkins
       spec:
         replicas: 1
         selector:
           matchLabels:
             app: jenkins
         template:
           metadata:
             labels:
               app: jenkins
           spec:
             # 强制调度到指定节点（需确认节点标签）
             nodeSelector:
               kubernetes.io/hostname: k8s-node-96
             # 配置 DNS 解析（核心修复点）
             dnsConfig:
               nameservers:
                 - 114.114.114.114  # 国内公共 DNS
                 - 8.8.8.8          # Google DNS
               options:
                 - name: ndots
                   value: "1"
             containers:
             - name: jenkins
               image: swr.cn-north-4.myhuaweicloud.com/ddn-k8s/docker.io/kubesphere/ks-jenkins:v3.4.1-2.319.3
               ports:
               - containerPort: 8080
                 name: http
               - containerPort: 50000
                 name: agent
               volumeMounts:
               - mountPath: /var/jenkins_home
                 name: jenkins-data
               resources:
                 limits:
                   cpu: "2"
                   memory: 2Gi
                 requests:
                   cpu: "0.5"
                   memory: 1Gi
             volumes:
             - name: jenkins-data
               hostPath:
                 path: /opt/jenkins
                 type: DirectoryOrCreate
       ---
       apiVersion: v1
       kind: Service
       metadata:
         name: jenkins-service
       spec:
         type: NodePort
         selector:
           app: jenkins
         ports:
           - name: http
             port: 8080
             targetPort: 8080
             nodePort: 30081
           - name: agent
             port: 50000
             targetPort: 50000
       ---
       # 允许所有出站流量的网络策略（按需使用）
       apiVersion: networking.k8s.io/v1
       kind: NetworkPolicy
       metadata:
         name: allow-egress
       spec:
         podSelector:
           matchLabels:
             app: jenkins
         policyTypes:
         - Egress
         egress:
         - {}
       ```
     
     * 浏览器访问`Jenkins`
     
     * 第一次访问需要输入密码、密码在日志中`kubectl logs`
     
       * 查看密码`cat /opt/jenkins/secrets/initialAdminPassword`
     
     * 配置jenkins使用国内镜像地址修改数据卷中`hudson.model.UpdateCenter.xml`文件（阿里云）
     
       ```xml
       <?xml version='1.1' encoding='UTF-8'?>
       <jenkins>
         <updateCenter>
           <sites>
             <site>
               <id>default</id>
               <url>https://mirrors.aliyun.com/jenkins/updates/current/update-center.json</url>
             </site>
           </sites>
         </updateCenter>
       </jenkins>
       ```
     
     * 选择插件安装（安装）新建用户名，配置实例直接保存
     
       * manage(选择安装插件)，选择Available；搜索安装==Git Parameter、publish Over SSH==勾选然后install安装
     
   * 配置jentins
   
     1. 将jdk和maven放在Jenkins数据持久化目录
     2. 配置jenkins
        1. maven—–jdk：manag jenkins———–tools配置
        2. ssh sever：manag jenkins—-System

### CI

1. 在gitlab上创建厂库、将代码提交到仓库

2. 在jenkins上新item——freestyle project

   1. 源码管理配置（source code management）配置git输入git仓库地址，添加用户名密码

   2. 配置maven打包（Buid Steps）选择maven版本，输入命令`clean package -DskipTest`打包跳过测试

      ![image-20250321061158490](../typoratuxiang/yunwei/jenkins2.png)

   3. 在当前项目目录下新建dockerfile目录编写dockerflie、和k8syml

      ```yml
      FROM swr.cn-north-4.myhuaweicloud.com/ddn-k8s/docker.io/library/openjdk:17-jdk-slim
      COPY jenkinssandqm.jar /user/local/
      WORKDIR /user/local
      EXPOSE 8080
      ENTRYPOINT ["java", "-jar", "jenkinssandqm.jar"]
      # k8s
      version: '0.1'
      services:
        jenkinssandqm:
          build:
            context: ./
            dockerfile: dockerfile
          image: jenkinssandqm:v0.1
          container_name: jenkinssandqm
          ports:
            - 8080:8080
      ```
   
   4. 在jinkins中配置构建后操作，将dockerfile目录也复制到当前宿主机并且编写Exec  command
   
      * name选择配置的gitlab过来的文件存放路径
   
      * suorce files选择gitlab到本地需要的文件
   
      * 第一次构建镜像要在绝对路径上构建
   
        ```shell
        cd /export/gitlabssh/Dockerfile
        mv ../target/*.jar ./
        kubectl delete deployment jenkinssandqm-deployment
        kubectl delete service jenkinssandqm-service
        docker build -t jenkinssandqm:v1.0 . 
        kubectl apply -f ./jenkinssandqm-deployment.yml
        docker image prune -f
        ```
   
        ![image-20250326005152022](../typoratuxiang/yunwei/jenkins1.png)
   
   5. 清理悬空镜像`docker image prune -f`

### CD

1. 配置参数化构建过程

   ![image-20250326010814641](../typoratuxiang/yunwei/cd1.png)

2. 在Build Steps上加入增加构建步骤，放到maven前面

   ![image-20250326011853091](../typoratuxiang/yunwei/cd2.png)

3. 在gitlab上给代码打标签

### Sonar Qube

==代码质量检查==

1. 安装
   1. 拉取镜像因为Sonar Qube需要PostgreSQL数据库支持所有需要拉取postgres镜像

   2. 拉取Sonar Qube镜像

   3. 创建k8s运行yml文件、需要先运行PostgreSQL在运行Sonar Qube镜像，因为Sonar Qube依赖与PostgreSQL

      ```yml
      apiVersion: apps/v1
      kind: Deployment
      metadata:
        name: qualityinspection-deployment
      spec:
        selector:
          matchLabels:
            app: qualityinspection
        template:
          metadata:
            labels:
              app: qualityinspection
          spec:
            nodeSelector:
              kubernetes.io/hostname: k8s-node-96
            containers:
            - name: qualityinspection
              image: swr.cn-north-4.myhuaweicloud.com/ddn-k8s/docker.io/bitnami/postgresql:latest
              resources:
                limits:
                  memory: "512Mi"
                  cpu: "500m"
              ports:
              - containerPort: 5432
                name: postgresq-port
              env:
              - name: POSTGRES_USER
                value: "sonaruser"
              - name: POSTGRES_PASSWORD
                value: "sonarpassword"
              - name: POSTGRES_DB
                value: "sonarqube"
              volumeMounts:
              - mountPath: /bitnami/postgresql
                name: postgresql-sql
              - mountPath: /docker-entrypoint-initdb.d
                name: postgresql-initdb
              - mountPath:  /docker-entrypoint-preinitdb.d
                name: postgresql-preinitdb
            volumes:
            - name: postgresql-sql
              hostPath:
                path: /opt/postgresql/sql
                type: DirectoryOrCreate
            - name: postgresql-initdb
              hostPath:
                path: /opt/postgresql/initdb
                type: DirectoryOrCreate
            - name: postgresql-preinitdb
              hostPath:
                path: /opt/postgresql/preinitdb
                type: DirectoryOrCreate
      ---
      apiVersion: v1
      kind: Service
      metadata:
        name: qualityinspection-service
      spec:
        type: NodePort
        selector:
          app: qualityinspection
        ports:
        - name: postgresq-port
          port: 5432
          targetPort: 5432
          nodePort: 30083
      ```

      ```yml
      apiVersion: apps/v1
      kind: Deployment
      metadata:
        name: sonarqube-deployment
      spec:
        selector:
          matchLabels:
            app: sonarqube
        template:
          metadata:
            labels:
              app: sonarqube
          spec:
            nodeSelector:
              kubernetes.io/hostname: k8s-node-96
            containers:
            - name: sonarqube
              image: swr.cn-north-4.myhuaweicloud.com/ddn-k8s/docker.io/sonarqube:8.9-community
              resources:
                limits:
                  memory: "2Gi"
                  cpu: "1"
              ports:
              - containerPort: 9000
                name: sonarqube-port
              env:
              - name: SONARQUBE_JDBC_USERNAME
                value: "sonaruser"
              - name: SONARQUBE_JDBC_PASSWORD
                value: "sonarpassword"
              - name: SONARQUBE_JDBC_URL
                value: "jdbc:postgresql://qualityinspection-service.default.svc.cluster.local:5432/sonarqube"
              volumeMounts:
              - mountPath: /opt/sonarqube
                name: sonarqube-data
            volumes:
            - name: sonarqube-data
              hostPath:
                path: /opt/sonarqube
                type: DirectoryOrCreate
      ---
      apiVersion: v1
      kind: Service
      metadata:
        name: sonarqube-service
      spec:
        type: NodePort
        selector:
          app: sonarqubeport
        ports:
        - name: sonarqube-port
          port: 9000
          targetPort: 9000
          nodePort: 30084
      ```

2. Sonar Qube需要linux虚拟内存为262144、在`/etc/sysctl.conf`文件里添加`vm.max_map_count = 262144`、使用`sysctl -p`应用

3. Sonar Qube默认用户名密码admin

4. 使用maven检测

   1. 在maven的settings.xml里面添加

      ```xml
      <profiles>
        <profile>
          <id>sonar</id>
          <activation>
            <activeByDefault>true</activeByDefault>
          </activation>
          <properties>
            <sonar.login>admin</sonar.login>
            <sonar.password>Your Project Name</sonar.password>
            <sonar.host.url>http://192.168.31.96:30084</sonar.host.url>
          </properties>
        </profile>
      </profiles>
      <activeProfiles>
        <activeProfile>sonar</activeProfile>
      </activeProfiles>
      ```

   2. idea的命令行中输入`mvn sonar:sonar`

5. 使用soanr-scanner检测（与Jenkins结合）

   1. 下载soanr-scanner在linux里解压放到持久化的Jenkins数据卷中

   2. 进入soanr-scanner的conf文件夹修改配置文件，将`sonar-scanner.properties`配置文件中的地址，修改为自己的地址`sonar.host.url=http://localhost:9000`

   3. 进入代码存放目录`workspace`里面(一定是代码目录，而不是jenkins的名称)、使用`sonar-scanner`命令的绝对路径、也就是sonar-scanner的bin目录下

   4. 点击自己头像选择我的账号（my account）选择安全（Security），随便输入点什么就可以生成一个令牌（key)

   5. 检测代码

      ```bash
      /opt/jenkins/sonar-scanner/bin/sonar-scanner -Dsonar.sources=./ -Dsonar.projectname=jenkinssandqm -Dsonar.login=65458c9c525ac232732f364656b894297aa54fd6 -Dsonar.projectKey=jenkinssandqm-key -Dsonar.java.binaries=./target/
      # /opt/jenkins/sonar-scanner/bin/sonar-scanner  sonar-scanner的绝对路径
      # -Ssoanr.sources=./ 指定为当前目录
      # -Dsonar.projectname=jenkinssandqm 给当前项目指定名称
      # -Dsonar.login=65458c9c525ac232732f364656b894297aa54fd6 指定连接Sonar Qube的key
      # -Dsonar.projectKer=jenkinssandqm-key 给key命名
      # -Dsonar.java.binaries=./target/ 指定编译后代码存放位置
      ```

6. 在jenkins中配置Sonar Qube一体化

   1. 下载插件Sonar Qube

   2. 在jenkins的系统配置里面配置`SonarQube servers`添加一个

      ![image-20250410025910861](../typoratuxiang/yunwei/sqb1.png)

   3. 点击添加添加凭据

      ![image-20250410030312501](../typoratuxiang/yunwei/sqb2.png)

   4. 在jenkins中添加全局配置，找到`SonarQube Scanner 安装`(不要勾选自动安装)

      ![image-20250410031357447](../typoratuxiang/yunwei/sqb3.png)

   5. 在任务中配置（构建后操作）

      ```bash
      sonar.projectname=${JOB_NAME}
      sonar.projectKey=${JOB_NAME}
      sonar.sources=./
      sonar.java.binaries=./target/
      ```

      ![image-20250410032615569](../typoratuxiang/yunwei/sqb4.png)

### Harbor

==镜像仓库==

1. 拉取镜像，使用yml运行

2. github上，下载压缩包解压安装，下载`harbor-offline-installer-v2.12.1-rc1`

   1. 进入解压目录harbor、修改文件 `harbor.yml.tmpl`名为`harbor.yml`

   2. 修改文件内容`harbor.yml`

      ```bash
      hostname: 192.168.31.96
      http:
        # port for http, default is 80. If https enabled, this port will redirect to https port
        port: 80
      # 注释掉https
      # 查看harbor的密码
      harbor_admin_password: Harbor12345
      # 还可以修改数据目录
      data_volume
      ```

   3. 运行`install.sh`进行安装，最终运行起来还是以docker容器在运行

   4. 定制harbor服务启动文件`/etc/systemd/system/harbor.service`

3. 镜像仓库基本使用

   1. 新建仓库

   2. 将自己的镜像命名`harbor地址/项目名称/镜像名称：版本`

   3. 修改`/etc/docker/daemon.json`文件，加上镜像仓库地址、修改完成重启docker服务`systemctl restart docker`

      ```json
      {
                "exec-opts": ["native.cgroupdriver=systemd"]// 指定容器运行时的执行选项。
                "insecure-registries": ["192.168.31.96:80"]// 允许 Docker 使用非安全的私有镜像仓库。
      }
      ```

   4. 修改镜像名称`docker tag bce6b32dabf9 192.168.31.96:80/cs/jenkinssandqm:v1.0`

   5. 登录镜像仓库`docker login -u admin -p Harbor12345 192.168.31.96:80`

   6. 推送至镜像仓库`docker push 192.168.31.96:80/cs/jenkinssandqm:v1.0`

   7. 之后就可以正常拉取，推送

#### 在jenkins内部使用Harbor

1. 在Jenkins内部安装docker

2. 使用宿主机的docker

   1. 修改`/var/run/`目录下的`docker.sock`文件的所属用户，用户组，全部改为root`chown root:root docker.sock`

   2. 给所有用户`docker.sock`文件读和改的权限`chmod o+rw docker.sock`

   3. 修改jenkins的启动yml，将docker的文件==`docker.sock`、`daemon.json`==和`/usr/bin/docker`映射到jenkns内部

      ```yaml
      volumeMounts:
              - mountPath: /var/jenkins_home
                name: jenkins-data
              - mountPath: /var/run/docker.sock
                subPath: docker.sock
                name: jenkins-docker-sock
              - mountPath: /usr/bin/docker
                subPath: docker
                name: jenkins-docker
              - mountPath: /etc/docker/daemon.json
                subPath: daemon.json
                name: jenkins-docker-daemon
            volumes:
            - name: jenkins-data
              hostPath:
                path: /opt/jenkins
                type: DirectoryOrCreate
            - name: jenkins-docker-sock
              hostPath:
                path: /var/run/docker.sock
                type: File
            - name: jenkins-docker
              hostPath:
                path: /usr/bin/docker
                type: File
            - name: jenkins-docker-daemon
              hostPath:
                path: /etc/docker/daemon.json
                type: File
      ```

3. 使用jenkins推送镜像到镜像仓库

   ```bash
   cd Dockerfile
   mv ../target/*.jar ./
   docker build -t jenkinssandqm:$tag . 
   docker tag jenkinssandqm:$tag 192.168.31.96:80/cs/jenkinssandqm:$tag
   docker login -u admin -p Harbor12345 192.168.31.96:80
   docker push 192.168.31.96:80/cs/jenkinssandqm:$tag
   ```

   ![image-20250425161113725](../typoratuxiang/yunwei/harbor1.png)

4. 写shell脚本进行构建后操作

   ```bash
   #/bin/bash
   harbor_address=$1
   harbor_warehouse=$2
   harbor_mirror=$3
   harbor_tag=$4
   imageName=$harbor_address/$harbor_warehouse/$harbor_mirror:$harbor_tag
   docker_ps_id=`docker ps -a | grep ${harbor_mirror} | awk '{print $1}'`
   echo $docker_ps_id
   if [ "$docker_ps_id" != "" ]; then
           kubectl delete deployment $harbor_mirror-deployment
           kubectl delete service $harbor_mirror-service
   fi
   docker_image_tag=`docker images | grep ${harbor_mirror}|awk '{print $2}'`
   echo $docker_image_tag
   if [[ "$docker_image_tag" =~ "$harbor_tag" ]]; then
           docker rmi -f $imageName
   fi
   docker login -u admin -p Harbor12345 192.168.31.96:80
   docker pull $imageName
   kubectl apply -f /export/gitlabssh/Dockerfile/$harbor_mirror-deployment.yml
   echo "SUCCESS"
   ```

5. 在jenkins里面添加构建后操作

   ![image-20250426052151332](../typoratuxiang/yunwei/jenkins3.png)

## pipeline

==流水线构建模式==

### 语法

```java
//所有的脚本命令都在pipeline中执行
pipeline {
    agent any//指定任务在那个集群节点中执行
    
    environment {//指定全局变量，方便后面使用
        key = 'value' //使用全局变量的方式 ${key}
    }
    
    stages {
        stage('Hello') {//给当前步骤命名
            steps {
                echo 'Hello World'//执行当前步骤的流水线语法
            }
        }
        stage('Hello') {//给当前步骤命名
            steps {
                echo 'Hello World'//执行当前步骤的流水线语法
            }
    }
    post{//配置推送远端
        success{//成功
            robot:''//配置的推送远端的名称
            type: 'MARKDOWN' //推送远端的语法格式
            title: ""//推送远端输出的文本
        }
        failure{//失败
            robot:''//配置的推送远端的名称
            type: 'MARKDOWN' //推送远端的语法格式
            title: ""//推送远端输出的文本
        } 
    }
}

```

### 使用方法

1. 同样可以使用参数化构建过程，添加相应参数、例如版本信息等等

2. 可以在代码仓库里面写jenkinsfile文件，也就是流水线语法的文件、jenkins和会使用这个文件作为执行文件进行执行

   * jenkins(J一定要大写)

3. jenkinfile使用版本控制工具（git）

   ![image-20250428170345512](../typoratuxiang/yunwei/jenkins8.png)

4. 使用maven(sh)

   ![image-20250428171445523](../typoratuxiang/yunwei/jenkins9.png)

5. sonarqube和harbor同maven一样使用shell命令

6. 部署使用

   ![image-20250428225655251](../typoratuxiang/yunwei/jenkins10.png)
   
   * `execCommand: "sh /export/sh/testcicd.sh ${harboraddress} ${harborwarehouse} ${harbormirror} ${tag}",`这个地方必须使用一行双引号

### 构建完整语法

```
pipeline {

    agent any

    environment{
        harboruser = 'admin'
        harboraddress = '192.168.31.96:80'
        harborwarehouse = 'cs'
        harbormirror = 'jenkinssandqm'
        harborpassword = 'Harbor12345'
    }

    stages {
        stage('git') {
            steps {
                checkout poll: false, scm: scmGit(branches: [[name: "${tag}"]], extensions: [], userRemoteConfigs: [[credentialsId: '21537b59-4ce9-49c0-8190-abd0ac87c8dc', url: 'http://192.168.31.96:30080/root/jenkinslll.git']])
                }
            }
        stage('maven') {
            steps {
                sh '/var/jenkins_home/maven/bin/mvn clean package -DskipTests'
                }
            }
        stage('sonarqube') {
            steps {
                sh '/var/jenkins_home/sonar-scanner/bin/sonar-scanner -Dsonar.sources=./ -Dsonar.projectname="${harbormirror}" -Dsonar.login=65458c9c525ac232732f364656b894297aa54fd6 -Dsonar.projectKey=jenkinssandqm-key -Dsonar.java.binaries=./target/'
                }
            }
        stage('docker镜像') {
            steps {
                sh '''mv ./target/*.jar ./Dockerfile/
                docker build -t "${harbormirror}":"${tag}" ./Dockerfile/'''
                }
            }
        stage('推送harbor') {
            steps {
                sh '''docker tag ${harbormirror}:"${tag}" "${harboraddress}"/"${harborwarehouse}"/"${harbormirror}":"${tag}"
                docker login -u "${harboruser}" -p "${harborpassword}" "${harboraddress}"
                docker push "${harboraddress}"/"${harborwarehouse}"/"${harbormirror}":"${tag}"'''
                }
            }
        stage('部署') {
            steps {
                sshPublisher(publishers: [
                    sshPublisherDesc(
                        configName: 'k8s-master-98',
                        transfers: [
                            sshTransfer(
                                cleanRemote: false,
                                excludes: '',
                                sourceFiles: 'Dockerfile/*.yml',
                                execCommand: "sh /export/sh/testcicd.sh ${harboraddress} ${harborwarehouse} ${harbormirror} ${tag}",
                                execTimeout: 120000,
                                flatten: false,
                                makeEmptyDirs: false,
                                noDefaultExcludes: false,
                                patternSeparator: '[, ]+',
                                remoteDirectory: '',
                                remoteDirectorySDF: false,
                                removePrefix: '')],
                                usePromotionTimestamp: false,
                                useWorkspaceInPromotion: false,
                                verbose: true)])
                }
            }
        }
    post{
        success{
            dingtalk(
                robot:'dingding',
                type: 'MARKDOWN',
                title: "SUCCESS",
                text:["构建成功"]
            )
        }
        failure{
            dingtalk(
                robot:'dingding',
                type: 'MARKDOWN',
                title: "FAILURE",
                text:["构建失败"]
            )
        }
    }
}
```

### 推送消息、外部软件

1. 下载插件、钉钉、微信或是其他

   * 钉钉机器人配置

     ![image-20250428160004496](../typoratuxiang/yunwei/jenkins6.png)

   * 复制webhook地址`https://oapi.dingtalk.com/robot/send?access_token=06266e012f6f175e9a618fa622a254e87540ea3eaa9c296772fdf2cbdffed3d5`

     ![image-20250428160144996](../typoratuxiang/yunwei/jenkins7.png)

2. 然后在系统配置里面进行配置

   ![image-20250428154041184](../typoratuxiang/yunwei/jenkins4.png)

   ![image-20250428160555462](../typoratuxiang/yunwei/jenkins5.png)

3. 流水线语法

   ```java
      post{//配置推送远端
           success{//成功
               robot:'',//配置的推送远端的名称
               type: 'MARKDOWN', //推送远端的语法格式
               title: "",//推送远端输出的文本
               text:["构建成功"]
           }
           failure{//失败
               robot:'',//配置的推送远端的名称
               type: 'MARKDOWN', //推送远端的语法格式
               title: "",//推送远端输出的文本
               text:["构建失败"],
           } 
       }
   ```
   

## 自动化CI

1. 在jenkins中配置《构建触发器》

   ![image-20250503200108436](../typoratuxiang/yunwei/gitlab4.png)

2. 在gitlab中配置webhook、(也就是系统钩子、粘贴构建触发器的地址)

   ![image-20250503172200403](../typoratuxiang/yunwei/gitlab2.png)

3. 在gitlab中配置允许本地请求、设置里面

   ![image-20250503172030486](../typoratuxiang/yunwei/gitlab1.png)

4. 在jenkins中配置允许gitlab访问，开启安全认证（下载gitlab插件、取消勾选）

   ![image-20250503195914936](../typoratuxiang/yunwei/gitlab3.png)

5. 取消Jenkins的参数化构建、并修改Jenkins里面使用的版本信息`${tag}`

   * 第一个`${tag}`修改为`*/master`表示使用master分支的最新更改
   * 其余`${tag}`全部修改为同一个版本，或者修改为latest，表示最新版本

6. 如果jenkinsfile文件没有进行改变那么容器就不会进行更新、需要使用k8s命令`kubect rollout restart 容器deployment名称 -n 容器的命名空间`进行更新

7. 在部署阶段可能存在找不到命令，加上命令的绝对路径`/usr/bin/kubectl`

8. 使用ssh远程，无密码方式

   1. 在本机上生成目录`.ssh`：`ssh-keygen -t rsa`
      * 容器需要使用容器内的`.ssh`
   2. 上传公钥到目标机器（需要远程到的机器）`ssh-copy-id root@192.168.157.146`
   3. 重启 SSH服务命令使其生效`service sshd restart`

### 全CI的jenkinsfile

```
pipeline {

    agent any

    environment{
        harboruser = 'admin'
        harboraddress = '192.168.31.96:80'
        harborwarehouse = 'cs'
        harbormirror = 'jenkinssandqm'
        harborpassword = 'Harbor12345'
    }

    stages {
        stage('git') {
            steps {
                checkout poll: false, scm: scmGit(branches: [[name: "*/master"]], extensions: [], userRemoteConfigs: [[credentialsId: '21537b59-4ce9-49c0-8190-abd0ac87c8dc', url: 'http://192.168.31.96:30080/root/jenkinslll.git']])
                }
            }
        stage('maven') {
            steps {
                sh '/var/jenkins_home/maven/bin/mvn clean package -DskipTests'
                }
            }
        stage('sonarqube') {
            steps {
                sh '/var/jenkins_home/sonar-scanner/bin/sonar-scanner -Dsonar.sources=./ -Dsonar.projectname="${harbormirror}" -Dsonar.login=65458c9c525ac232732f364656b894297aa54fd6 -Dsonar.projectKey=jenkinssandqm-key -Dsonar.java.binaries=./target/'
                }
            }
        stage('docker镜像') {
            steps {
                sh '''mv ./target/*.jar ./Dockerfile/
                docker build -t "${harbormirror}":"v4.0.0" ./Dockerfile/'''
                }
            }
        stage('推送harbor') {
            steps {
                sh '''docker tag ${harbormirror}:"v4.0.0" "${harboraddress}"/"${harborwarehouse}"/"${harbormirror}":"v4.0.0"
                docker login -u "${harboruser}" -p "${harborpassword}" "${harboraddress}"
                docker push "${harboraddress}"/"${harborwarehouse}"/"${harbormirror}":"v4.0.0"'''
                }
            }
        stage('部署') {
            steps {
                sshPublisher(publishers: [
                    sshPublisherDesc(
                        configName: 'k8s-master-98',
                        transfers: [sshTransfer(
                            cleanRemote: false,
                            excludes: '',
                            execCommand: '''cd /export/gitlabssh/Dockerfile
                                            /usr/bin/kubectl apply -f ./jenkinssandqm-deployment.yml
                                            /usr/bin/kubectl rollout restart deployment jenkinssandqm-deployment -n default''',
                                            execTimeout: 120000,
                                            flatten: false,
                                            makeEmptyDirs: false,
                                            noDefaultExcludes: false,
                                            patternSeparator: '[, ]+',
                                            remoteDirectory: '',
                                            remoteDirectorySDF: false,
                                            removePrefix: '',
                                            sourceFiles: 'Dockerfile/*.yml')],
                                            usePromotionTimestamp: false,
                                            useWorkspaceInPromotion: false,
                                            verbose: false)])
                }
            }
        }
    post{
        success{
            dingtalk(
                robot:'dingding',
                type: 'MARKDOWN',
                title: "SUCCESS",
                text:["构建成功"]
            )
        }
        failure{
            dingtalk(
                robot:'dingding',
                type: 'MARKDOWN',
                title: "FAILURE",
                text:["构建失败"]
            )
        }
    }
}
```

