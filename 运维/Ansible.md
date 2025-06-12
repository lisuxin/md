[toc]

# Ansible

## 安装

1. 拉取docker镜像、yaml进行运行

2. yum进行安装

   ```bash
   yum install epel-release -y # 阿里云源
   yum install ansible -y # 安装ansible
   yum install libselinux-python -y # python依赖
   ansible --version #查询版本
   ansible-doc -s 模块名 # 参看模块的所有参数
   ```

## 主机清单

1. 命令格式：与普通linux命令一个意思

   命令：`ansible linux-zhuji -m command -a "hostname"`

   * `ansible all -m command -a "hostname"`:`all`所有主机
   * 参数：`-vvvv`运行ansible命令时查看运行过程、`debug`日志
   
   ```mermaid
   graph TB
     命令格式-->格式说明
     ansible-->命令
     linux-zhuji-->主机组名:由/etc/ansible/hosts定义
     -m-->指定模块参数
     command-->模块名
     -a-->指定模块的执行动作参数
     hostname-->批量执行的操作
   ```

### 批量管理服务器组

==清单：格式、主机和组==

1. 主机清单配置文件`/etc/ansible/hosts`

   * ini格式

     ```bash
     # 方括号中的标题是组名称，用于对主机进行分类，并决定您在什么时间以及出于什么目的控制哪些主机。组名称应遵循与创建有效的变量名称相同的准则。
     mail.example.com # 本机
     
     [webservers] # 组名称
     foo.example.com
     bar.example.com
     www[01:50].example.com # 表示01到50这个范围的所有主机
     www[01:50:2].example.com # 2表示步长，序列号之间的增量
     db-[a:f].example.com # 也可以定义字母的范围
     
     [dbservers]
     one.example.com
     two.example.com
     three.example.com
     
     # 定义一个父组，包含 webservers 和 dbservers 子组
     [production:children]
     webservers
     dbservers
     ```

   * 这是 YAML 格式的相同基本清单文件

     ```yaml
     ungrouped:
       hosts:
         mail.example.com: # 本机
     webservers: # 组名称
       hosts:
         foo.example.com:
         bar.example.com:
         www[01:50].example.com #表示01到50这个范围的所有主机
         www[01:50:2].example.com # 2表示步长，序列号之间的增量
     dbservers:
       hosts:
         one.example.com:
         two.example.com:
         three.example.com:
     prod:
       children:
         dbservers: # 表示dbservers组是prod组的子组
     ```

     1. 一个主机放在多个组
     2. 组之间创建父/子关系。父组也称为嵌套组或组的组
        * 在 INI 格式中，使用 `:children` 后缀
        * 在 YAML 格式中，使用 `children:` 条目

### 配置服务器认证

* ansible批量管理主机(认证方式)

  * 密码认证：修改`/etc/ansible/hosts`文件

    ```bash
    [webservers]
    # 在主机名后面加上 ansible_port ansible_password ansible_user
    foo.example.com ansible_port=22 ansible_password='219798' ansible_user=root  # 单个机器密码认证
    ----------------------
    [webservers:vars] # 对于一组机器进行密码认证、对密码信息进行抽象
    ansible_port=22
    ansible_password='219798'
    ansible_user=root
    [webservers]
    foo[1,10,2].example.com
    ```
  
    1. 修改宿主机密码`passwd`
    2. 修改宿主机sshd访问端口`vim /etc/ssh/ssh_config`
  
  * 公钥私钥认证
  
    * 上传公钥到目标机器（需要远程到的机器）`ssh-copy-id root@192.168.157.146`
      * 可以使用shell脚本对所有主机进行分发
    * 重启 SSH服务命令使其生效`service sshd restart`
    
  * 使用`ping`模块：
  
    * `ansible-doc -s ping`：查看`ping`模块的信息
  
    * `ansible web -m ping`意思是尝试访问这个主机，成功返回pong、失败没有返回值

### 指纹

* 关于 ansible 连接指纹确认的问题
  * ansible就是以ssh链接标准来
  * `/etc/.ssh/known_hosts`文件中存放了目标机器的指纹
  * 首次远程链接需要指纹确认（可以忽略指纹确认）
  * 解决方案
    1. 对公钥进行分发，实现免密登录，在使用ansible免密远程执行命令
    2. 先使用ssh链接一次，确认指纹，在使用ansible免密远程执行命令
    3. 修改ansible配置文件`/etc/ansible/ansible.cfg`，修改`host_key_checking = false`

