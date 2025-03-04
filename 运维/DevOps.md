[toc]

==devops:开发运维一体化，解决开发与运维之间沟通问题==

## GitLab

* GitLab是利用Ruby on Rails一个开源的版本管理系统，实现一个自托管的Git项目仓库，可通过Web界面进行访问公开的或者私人项目。与Github类似，GitLab能够浏览源代码，管理缺陷和注释。可以管理团队对仓库的访问，它非常易于浏览提交过的版本并提供一个文件历史库。团队成员可以利用内置的简单聊天程序(Wall)进行交流。它还提供一个代码片段收集功能可以轻松实现代码复用，便于日后有需要的时候进行查找。

### **环境部署**

1. docker镜像部署直接拉取镜像

   

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



### Sonar Qube

### Harbor

### pipeline

### Kuoard