### 状态颜色原理（ansible命令执行结果会有不同颜色）

* 绿色：命令以用户期望的执行了，但是状态没有发生改变；
* 黄色：命令以用户期望的执行了，并且状态发生了改变；
* 紫色：警告信息，说明 ansible 提示你有更合适的用法：
* 红色：命令错误，执行失败；
* 蓝色：详细的执行过程：
* ansible与shell的区别
  * shell：shell 脚本不够智能，不会记录上一次的执行状态，以及修改的状态，因此导致，傻瓜式的，重复性执行。效率是极其低下的，不做状态记录
  * 第一次执行，命令之后，的确对目标机器产生了修改的状态，会返回一个命令的执行结果，执行状态，存储下来；再次执行时ansible 会检测目标机器，对比这个状态，如果状态没变， ansible 就不会再执行该命令，因此效率很高。

## 常见模块

### ping模块

* 作用：测试连通性
* 语法：`ansible 主机名 -m 模块名`
* 使用：`ansible all -m ping`
* 返回值：是一个json的数据格式

### Command模块

* 作用：简单命令，在目标机器执行一些简单命令，command模块是ansible的默认模块
* 语法：`ansible 主机名 -m command -a "需要批量执行的命令"`或`ansible 主机名 -a "需要批量执行的命令"`
* 规则
  * 使用command模块不得使用变量`$HOME`
  * 使用command模块不得出现特殊符号`<、>、|、;、&`否则无法识别，需要shell模块实现
  * 使用command模块也无法使用复制的Linux命令
* 使用
  1. 查看远程主机名：`ansible all -m command -a "hostname"`
  2. 看远程主机内存：`ansible -a "free -m"`
  3. 远程创建文件、查看文件：`ansible all -a "touch /opt/"`、`ansible all -a "cat /opt/"`
  4. 远程获取机器负载`ansible all -a "uptime"`
  5. 关闭告警信息`ansible all -a "touch /opt/  warn=false"`
  6. 在所有机器上，创建用户`ansible all -a "useradd qwe"`
  7. 使用 command 提供的专有命令：这些命令用于编写 ansible-playbook ，完成服务器部署的各种复杂条件限定。
     * `chdir`：在执行命令执行，通过 cd 命令进入指定目录
     * `creates`：定义一个文件是否存在，若不存在，则运行相应命令；存在则跳过
     * `free_form(必须)`：参数信息中可以输人任何系统命实现远程管理
     * `removes`：定义一个文件是 否存在，如果存在，则运行相应命令；如果不存在则跳过
     * 练习
       * 备份`/var/log`日志目录，需要先进入根目录
         * linux命令：`cd /&& tar -zcvf /opt/log.tgz /var/log`
         * absible命令：`ansible all -a "tar -zcvf /opt/log.tgz var/log chdir=/"`
       * 在`/opt`目录下创建文件
         * linux命令：`cd /&& touch 12.log /opt`
         * absible命令：`ansible all -a "touch 12.log chdir=/opt"`

### Shell模块

* 作用：在远程节点上执行命令（复杂的命令）；也就是等于你在linux上直接执行任何复杂的命令都可以
* 语法：`ansible 主机名 -m shell -a "需要批量执行的命令"`
* 规则：执行的多个命令之间使用`;`进行分割

### copy模块

* 作用：复制文件到远程主机，只能把数据推送给远程主机节点，无法拉取数据到本地。
* 语法：`ansible all -m copy -a "src=/etc/ansible/ansible.cfg dest=/tmp/ansible.cfg owner=root group=root mode=0755"`
* 参数：
  * backup：在覆盖之前，将源文件备份，备份文件包含时间信息。有两个选项：yes|no
  * content：用于替代“src”，可以直接设定指定文件的值（指定文件内容）
  * dest：必选项。要将源文件复制到的远程主机的绝对路径，如果源文件是一个目录，那么该路径也必须是个目录
  * directory_mode：递归设定目录的权限，默认为系统默认权限
  * force：如果目标主机包含该文件，但内容不同，如果设置为yes，则强制覆盖，如果为no，则只有当目标主机的目标位置不存在该文件时，才复制。默认为yes
  * others：所有的file模块里的选项都可以在这里使用
  * src：被复制到远程主机的本地文件，可以是绝对路径，也可以是相对路径。如果路径是一个目录，它将递归复制。在这种情况下，如果路径使用“/”来结尾，则只复制目录里的内容，如果没有使用“/”来结尾，则包含目录在内的整个内容全部复制，类似于rsync。（源文件路径、指定文件）
  * owner：设定一个用户拥有拷贝到远程节点的文件权限
  * group：设定一个用户组拥有拷贝到远程节点的文件权限
  * mode：等同于`chmod`
* 示例：将本地文件`“/etc/ansible/ansible.cfg”`复制到远程服务器
  * `ansible all -m copy -a "src=/etc/ansible/ansible.cfg dest=/tmp/ansible.cfg owner=root group=root mode=0755"`

### File模块

* 作用：管理文件，设置文件目录属性，用于远程机器上所有文件的操作

* 语法：`ansible 主机名 -m file -a "需要批量执行的命令"`

* 参数：
  * src：本机位置
  * dest：目标机器位置
  * state：touch（创建目录）、directory（创建文件及目录）、hard（创建硬链接）、link（创建符号链接（软链接））、file（确保文件存在。如果该文件不存在，则不会自动创建它）
  * path：指定路径
  * owner：设定一个用户拥有拷贝到远程节点的文件权限
  * group：设定一个用户组拥有拷贝到远程节点的文件权限
  * mode：等同于`chmod`
  * force：强制创建软连接
  
* 示例
  * 创建文件、目录数据、以及对现有的文件、目录权限进行修改、对文件属性的各种操作
  
  * `ansible all -m file -a "path=/opt/log.log state=directory"`
  
  * 替换为yaml语法
  
    ```yaml
    -name：mkdir optlog
    file:
      path=/opt/log.log
      state=directory
    ```

### Script模块

* 作用：把本地脚本传输到远程节点并运行脚本
* 语法：`ansible 主机名 -m script -a "需要批量执行的命令"`
* 参数：
  * `creates`：定义一个文件是否存在，若不存在，则运行相应命令；存在则跳过
  * `free_form(必须)`：参数信息中可以输人任何系统命实现远程管理
  * `removes`：定义一个文件是 否存在，如果存在，则运行相应命令；如果不存在则跳过
* 示例：
  * 脚本`1.sh`，赋予执行权限、远程执行`ansible all -m script -a "1.sh"`

### Cron模块

* 作用：用于管理定时任务（与crontab没什么区别）
* 语法：`ansible 主机名 -m cron -a "需要批量执行的命令"`
* 参数：
  * minute：分钟；当不使用该参数时默认为`"*"`
  * hour：时
  * day：日
  * month：月
  * weekday：周
  * job：执行命令
  * name：为定时任务起名
  * state：当定时任务有命名后，可以更具名字进行删除；值：absent
* 示例：
  * 每5分钟执行一次时间同步`ansible all -m cron -a "name='ntp aliyun' minute=*/ job='ntpdate -u ntp.aliyun.com'"`
  * 删除`ntp aliyun`定时任务：`ansible all -m cron -a "name='ntp aliyun' state=absent"`

### group模块

* 作用：管理系统用户组
* 语法：`ansible 主机名 -m group -a "需要批量执行的命令"`
* 参数：
  * name：创建指定的组名
  * gid：组的id
  * state：
    * absent：移除远端主机的组
    * present：创建远端主机的组
* 示例：
  * 在远端创建组：`ansible all -m group -a "anme='system' gid='1234' state=present"`

### user模块

* 作用：管理用户的：uid、用户名、用户主组、用户附加组、创建用户、删除用户、创建关于用户的公私钥、用户过期时间、用户密码过期时间
* 语法：`ansible 主机名 -m user -a "需要批量执行的命令"`
* 参数：
  * create_home：创建家目录、设置no则不创建家目录
  * uid：创建用户uid
  * name：用户名
  * group：用户主组
  * state：
    * present：创建用户
    * absent：删除用户
  * expires：用户过期时间
  * shell：用户登录解释器
* 示例：
  * 创建用户、没有家目录、不允许登录`ansible 主机名 -m user -a "group='system' name='system' uid='1234' create_home=no "`

### Yum模块

* 作用：软件管理、安装、卸升级
* 语法：`ansible 主机名 -m yum -a "需要批量执行的命令"`
* 参数：
  * conf_file：设定远程yum执行时所依赖的yum配置文件
  * disable_gpg_check：选项（yes/no）；在安装包前检查包
  * list：只能由ansible调试、不能用于palybook
  * name：需要安装的安装包名字
  * state：选项（present（installed）、latest(安装升级)、absent）、描述安装包的最终状态；present、latest用于安装包、absent用于remove（卸载）安装包
  * update_cache：选项（yes/no），用于安装包执行更新list
* 示例
  * 安装python3.7、升级`ansible all -m yum -a "name=python3.7 state=latest"`

### Systemd模块

* 作用：对应service作用一样、管理服务状态
* 语法：`ansible 主机名 -m systemd -a "需要批量执行的命令"`
* 参数：
  * daemon_reload：在执行任何其他操作之前运行守护进程重新加载，以确保 systemd 己经读取其他更改
  * enabled：服务是否自启动（yes/no）
  * masked：是否将服务设置为masked状态、被masked的服务是无法启动的
  * name：服务名称
  * no_block（2.3后新增）：不要同步等待操作请求完成
  * state：对当前服务执行启动，停止、重启、重新加载等操作（started ， stopped, restarted, reloaded ）
  * user：使用服务的调用者运行 systemctl ，而不是系统的服务管理者
* 示例：
  * 设置nginx的启动、开机自启`ansible all -m systemd -a "name=nginx state=started enabled=yes"`

### Mount模块

* 作用：挂载文件系统、xfs、nfs、ext4
* 语法：`ansible 主机名 -m mount -a "需要批量执行的命令"`
* 参数：
  * path：挂载点
  * src：挂载设备
  * state：挂载动作
    * mounted挂载、写入fatab文件、创建挂载点
    * unmounted卸载挂载设备、不会删除/etc/fstab文件记录
    * present：只写入fstab文件不立即挂载
    * absent：删除/etc/fstab文件记录、卸载挂载设备
    * remounted：重新挂载设备
  * fstype：文件系统类型
* 示例：
  * 立即挂载`ansible all -m mount -a "src='24.34.123.125:/nfs-data' path='/test' fstype=ext4 state=mounted"`
  * 重启后开机自动挂载（修改etc/fstab）`ansible all -m mount -a "src='24.34.123.125:/nfs-data' path='/test' fstype=ext4 state=remounted"`

### Archive模块

* 作用：打包压缩、文件、文件夹tar
* 语法：`ansible 主机名 -m archive -a "需要批量执行的命令"`
* 参数：
  * dest：压缩文件存放路径
  * path：需要压缩文件路径
  * format：支持的压缩格式：bz2、gz、tar、xz、zip
* 示例：
  * 压缩文件`ansible 192.168.31.96 -m archive -a "path=/etc/ dest=/tec/etc.tar.gz format=tar"`

### unarchive模块

* 作用：拆包、解压缩untar
* 语法：`ansible 主机名 -m unarchive -a "需要批量执行的命令"`
* 参数：
  * dest：解压缩文件存放路径
  * src：需要解压缩文件路径
  * remote_src：文件是否远程
* 示例：
  * 解压文件（（远程机器）文件在本地、解压到本地）`ansible 192.168.31.96 -m unarchive -a "dest=/etc/ src=/tec/etc.tar.gz remote_src=yes"`
  * 解压文件（文件在本地、解压到远程）`ansible 192.168.31.96 -m unarchive -a "dest=/etc/ src=/tec/etc.tar.gz"`

## 剧本ansible-playbook

### yaml

```yaml
--- # 表示这是一个剧本
- name: # 剧本名称
  hosts: # 需要执行的机器
  remote_user: root # 使用远程主机上的 root 用户执行操作
  tasks:
   - name: jieya # 第一个任务
    ansible.builtin.unarchive # 使用的模块
      # 执行的参数操作
      
   - name: jieya # 第二个任务
    ansible.builtin.unarchive # 使用的模块
      # 执行的参数操作
--- # 第二个剧本（字典风格）
- name: # 剧本名称
  hosts: # 需要执行的机器
  remote_user: root # 使用远程主机上的 root 用户执行操作
  tasks:
    yum: # 模块名称
      # 执行的参数操作
```

1. 修改输出结果为json格式

   * 修改ansible配置文件`/etc/ansible/ansible.cfg`
   * 加入参数`stdout_callback = json、bin_ansible_callbacks = True`

2. 转换解压文件为yaml

   ```yaml
   ---
   - name: jieya
     hosts: all
     remote_user: root
     tasks:
       - name: jieya
         ansible.builtin.unarchive:
           dest: /etc/
           src: /tec/etc.tar.gz 
           remote_src: yes
   ```

3. 验证脚本`ansible-palybook -C 剧本名称.yaml`

4. 



### json



## 角色
