[toc]

# linux

## 初识Linux

### 初识

1. linux诞生

   * Linux 创始人 ： 林纳斯托瓦兹
   * Linux 诞生于 1991 年作者上大学期间
   * 因为创始人在上大学期间经常需要浏览新闻和处理邮件发现现有的操作系统不好用 ， 于是他决心自己写一个保护模式下的操作系统 ， 这就是 Linu × 的原型 ， 当时他 21 岁 ， 后来经过全世界网友的支持 ， 现在能够兼容多种硬件 ， 成为最为流行的服务器操作系统之一

2. 内核

   * Linu× 系统的组成如下 ：

     1. Linux 系统内核;系统级应用程序两部分组成 。

        ![image-20230625162205676](../typoratuxiang/linux/image-20230625162205676.png)

     2. 内核提供系统最核心的功能 ， 如 ： 调度 CPU 、 调度内存 、 调度文件系统 、 调度网络通讯 、 调度旧等 。

     3. 系统级应用程序 ， 可以理解为出厂自带程序 ， 可供用户快速上手操作系统 ， 如 ，文件管理器 、 任务管理器 、 图片查看 、 音乐播放等 。

3. 常见发行版本

   1. 可以看出 / 内核是 Linux 操作系统最核心的所在 ， 系统级应用程序只是锦上添花 。
      * Linux 内核是免费开源的 ， 任何人都可以下载内核源码并查看且修改 。
      * 可以通过 ： `https://www.kernel.org` 去下载 Linux内核
      
   2. 内核是免费 、 开源的 / 这也就代表了 ：
   
      * 任何人都可以获得并修改内核 / 并且自行集成系统级程序
      * 提供了内核 + 系统级程序的完整封装 / 称之为 Linu × 发行版
   
      ![image-20230628092337438](../typoratuxiang/linux/image-20230628092337438.png)

### 虚拟机

==借助虚拟化技术 , 我们可以在系统中 ,通过软件 ： 模拟计算机硬件 , 并给虚拟硬件安装真实的操作系统 。这样 , 就可以在电脑中 ,虚拟出一个完整的电脑以供我们学习 Linux系统 。==

1. **安装VMware WorkStation**

   * 下载地址 ： `https://www.vmware.com/cn/products/workstation-pro.html`

   * 打开网卡设置---`win+r`--->`ncpa.cpl`

2. **吏用 VMware 安装 Linux 虚拟机**
   *  Cent OS下载地址:`https://vault.centos.org/7.6.1810/isos/x86_64/CentOS-7-x86_64_DVD-1810.iso`

3. **远程链接Linux系统**

   1. 掌握操作系统的图形化 、 命令行 2 种操作模式
      1. 对于操作系统的使用 ， 有 2 种使用形式 ：
         * 图形化页面使用操作系统:使用操作系统提供的图形化页面 ， 以获得图形化反馈的形式去使用操作系统 。
         * 以命令的形式使用操作系统:使用操作系统提供的各类命令 / 以获得字符反馈的形式去使用操作系统 。
   2. 理解为什么使用命令行操作 Linux 系统
   3. 掌握使用 FinaISheII 软件连接 Linux 操作系统
      1. 下载finalshell并安装--安装依赖
      2. 输入`ifconfig`查看服务器ip
      3. `ip route`查看路由信息
      4. 点击finalshell的文件夹图标---点击代加号的白色文件夹---SSH链接（Linux），创建远程链接
      5. 输入名称---自取
      6. 输入IP---账号密码
   4. WSL(在win中的Linux系统)
      1. 点击`win`--`启用或关闭win功能`--勾选`适用于Linux的win子系统`---重新启动
      1. 然后在win上自带的应用商店获取Ubuntu
      1. 开启虚拟化
      1. 安装Terminal
      1. 查看虚拟架构`uname -m`
   5. 虚拟机快照

      1. 通过快照将当前虚拟机的状态保存下来，在以后可以通过快照恢复虚拟机到保存的状态

         * VMware Workstation 制作快照
           1. 确保虚拟机关机，找到快照管理器
           2. 找到虚拟机鼠标右击---快照---快照管理器---拍摄快照----给名字、描述---拍摄快照
         * VMware Fusion 制作快照
           1. 快照可以保存虚拟机的状态 ， 当虚拟机出现问题的时候 ， 可以通过预先制作的快照恢复到制作时候的状态用作备份用 。
           2. VMware Workstation 和 VMware Fusion 都支持制作快照去使用

4. **如何让局域网中的其他主机访问虚拟机**

   ==前提：==同一局域网主机1，主机2都为Windows系统，主机1上安装了VMware Workstation 14 Pro，并创建了一台虚拟机1，使用CentOS 7系统。

   1. 虚拟机1的网络适配器设置为NAT模式。

   2. 启动虚拟机1，用命令“ip addr”查看虚拟机的ip地址。

      1. 如果没有看到ip地址，则进入目录“cd /etc/sysconfig/network-scripts”，用命令“ls | grep 'ifcfg-*'”来找到配置文件ifcfg-ens33（这个名称不同的虚拟机不一样）。

      2. 编辑这个配置文件ifcfg-ens33，重点修改（增加）这两行：

         ```
         BOOTPROTO=dhcp
         ONBOOT=yes
         ```

      3. 用命令重启网络服务“service network restart”。再次用命令“ip addr”查看ip地址，可以看到虚拟机的ip.

   3. 可以通过ping命令，互相ping通主机1和虚拟机1，并且虚拟机1能ping通www.baidu.com。主机1也能访问虚拟机1的网页，但是主机2并不能访问到虚拟机1的网页。接下来打开VMware Workstation，从菜单栏中选择“编辑-->虚拟网络编辑器”,点击“更改设置”。

   4. 选中“VMnet8”——输入端口——类型选择TCP——输入虚拟机ip——输入端口“确定”

      1. 同一网络下两台==win==主机无法ping通：
         1. 第一步：启用规则
            1. 打开 **控制面板**，查看方式选择 **类别**，选择 **系统和安全**，选择 **Windows Defender 防火墙**打开左边的 **高级设置**，选择 **入站规则**，找到这两条规则，右键 **启用规则**（远程地址也就是作用域改为任何）
         2. 第二步：修改高级共享设置
            1. 打开 **控制面板**，查看方式选择 **类别**，选择 **网络和 Internet**，选择 **网络和共享中心**，打开左边的 **更改高级共享设置**，按图中选择：**启用网络发现** 和 **启用文件和打印机共享** 后点击下方的 **保存更改**

### 配置锁定IP

1. 配置桥接网络锁定IP

   1. 查询本地网卡配置信息

      ```
      ip addr
      ```

   2. 打开网卡配置文件

      ```
      vi /etc/sysconfig/network-scripts/ifcfg-ens160
      ```

   3. 需要修改的网卡配置

      ```
      BOOTPROTI=static
      ONBOOT=yes 
      ```

      - BOOTPROTI
         * dhcp: DHCP动态地址协议 。
         * static：静态地址协议。

      - ONBOOT
         * 系统启动时是否激活网卡接口，yes为激活，no为不激活。

   4. 添加的内容

      ```
      IPADDR=192.168.31.98                   #静态ip地址，需要确保在局域网中的唯一性,锁定的IP地址
      NETMASK=255.255.255.0                  #子网掩码
      GATEWAY=192.168.31.1                   #网关地址
      ```

   5. 配置公共 DNS 服务器

      ```
      vim /etc/resolv.conf
      nameserver 8.8.8.8
      nameserver 8.8.4.4
      ```

   6. 手动添加IP网关

      ```
      ip addr add 192.168.31.98/24 dev ens160
      ip route add default via 192.168.31.1
      
      删除指定IP
      sudo ip addr del 192.168.31.98/24 dev ens160
      ```

   7. 重启网络服务

      ```
      systemctl restart NetworkManager
      ```

   8. 遇到问题`Failed to start LSB: Bring up/down networking.`解决办法

      ```
      systemctl stop NetworkManager # 关闭网络管理
      systemctl disable NetworkManager # 禁用网络管理
      ```

   9. 重新启用 `NetworkManager`：

      ```bash
      # 启用服务
      systemctl enable NetworkManager
      # 启动服务
      systemctl start NetworkManager
      ```

   10. 查询`NetworkManager`网络状态

      ```
      systemctl status NetworkManager
      ```

   11. 手动开启（关闭）网络接口

      ```
      ip link set dev ens160 down     #（关闭）
      ip link set dev ens160 up       #（开启）
      ```

2. 配置数据源

   ```bash
   #查看本机yum数据源
   yum repolist
   #备份
   mv /etc/yum.repos.d/ /etc/yum.repos.d_bak 
   #创建新的 YUM 配置文件夹
   mkdir /etc/yum.repos.d/
   #下载阿里云的 CentOS 8.5.2111 镜像源配置文件
   wget -O /etc/yum.repos.d/CentOS-Base.repo https://mirrors.aliyun.com/repo/Centos-vault-8.5.2111.repo
   ```

3. 报错

   ```bash
   Errors during downloading metadata for repository 'appstream':
     - Curl error (6): Couldn't resolve host name for http://mirrorlist.centos.org/?release=8&arch=x86_64&repo=AppStream&infra=stock [Could not resolve host: mirrorlist.centos.org]
   Error: Failed to download metadata for repo 'appstream': Cannot prepare internal mirrorlist: Curl error (6): Couldn't resolve host name for http://mirrorlist.centos.org/?release=8&arch=x86_64&repo=AppStream&infra=stock [Could not resolve host: mirrorlist.centos.org]
   ```

   1. 测试 DNS 解析

      ```bash
      nslookup mirrors.aliyun.com
      # 或者
      dig mirrors.aliyun.com
      ```

   2. 在文件内配置网关(添加)

      ```bash
      nameserver 网关地址
      ```

**配置 Linux 固定 IP 地址**

* 在 VMware Workstation 中配置 Linux 系统的固定IP地址（用于 Windows 系统）
   1. 在 VMwa re W0rkstation （或 Fusion ）中配置IP地址网关和网段（IP地址的范围）
   2. 在 Linux系统中手动修改配置文件，固定IP
      1. 使用vim编辑==/etc/sysconfig/network-scripts/ifcfg-ens33==
      2. 修改`BOOTPROTO="static"`、`IPADDR="IP地址"`、`NETMASK="子网掩码255.255.255.0"`、`GATEWAY='网关与VM虚拟网络编辑器中一致'`、`DNS1='网关'`
      3. 网卡启停`systemctl start network`、`systemctl stop network`
* 在 VMware Fusion 中配置 Linux 系统的固定 IP 地址（用于 MacOS 系统）

## Linux基础命令

1. Linux目录结构

   1. 在 Linux 系统中 / 路径之间的层级关系 ， 使用 ： / 来表示
   2. 在 Windows 系统中 ， 路径之间的层级关系 ， 使用 ： \ 来表示

   1. 学习 Linux, 本质上是学习在命令行下熟练使用 Linux的各类命令 。

      * 命令行 ： 即 Linux 终端 (Terminal), 是一种命令提示符页面 。 以纯 “ 字符 “ 的形式操作系统 ， 可以使用各种字符化命令对系统发出操作指令 。
      * 命令 ： 即 Linux 程序 。 一个命令就是一个 Linux的程序 。 命令没有图形化页面 / 可以在命令行 （ 终端中 ） 提供字符化的反馈。

   2. Linux命令基础格式

      * 无论是什么命令 / 用于什么用途 ， 在 Linux 中，命令有其通用的格式 ：
        ==command [-options] [parameter]==

        * command: 命令本身
        * -options: [ 可选 ， 非必填 ] 命令的一些选项 ， 可以通过选项控制命令的行为细节
        * paramete: [ 可选 ， 非必填 ] 命令的参数 ， 多数用于命令的指向目标等
          ==语法中的[], 表示可选的意思==

      * 示例 ：

        * ls /home/itheima, [ s 是命令本身 ， 是选项 / /home/itheima 是参数
          ==意思是以列表的形式 ， 显示 /home/itheima 目录内的内容==

        * cp -r testl test2 , cp 是命令本身 ， -r 是选项 ， test1 和 test2 是参数

          ==意思是复制文件夹 test1 成为 test2==
      
   5. `命令 --help`：查看命令用法

### ls命令

1. ls 命令的作用是列出目录下的内容，语法细节如下 ：
2. `ls [-a -l -h] [Linux路径]`
3. -a -l -h是可选的选项
4. Linux 路径是此命可选的参数
==当不使用选项和参数，直接使用 ls 命令本体,表示 :以平铺形式,列出当前工作目录下的内容==
5. 头的文件或文件夹默认被隐藏 ，需一来彐选项 ， 以列表的形式展示内容 ， 并展示更多细节
6. 参数和选项
      1. 当 ls 不使用参数 , 表示列出 ： 当前工作目录的内容 ， 即用户的 HOME 目录
      2. 当使用参数 ， ls 命令的参数表示 ： 指定一个 Linu × 路径 , 列出指定路径的内容
      3. -a选顶表示 :all 的意思即列出全部文件 （ 包含隐藏的文件 / 文件夹 ）
         * 图中以`.`开头的表示是 Linux系统的隐藏文件 / 文件夹 （ 只要以 `.`开头,就能自动藏 ）
         * 只有通过 -a 选项 ， 才能看到这些喼藏的文件 / 文件夹
      4. -l 选项表示:以列表（ 竖向排列 ）的形式展示内容 / 并展示更多信息
         * -l选项其实和图形化中 / 文件夹以列表形式排列是一个意思
         * 给出了[权限--用户和用户组--大小--创建时间]
         * 语法中的选项是可以组合使用的 ， 比如学习的 -a 和 -l 可以组合应用
         * 写法 ：`ls -a`、`ls -la`、`ls -al`
         * 上述三种写法 ， 都是一样的 ， 表示同时应用-l 和-a的功能
      5. -h 表示以易于阅读的形式 ，列出文件大小 ，如 K 、 M 、 G
      6. -h 选项必须要`-l`搭配一起使用

### xargs 命令

`xargs`是一个在Linux和其他Unix-like系统中使用的命令行实用工具，它从标准输入读取数据，然后将这些数据转换成一个命令行参数列表，并执行指定的命令。

* `somecommand | xargs anothercommand`
* `somecommand`的输出会被`xargs`读取，并作为参数传递给`anothercommand`

### wc 命令

`wc` 命令在 Linux 和 Unix 系统中用于统计文件的行数、字数和字节数（或字符数）。

- **无选项**: 如果不使用任何选项，`wc` 会输出文件的行数、单词数、字节数（对于非二进制文件）以及文件名。
  
- **-l** 或 **--lines**: 统计指定文件的行数。

- **-w** 或 **--words**: 统计指定文件的单词数量。一个“单词”被定义为由空白字符分隔的字符串。

- **-c** 或 **--bytes**: 统计文件中的字节数。这通常等同于文件大小，但对于包含多字节字符的文件可能不是这样。

- **-m** 或 **--chars**: 统计字符数。与 `-c` 不同，此选项正确计算多字节字符。

- **-L** 或 **--max-line-length**: 打印最长的一行的长度。

使用示例：

1. 统计文件的行数：`wc -l filename`
2. 统计文件的单词数：`wc -w filename`
3. 统计文件的字节数：`wc -c filename`
4. 统计文件的字符数（适用于多字节字符）：`wc -m filename`
5. 统计文件的所有信息（行数、单词数、字节数/字符数）：`wc filename`

也可以同时使用多个选项，例如 `wc -lwm filename` 来同时获取行数、单词数和字符数。如果将标准输入（stdin）传递给 `wc`（例如通过管道），它会对从stdin读取的数据进行统计。例如，`cat filename | wc -l` 会统计文件的行数。

### nohub 命令

主要用于在用户退出终端之后继续运行指定的进程

语法`nohup command [arguments] & >dev/null`

* `command`: 您想要运行的命令。
* `[arguments]`: 传递给命令的参数（如果有的话）。
* `&`: 将命令放到后台执行。
* `>dev/null`将输出到命令行的打印，全部写进黑洞文件

### expr 计算表达式的命令行工具

* 数学运算

  ```bash
  # 加法、减法、乘法、除法和取模：
    expr 5 + 3    # 输出 8
    expr 10 - 2   # 输出 8
    expr 4 \* 5   # 注意乘法需要用反斜杠转义，输出 20
    expr 9 / 2    # 输出 4 (整数除法)
    expr 9 % 2    # 输出 1 (取模)
  ```

* 字符串操作

  ```bash
  # 获取字符串长度：
    expr length "hello world"    # 输出 11
  # 查找字符首次出现的位置：
    expr index "hello world" lo  # 输出 3 (从第一个'l'开始计数)
  # 提取子串：
    expr substr "hello world" 3 5    # 输出 'llo w'
  # 正则表达式匹配
  # 匹配以特定模式开头的字符串，并返回匹配部分：
    expr match "hello world" "hell.*"    # 输出 11 (匹配的字符串长度)
  ```

* 注意，在使用 `expr` 时，操作数与运算符之间必须有空格，否则会导致语法错误。此外，对于一些特殊字符（如乘号 `*`），需要使用反斜杠 `\` 进行转义。

### awk 命令

`awk` 能够对文本文件中的数据进行扫描、过滤、排序以及格式化输出等操作

- `-F 分隔符`：指定字段分隔符，默认为空格或制表符。
- `-v 变量=值`：定义变量并赋值。
- `-f 脚本文件`：从脚本文件中读取 `awk` 命令。
- 基本概念
  1. 字段
     * awk 将每一行按指定的分隔符分割成多个字段。
     * `$1` 表示第一个字段，`$2` 表示第二个字段，依此类推。
     * `$0` 表示整行内容。
  2. 内置变量
     * NF：当前行的字段数（Number of Fields）。
     * NR：当前行号（Number of Records）。
     * FS：字段分隔符（Field Separator），默认为空格。
     * OFS：输出字段分隔符（Output Field Separator），默认为空格。
     * RS：记录分隔符（Record Separator），默认为换行符。
     * ORS：输出记录分隔符（Output Record Separator），默认为换行符。

### cd-pwd命令

1. 我们可以通过cd命令,更改当前所在的工作目录 。
     * cd 命令来自英文 ： change Directory
             `语法 ：cd [Linux 路径 ]`
     * cd 命令无需选项 ， 只有参数 ， 表示要切换到哪个目录下
     * cd 命令直接执行 ， 不写参数 ， 表示回到用户的 HOME 目录
2. 我们可以通过 pwd 命令 ， 来查看当前所在的工作目录 。
     * pwd 命令来自 ： Print Work Di rectory
              `语法 ： pwd`
     * pwd 命令 ， 无选顶 ， 无参数 ， 直接输入 pwd 即可

### 相对路径、绝对路径和特殊路径

1. 绝对路径 ： 以根目录为起点 ， 描述路径的一种写法 ， 路径描述以 / 开头
2. 相对路径 ： 以为起点 ， 描述路径的一种写法 ， 路径描述无需以 / 开头
3. 特殊路径符
     * `.`     表示当前目录 ， 比如 `cd ./Desktop` 表示切换到当前目录下的 Desktop 目录内 ， 和 cd Desktop 效果一   
     *  `..`   表示上一级目录 / 比如 ： `cd..`即可切换到上一级目录 / cd “ / “ 切换到上二级的目录
     *  `~`     表示 HOME 目录 / 比如 ： `cd~` 即可切换到 HOME 目录或 cd /Desktop, 切换到 HOME 内的 Desktop 目录

### 创建目录命令（mkdir）

1. 通过 mkdir 命令可以创建新的目录 （ 文件夹 ）
     * mkdir 来自英文 ： Make Directory
     * 语法 ：`mkdir [-p] Linnux路径`
       * 参数==必填==，表示 Linux 路径，即要创建的文件夹的路径 ， 相对路径或绝对路径均可
       * `-m, --mode=MODE`：设置目录的权限模式，不需要再使用 `chmod` 命令来更改权限。
       * `-p, --parents`：如果需要创建的目录的父目录不存在，则会一并创建所有必要的父目录。
       * `-v, --verbose`：输出每个创建的目录的信息。

### 文件操作命令part1(touch、cat、more、tail)

1. touch创建文件
          1. 可以通过 touch 命令创建文件
      
      * 语法：`touch Linux路径`
      * touch 命令无选项，参数必填，表示要创建的文件路径，相对、绝对、特殊路径符均可以使用
      
2. cat、more查看文件内容
     1. 准备好文件内容后，可以通过 cat 查看内容 。
                 1. 语法 ： `cat Linux路径`
                    * cat 同样没有选项，只有必填参数，参数表示：被查看的文件路径，相对、绝对、特殊路径符都可以使用
             
     1. more 命令同样可以查看文件内容，同 cat 不同的是 ：
        
         * cat 是直接将内容全部显示出来
         
         * more 支持翻页 ， 如果文件内容过多 ， 可以一页页的展示
         
           语法 ：`more Linux路径`
         
         * 同样没有选项 ， 只有必填参数，参数表示，被查看的文件路径，相对 、 绝对 、 特殊路径符都可以使用
         
         * 在查看的过程中 ， 通过空格翻页
         
         * 通过 q 退出查看

3. tail查看文件末尾内容

     * 语法`tail 选项 文件`
     * `-n` NUM 或 -NUM显示文件的最后 NUM 行
     * `-c`NUM显示文件的最后 NUM 字节
     * `-f`实时监控文件的变化，显示新添加的内容
     * `--follow=name`即使文件被删除或重命名，也继续监控同名的新文件
     * `--follow=descriptor`只监控当前打开的文件描述符，不跟踪新文件
     * `-q`不显示文件名前缀（适用于多个文件）
     * `-v`总是显示文件名前缀（即使只有一个文件）

### cp--mv--rm

1. cp 命令可以用于复制文件\文件夹,cp 命令来自英文单词：copy
   * 语法：`cp [-r] 参数1 参数2`
     
     ```bash
     cp [选项] 源文件 目标文件
     cp [选项] 源文件... 目录
     ```
     
     * -r 选顶，可选，用于复制文件夹使用，表示递归
        - `-i` 或 `--interactive`：在覆盖现有文件之前提示用户确认。
        - `-f` 或 `--force`：如果目标文件已经存在，则强制覆盖而不提示。
        - `-p` 或 `--preserve`：保留文件属性，如修改时间、访问时间和权限。
        - `-r` 或 `-R` 或 `--recursive`：递归地复制整个目录及其内容。
        - `-v` 或 `--verbose`：详细模式，显示正在复制的文件信息。
        - `-a` 或 `--archive`：归档模式，相当于 `-dR --preserve=all`，用于备份或镜像目录树。
        - `-l` 或 `--link`：不复制文件，而是创建硬链接。
        - `-s` 或 `--symbolic-link`：不复制文件，而是创建符号链接。
     * 参数1,Linux 路 径， 表示被复制的文件或文件夹
     * 参数2,Linux 路径，表示要复制去的地方
   
  2. mv命令可以用于移动文件或文件夹 ，mv 命令来自英文单词：move，`mv` 命令不会复制文件的内容，而是直接改变文件的位置或名称
     * 语法：`mv 参数1 参数2`
       
       ```
       mv [选项] 源文件 目标文件
       mv [选项] 源文件... 目录
       ```
       
       * 如果提供了两个文件名（源文件和目标文件），`mv` 会将源文件移动到目标位置，并且如果目标是一个不同的文件名，则相当于给文件重命名。
       * 如果提供了一个或多个文件名和一个目录，`mv` 会将这些文件移动到指定的目录中。
       * **常用选项**
          - `-i` 或 `--interactive`：在覆盖现有文件之前提示用户确认。
          - `-f` 或 `--force`：如果目标文件已经存在，则强制覆盖而不提示（默认行为）。
          - `-n` 或 `--no-clobber`：不覆盖已存在的文件。
          - `-v` 或 `--verbose`：详细模式，显示正在移动的文件信息。
          - `-u` 或 `--update`：仅在源文件比目标文件新，或者目标文件不存在时才移动。
          - `-b` 或 `--backup`：在覆盖文件前进行备份，默认使用简单备份方法。
          - `--suffix=SUFFIX`：与 `-b` 一起使用，指定备份文件的后缀。
          - `--strip-trailing-slashes`：从每个源参数中去掉任何结尾的斜杠。
          - `-T` 或 `--no-target-directory`：将目标视为普通文件，即使它是一个目录。
     
  3. rm 命令可用于删除文件、文件夹，rm 命令来自英文单词：remove
     * 语法：`rm [-r -f] 参数1 参数2......参数n`
       * 同cp命令一样，-r 选顶用于删除文件夹
       * -f 表示 force, 强制删除（不会弹出提示确认信息）
       * 普通用户删除内宕不会弹出提示，只有 root 管理员用户删除内容会有提示
       * 所以一般普通用户用不到-f 选顶
      * 参数 1 、参数 2 、......参数 N 表示要删除的文件或文件夹路按照空格隔开
      * rm 命令支持通配`*`符用来做模糊匹配
        * 符号`*`表示通配符，即匹配任意内容（包含空），示例:
        * test`* `,表示匹配任何以test开头的内容
        * `*`test,表示匹配任何以test结尾的内容
        * `*`test`*`表示匹配任何包含test 的内容
        * `-f, --force`：强制删除文件，忽略不存在的文件，不提示确认。
        * `-i, --interactive`：在每个删除操作前提示用户确认。
        * `-r, -R, --recursive`：递归地删除目录及其内容。
        * `-v, --verbose`：显示详细的删除过程信息。
        * `--preserve-root`：防止递归删除 `/` 根目录（这是许多 Linux 发行版的默认行为）。

### which--find

1. which:我们可以通过which命令，查看所使用的一系列命令的程序文件存放在哪里
   
    * 语法：`which 要查找的命令`
1. find 在Linux系统中我们可以通过 find 命令去搜索指定的文件。
   
    * 语法：`find 起始路径 -name "查找文件名"`
      * find 命令-按文件大小查找文件
      * 语法：`find 起始路径 -size + l-n[kMG]`
      *  +、-表示大于和小于
      * n表示大小数字
      * kMG 表示大小单位，k(小写字母）表kb,M表示mb,G 表示 GB
    
       * `-name`
          * `-name` 是一个测试选项，用于根据文件名模式来查找文件。它允许用户指定一个文件名模板（支持通配符），`find` 会尝试匹配给定路径下的文件名与此模板。
          * `find [路径] -name "模式"`
          * **路径**：指定从哪个目录开始搜索。如果省略，则默认为当前目录。
          * **模式**：要匹配的文件名模式。可以包含通配符如 `*` 和 `?`。
       * `-type`：`-type [文件类型]`
          * `-type` 是一个选项，用于根据文件类型来过滤搜索结果。通过指定 `-type` 后跟一个指示符，可以限定 `find` 命令只查找特定类型的文件系统对象（如普通文件、目录等）
          * **`f`**：普通文件。
          * **`d`**：目录。
          * **`l`**：符号链接。
          * **`c`**：字符设备文件。
          * **`b`**：块设备文件。
          * **`p`**：命名管道（FIFO）。
          * **`s`**：套接字。
       * `-mtime`:` -mtime [n]`
          * `-mtime` 是一个用于根据文件的修改时间来搜索文件的测试选项。它允许用户指定一个天数
          * **`n`**：正好 n 天前修改的文件。
          * **`-n`**：在过去 n 天内（包括第 n 天）修改的文件。
          * **`+n`**：超过 n 天前修改的文件。

### grep--wc管道符

1. 可以通过 grep 命令，从文件中通过关键字过滤文件行。

     * 语法： `grep [-n ] 关键字 文件路径` 
       * 选项`-n` 可选，表示在结果中显示匹配的行的行号。
       * 参数，关键字，必填，表示过滤的关腱字，带有空格或其它特殊符号，建议使用`“ ”`将关键字包围起来
       * 参数，文件路径，必填，表示要过滤内容的文件路径，==可作为内容输入端口==

2. 可以通过 wc命令统计文件的行数、单词数量等
     * 语法：`wc [-c -m -l -w]文件路径`
       * 选项， -c, 统计 bytes 数量
       * 选项， -m, 统计字符数量
       * 选项，-l,统计行数
       * 选项， -w, 统计单词数量
       * 参数文件路径，被统计的文件,可作为内容输入端口

3. 学习了 grep 命令后，我们在来学习一个新的特殊符号，管道符：`|`管道符的含义是：将管道符左边命令的结果，作为右边命令的输入

### echo--tail重定向符

 1. 掌握使用echo命令输出内容
            * 可以使用 echo 命令在命令行内输出指定内容
            * 语法： `echo 输出内容`
              * 无需选项，只有一个参数,表示要输出的内容，复杂内容可以用`““`包围
 1. 掌拥反引号的使用
         * 我们可以通过将命令用反引号（通常也称之为飘号）、将其包围被包围的内容，会被作为命令执行，而非普通字符
 3. 掌握tail命令跟踪文件更改
       * 使用 tail命令，可以查看文件尾部内容，跟踪文件的最新更改，
       * 语法：`tail [-f -num] Linux路径`
         * 参数，Linux路径，表示被跟踪的文件路径选项
         * 选项，`-f`表示持续跟踪
         * 选项，`-num`, 表示，查看尾部多少行，不填默认10行
 4. 掌握重定向符号的使用
       * 重定向符：`>`和`>>`
         * `>`将左侧命令的结果，==覆盖==写入到符号右侧指定的文件夹中
         * `>>`将左侧命令的结果，==追加==写入到符号右侧指定的文件夹中

### vi编辑器

1. vi\vim是 visual interface 的简称，是 Linux中最经典的文本编辑器,同图形化界面中的文本编辑器一样， vi 是命令行下对文本文件进行编辑的绝佳选择。vim 是 vi 的加强版本，兼容 vi 的所有指令，不仅能编辑文本，而且还具有 shell 程序编辑的功能，可以不同颜色的字体来辨别语法的正确性，极大方便了程序的设计和编辑性。

2. `vi\vim`编辑器的三种工作模式

      * 命令模式 (Command mode)

        * 命令模式下，所敲的按键编辑器都理解为命令，以命令驱动执行不同的功能。此模型下，不能自由进行文本编辑。
        * 如果需要通过 vi / vim 编辑器编辑文件，请通过如下命令：vim 而兼容全部的 vi 功能，后续全部使用 vim 命令
        * `vi 文件路径\vim 文件路径`
          * 如果文件路径表示的文件不存在，那么此命令会用于编辑新文件
          * 如果文件路径表示的文件存在，那么此命令用于编辑已有文件

      * 输入模式 (lnsert mode)

        * 也就是所渭的编辑模式、插入模式。此模式下，可以对文件内容进行自由编辑。

      * 底线命令模式（ Last line mode)以：

        * 开始，通常用于文件的保存、退出。
        
        ![image-20240327161655843](../typoratuxiang/linux/vigzms.png)

3. 通过 `vi/vim` 命令编辑文件，会打开一个新的窗口，此时这个窗口就是：命令模式窗口，命令模式是 vi 编辑器的入口和出口，

      * 进入vi 编辑器会进入命令模式

      * 通过命令模式输入键盘指令，可以进入输入模式输入模式

      * 需要退回到命令模式，然后通过命令可以进入底线命令模

        |     模式     |      命令      |                描述                 |
        | :----------: | :------------: | :---------------------------------: |
        |   命令模式   |     ==i==      |   在当前光标位置进入==输入模式==    |
        |   命令模式   |     ==a==      | 在当前光标位置之后进入==输入模式==  |
        |   命令模式   |     ==I==      |   在当前行的开头进入==输入模式==    |
        |   命令模式   |     ==A==      |   在当前行的结尾进入==输入模式==    |
        |   命令模式   |     ==o==      |  在当前光标下一行进入==输入模式==   |
        |   命令模式   |     ==O==      |  在当前光标上一行进入==输入模式==   |
        |   输入模式   |    ==esc==     | 任何情况下输入`esc`都能回到命令模式 |
        | 底线命令模式 |    ==:wq==     |             保存并退出              |
        | 底线命令模式 |     ==:q==     |               仅退出                |
        | 底线命令模式 |    ==:q!==     |              强制退出               |
        | 底线命令模式 |     ==:w==     |               仅保存                |
        | 底线命令模式 |  ==:set nu==   |              显示行号               |
        | 底线命令模式 | ==:set paste== |            设置粘贴模式             |

### sed

1. 基本语法

   ````bash
   sed [选项] '指令' 文件名
   ````

- **选项**：

  - `-n`：禁止自动打印模式空间的内容。
  - `-e`：允许多个编辑指令。
  - `-i`：直接修改文件内容（原地编辑）。
  - `-r`：启用扩展正则表达式（GNU sed）。

- 指令

  ```bash
  sed '2,5d' file.txt  # 删除第2到第5行
  ```

  **(1) 替换文本**

  使用 `s` 命令替换文本：
  ```bash
  sed 's/旧字符串/新字符串/' 文件名
  ```
  - 默认只替换每行的第一个匹配项。
  - 如果需要全局替换，添加 `g` 标志：
    ```bash
    sed 's/旧字符串/新字符串/g' 文件名
    ```

  示例：
  ```bash
  echo "hello world" | sed 's/world/universe/'
  # 输出：hello universe
  ```

  **(2) 删除行**

  使用 `d` 命令删除指定行或行范围：
  ```bash
  sed '2d' 文件名        # 删除第2行
  sed '2,5d' 文件名      # 删除第2到第5行
  sed '/pattern/d' 文件名 # 删除包含特定模式的行
  ```

  示例：
  ```bash
  echo -e "line1\nline2\nline3" | sed '2d'
  # 输出：
  # line1
  # line3
  ```

  **(3) 插入和追加文本**

  - 使用 `i` 命令在某行之前插入文本：
    ```bash
    sed '2i 新内容' 文件名
    ```
  - 使用 `a` 命令在某行之后追加文本：
    ```bash
    sed '2a 新内容' 文件名
    ```

  示例：
  ```bash
  echo -e "line1\nline2\nline3" | sed '2a inserted line'
  # 输出：
  # line1
  # line2
  # inserted line
  # line3
  ```

  **(4) 打印特定行**

  使用 `p` 命令打印特定行：
  ```bash
  sed -n '2p' 文件名       # 只打印第2行
  sed -n '2,5p' 文件名     # 打印第2到第5行
  sed -n '/pattern/p' 文件名 # 打印匹配模式的行
  ```

  示例：
  ```bash
  echo -e "line1\nline2\nline3" | sed -n '2p'
  # 输出：
  # line2
  ```

  **(5) 修改文本**

  使用 `c` 命令替换整行：
  ```bash
  sed '2c 新内容' 文件名
  ```

  示例：
  ```bash
  echo -e "line1\nline2\nline3" | sed '2c replaced line'
  # 输出：
  # line1
  # replaced line
  # line3
  ```

  ---

  **3. 地址范围**

  `sed` 支持通过行号或模式指定地址范围：
  - 行号范围：`2,5` 表示第2到第5行。
  - 模式范围：`/start/,/end/` 表示从匹配 `start` 的行到匹配 `end` 的行。

  示例：
  ```bash
  sed '/start/,/end/d' 文件名  # 删除从匹配 "start" 到 "end" 的所有行
  ```

  ---

  **4. 正则表达式**

  `sed` 支持基本正则表达式（BRE），也可以使用扩展正则表达式（ERE）：
  - 基本正则表达式示例：
    ```bash
    sed 's/[0-9]\+/NUM/g' 文件名
    ```
  - 扩展正则表达式（使用 `-r` 选项）：
    ```bash
    sed -r 's/[0-9]+/NUM/g' 文件名
    ```

  ---

  **5. 示例**

  **(1) 替换文件中的内容并保存**

  ```bash
  sed -i 's/foo/bar/g' file.txt
  ```
  此命令会直接修改 `file.txt` 文件，将所有的 `foo` 替换为 `bar`。

  **(2) 删除空白行**

  ```bash
  sed '/^$/d' 文件名
  ```

  **(3) 提取特定字段**

  结合正则表达式提取字段：
  ```bash
  echo "Name: John Doe, Age: 30" | sed 's/.*Name: \(.*\), Age:.*/\1/'
  # 输出：John Doe
  ```

  ---

  **6. 注意事项**

  - `sed` 是基于行的处理工具，默认不会修改原始文件，除非使用 `-i` 选项。
  - 复杂的文本处理任务可以结合 `awk` 或其他工具完成。

  通过熟练掌握 `sed`，可以高效地处理各种文本数据，尤其是在脚本中自动化文本操作时非常有用！

### info

`info` 命令是 Linux 系统中的一个文档查看工具，用于显示 GNU 项目提供的信息页面（info pages）。这些信息页面通常比 `man` 页面更详细，包含更多的背景信息和使用示例。`info` 命令主要用于浏览 GNU 软件的手册和文档。

* ==使用 `info` 命令的基本语法==

  ```bash
  info [选项] [主题]
  ```

* **`主题`**：你想要查看的命令或程序的名称。例如，`info tar` 会显示 `tar` 命令的信息页面。

- **`选项`**：可以指定一些选项来控制 `info` 的行为。

==常用选项==

- **`-f, --file=文件名`**：指定要查看的信息文件。默认情况下，`info` 会在标准路径中查找信息文件，但你可以通过这个选项指定一个特定的文件。
  
  ```bash
  info -f /usr/share/info/tar.info
  ```

- **`-n, --node=节点名`**：直接跳转到指定的节点（章节）。信息页面通常由多个节点组成，每个节点类似于一本书中的章节。

  ```bash
  info -n 'Top'
  ```

- **`-w, --where`**：显示某个主题的信息文件位置，而不打开它。

  ```bash
  info -w tar
  ```

- **`--help`**：显示 `info` 命令的帮助信息。

  ```bash
  info --help
  ```

- **`--version`**：显示 `info` 命令的版本信息。

  ```bash
  info --version
  ```

==浏览信息页面==

当你运行 `info` 命令后，会进入一个类似终端文本浏览器的界面，允许你导航和搜索信息页面。以下是一些常用的键盘快捷键：

- **`Space`**：向下滚动一页。
- **`b`**：返回到上一页。
- **`n`**：跳转到下一个节点（章节）。
- **`p`**：跳转到上一个节点（章节）。
- **`q`**：退出 `info` 浏览器。
- **`?`**：显示帮助信息，列出所有可用的快捷键。
- **`/`**：进行全文搜索。输入搜索词后按 `Enter`，然后按 `n` 或 `N` 来查找下一个或上一个匹配项。
- **`g`**：跳转到指定的节点或文件。例如，`g Top` 会跳转到顶级节点。

==示例==

1. **查看 `tar` 命令的信息页面**：
   ```bash
   info tar
   ```

2. **查看 `gcc` 编译器的信息页面，并直接跳转到 "Invoking GCC" 节点**：
   ```bash
   info -n 'Invoking GCC' gcc
   ```

3. **查找 `grep` 命令的信息文件位置**：
   ```bash
   info -w grep
   ```

4. **查看 `info` 命令的帮助信息**：
   ```bash
   info --help
   ```

5. **查看 `info` 命令的版本信息**：
   ```bash
   info --version
   ```

==`info` 与 `man` 的区别==

- **`man` 页面**：通常提供简洁的、面向用户的命令行工具和系统调用的参考手册。适合快速查找命令的用法和选项。
- **`info` 页面**：通常更详细，包含更多的背景信息、示例和解释。适合深入学习和理解软件的功能和工作原理。

### crontab命令

* `crontab` 命令用于在 Unix、Linux 和其他类 Unix 操作系统中安排定时任务。通过 `crontab`，用户可以设置命令或脚本在特定的时间间隔自动执行。

  * 查看当前登录用户的定时任务列表`crontab -l`
  * 编辑当前用户的定时任务`crontab -e`
  * 删除当前用户的所有定时任务`crontab -r`

* Crontab 时间格式

  ```bash
  * * * * *
  | | | | |
  | | | | +--- 星期几 (0 - 7) (星期天=0或7)
  | | | +----- 月份 (1 - 12)
  | | +------- 日期 (1 - 31)
  | +--------- 小时 (0 - 23)
  +----------- 分钟 (0 - 59)
  ```

* `&>/dev/null`: 这一部分负责处理命令的输出。

  - `&>` 是一个简写形式，意味着同时重定向标准输出(stdout)和标准错误(stderr)。
  - `/dev/null` 是一个特殊的文件，用于丢弃所有写入它的数据。当输出被重定向到这里时，就等于不保留任何输出信息。

### 其他

1. 在Linux系统中想要查看本机IP地址、显示网络接口的详细信息，包括IP地址。`ifconfig`

2. 使用ip命令：这将显示网络接口的详细信息，包括IP地址。`ip addr show`

3. 使用hostname命令：这将显示本机的所有IP地址。`hostname -I`

4. 使用curl命令：这将使用curl命令从ifconfig.me网站获取本机的公共IP地址。`curl ifconfig.me`

5. service sshd restart重启sshd服务

6. free:查看内存占用情况

7. 反引号：取出命令的执行结果

   ```
   echo `docker image -ag`
   ```

8. `dmesg`查看所有硬件信息

   * `dmesg |grep -i eth(网卡)`:查看网卡信息
   * `ethtool -i eth网卡`:查看网卡信息
   * `modprobe -r 驱动名称`:卸载驱动
   * `modprobe  驱动名称`:加载驱动

9. 查看文件信息`stat 文件`

### linux版本相关

* 查看centos发行版版本`cat /etc/redhat-release`
* 查看ubuntu发行版版本`cat /etc/os-release`
* 查看linux内核版本`uname -r`

## Linux权限管理

### Linux的root用户

1. 无论是 Windows 、 MacOS 、 Linux均采用多用户的管理模式进行权限管理。
   * 在 Linux 系统中事拥有最大权限的账户名为： root （超级管理员）
   * root 用户拥有最大的系统操作权限，而普通用户在许多地方的权限是受限的
   * 普通用户的权限，一般在其 HOME 目录内是不受限的
   * 一旦出了 HOME 目录，大多数地方，普通用户仅有只读和执行权限，无修改权限
2. su 命令就是用于账户切换的系统命令其来源英文单词： Switch User
   * 语法： `su [-] [用户名]`
   * `-`符号是可选的，表示是否在切换用户后加载环境变量（后续讲解 ), 建议带上
   * 参数：用户名，表示要切换的用户，用户名也可以省略，省略表示切换到==root==
   * 切换用户后，可以通过 ==exit== 命令退回上一个用户，也可以使用快捷键：`ctrl+d`
   * 使用普通用户，切换到其它用户需要输入密码，如切换到 root 用户
   * 使用 root 用户切换到其它用户,无需密码,可以直接切换
   * 可以通过 su -root, 并输入密码
   * 通过输入exit命令退回普通用户。
3. 我们可以使用sudo命令，为普通的命令授权，临时以 root 身份执行。
   * 语法： `sudo 其它命令`
   * 在其它命令之前，带上sudo, 即可为这一条命令临时赋予 root 授权
   * 但是并不是所有的用户，都有权利使用`sudo`我们需要为普通用户配置 sudo 认证
     * 为普通用户配置 sudo 认证
       1. 切换到 root 用户，执行 visudo 命令，会自动通过 vi 编辑器打开： `/etc/sudoers`
       2. 在文件的最后添加：`普通用户名 ALL=(ALL)  NOPASSWD:ALL`
       3. 其中最后的 NOPASSWD:ALL 表示使用 sudo 命令无需输入密码最后通过 wq 保存

### 用户和用户组

1. 用户、用户组的概念
   * Linux系统中可以：==配置多个用户、配置多个用户组、用户可以加入多个用户组中==
   * Linux中关于权限的管控级别有 2 个级别，分别是：==针对用户的权限控制、针对用户组的权限控制==
2. 用户、用户组管理的相关命令==以下命令需 root 用户执行==
   * 用户组管理
     1. 创建用户组`groupadd 用户组名`
     2. 删除用户组`groupdel 用户组名`
   * 用户管理
     1. 创建用户`useradd [-g -d] 用户名`
        * 选项：`-g`指定用户的组，不指定`-g`，会创建同名组并自动加入，指定`-g`需要组己经存在，如己存在同名组，必须使用`-g`
        * 选项：`-d`指定用户 HOME 路径，不指定，HOME 目录默认在： /home/ 用户名
     2. 删除用户`userdel [-r] 用户名`
        * 选项： `-r` ，删除用户的 HOME 目录，不使用`-r` ，删除用户时， HOME 目录保留
     3. 查看用户所属组`id [用户名]`
        * 参数：用户名，被查看的用户，如果不提供则查看自身
     4. 修改用户所属组`usermod -aG 用户组 用户名`
        * 将指定用户加入指定用户组
   * 使用 getent 命令，可以查看当前系统中有哪些用户语法：` getent passwd`
     * 共有 7 份信息，分别是：用户名：密码（×）：用户旧：组旧：描述信息（无用）： HOME 目录：执行终端（默认 bash ）
   * 使用 getent 命令，同样可以查看当前系统中有哪些用户组语法:`getent group`
     * 包含 3 份信息，组名称：组认证（显示为x）：组ID

### 查看权限控制信息

1. 查看 Linux 文件的权限管控信息

   * 通过`ls -l`可以以列表形式查看内容，并显示权限细节

     ![image-20240328010905399](../typoratuxiang/linux/xinxi.png)

   * 序号 1, 表示文件、文件夹的权限控制信息

     1. 序号 1, 权限细节

     2. 权限细节总共分为] 0 个槽位

        ![image-20240328011224665](../typoratuxiang/linux/chaoweixijie.png)

     3. 举例：`drwxr-xr-x`, 表示：

        * 这是一个文件夹，首字母 d 表示
        * 所属用户（右上角图序号 2 ）的权限是：有 r 有 w 有 x, rwx
        * 所属用户组（右上角图序号 3 ）的权限是：有 r 无 w 有 r-x （-表示无此权限）
        * 其它用户的权限是：有 r 无有 x ， r-x

   * 序号 2,表示文件、文件夹所属用户

   * 序号 3 ，表示文件、文件夹所属用户组

2. 读、写、执行三种权限的含义

   1. `RWX`
      * r 表示读权限
        1. 针对文件可以查看文件内容
        2. 针对文件夹，可以查看文件夹内容，如 ls 命令
      * w 表示写权限 
        1. 针对文件表示可以修改此文件
        2. 针对文件夹，可以在文件夹内：创建、删除、改名等操作
      * x 表示执行权
        1. 针对文件表示可以将文件作为程序执行
        2. 针对文件夹，表示可以更改工作目录到此文件夹，即 cd 进入

#### chmod命令

1. 使用 chmod 修改权限信息

   * 我们可以使用 chmod 命令，修改文件、文件夹的权限信息。==注意，只有文件、文件夹的所属用户或 root 用户可以修改==
   * 语法：` chmod [-R] 权限 文件或文件夹`
     * 选项：`-R`对文件夹内的全部内容应用同样的操作
     * `-R, --recursive`：递归地更改指定目录及其子目录和文件的权限。
     * `-v, --verbose`：显示详细的权限更改信息。
     * `-c, --changes`：像 `--verbose` 一样，但只显示实际上改变了的文件。
     * `--reference=ref_file`：将文件的权限设置为与 `ref_file` 相同。
   * 示例：·`chmod u=rwx,g=rx,o=x hello.txt`, 将文件权限修改为:`rwxr-x--x`
   * 其中： u 表示 user 所属用户权限， g 表示 group 组权限， 0 表示 other 其它用户权限

2. 使用数字序号标记权限

   * 权限可以用 3 位数字来代表，第一位数字表示用户权限，第二位表示用户组权限，第三位表示其它用户权限。

   * 数字的细节如下： 读（read）、写（write）、执行（execute）

     | 0    | 无任伺权限 | `---` |
     | ---- | ---------- | ----- |
     | 1    | 仅有×权限  | `--x` |
     | 2    | 仅有w权限  | `-w-` |
     | 3    | 有w和×权限 | `-wx` |
     | 4    | 仅有r权限  | `r--` |
     | 5    | 有r和×权限 | `r-x` |
     | 6    | 有r和w权限 | `rw-` |
     | 7    | 有全部权限 | `rwx` |

#### chown命令

* 使用 chown 命令，可以修改文件、文件夹的所属用户和用户组==普通用户无法修改所属为其它用户或组，所以此命令只适用于 root 用户执行==
* 语法：`chown [-R ][用户][:][用户组]文件或文件夹`
  * 选顶， -R, 同chmod, 对文件夹内全部内容应用相同规则
  * 选项，用户，修改所属用户
  * 选项，用户组，修改所属用户组
  * `：`用于分隔用户和用户组

### ssh密钥

使用ssh远程，无密码方式（免密码登录）

1. 在本机上生成目录`.ssh`：`ssh-keygen -t rsa`
2. 上传公钥到目标机器（需要远程到的机器）`ssh-copy-id root@192.168.157.146`
3. 重启 SSH服务命令使其生效`service sshd restart`

### 日志

==在 Linux 系统中，日志记录是系统管理和故障排除的重要组成部分。Linux 系统使用各种日志文件和工具来记录系统的活动、应用程序的行为以及用户的操作。以下是一些常见的日志文件位置和查看日志的命令。==

#### 常见的日志文件

1. **系统日志 (System Log)**
   - 位置：`/var/log/secure` 
   - 内容：包括启动过程中的信息、内核消息、服务启动/停止消息等。
   
2. **认证日志 (Authentication Log)**
   - 位置：`/var/log/auth.log` 或 `/var/log/secure`（取决于发行版）
   - 内容：包含用户登录尝试、权限更改等与安全相关的事件。

3. **守护进程日志 (Daemon Log)**
   - 位置：`/var/log/daemon.log`
   - 内容：特定于守护进程的日志信息。

4. **邮件日志 (Mail Log)**
   - 位置：`/var/log/mail.log` 或 `/var/log/maillog`
   - 内容：与邮件服务器相关的信息。

5. **包管理器日志 (Package Manager Log)**
   - 位置：`/var/log/dpkg.log` (Debian/Ubuntu) 或 `/var/log/yum.log` (RHEL/CentOS)
   - 内容：记录了通过包管理器安装、更新或删除软件包的历史。

6. **引导日志 (Boot Log)**
   - 位置：`/var/log/boot.log` 或者可以通过 `dmesg` 命令查看
   - 内容：记录系统启动时的信息。

7. **Apache 日志 (对于 Apache Web 服务器)**
   - 位置：通常位于 `/var/log/apache2/` 或 `/var/log/httpd/`
   - 内容：访问日志 (`access.log`) 和错误日志 (`error.log`)。

8. **MySQL/MariaDB 日志 (对于 MySQL/MariaDB 数据库)**
   - 位置：通常位于 `/var/log/mysql/` 或 `/var/log/mariadb/`
   - 内容：查询日志、慢查询日志、错误日志等。

9. **X Window System 日志 (对于图形界面)**
   - 位置：`/var/log/Xorg.0.log`
   - 内容：图形界面启动时的日志信息。

#### 查看日志的命令

1. **`cat`**：用于显示整个文件的内容。
   ```bash
   cat /var/log/syslog
   ```

2. **`less`**：分页查看大文件，并允许向前和向后滚动。
   ```bash
   less /var/log/syslog
   ```

3. **`tail`**：显示文件的最后几行，常用于实时监控日志文件。
   ```bash
   tail -f /var/log/syslog
   ```
   使用 `-n` 选项可以指定显示的行数，例如 `tail -n 50 /var/log/syslog` 显示最后50行。

4. **`grep`**：用于搜索日志文件中的特定模式或关键字。
   ```bash
   grep "ERROR" /var/log/syslog
   ```

5. **`journalctl`**：对于使用 systemd 的系统，`journalctl` 是一个强大的工具，可以用来查看系统日志和服务日志。
   
   ```bash
   # 查看所有日志：
   journalctl
   # 查看特定服务的日志：
   journalctl -u servicename
   # 实时查看日志：
   journalctl -f
   ```
   
6. **`dmesg`**：显示或控制内核环缓冲区的消息。
   ```bash
   dmesg
   ```

7. **`logrotate`**：用于管理和轮换日志文件，防止日志文件变得过大。它根据配置文件自动处理日志的归档、压缩和删除旧日志。
   - 配置文件通常位于 `/etc/logrotate.conf` 和 `/etc/logrotate.d/` 目录下。

#### 日志分析工具

- `rsyslog`：是一个增强的日志处理系统，支持复杂的过滤规则、远程日志传输等功能。
- `ELK Stack` (Elasticsearch, Logstash, Kibana)**：用于收集、解析、索引和可视化日志数据的强大工具集。
- `Graylog`：类似于 ELK Stack 的开源日志管理平台，易于设置和使用。
- `Splunk`：商业级的日志分析平台，提供强大的搜索和分析功能。
- `split`：用于将大文件分割成较小的部分
  * 基本语法`split [选项] [输入文件] [前缀]`
  * 假设你有一个20G的日志文件，并希望将其分割成每个1GB的小文件：`split -b 1G your_log_file.log your_log_file_split_`

### 服务启动配置文件

在Linux系统中，服务的启动配置文件通常与`systemd`相关联，因为它是大多数现代Linux发行版使用的初始化系统和服务管理器。`systemd`使用单元（unit）文件来定义如何启动和管理服务。以下是关于服务启动配置文件的主要信息：

**单元文件的位置**

1. **/etc/systemd/system/**: 这个目录用于存放用户自定义的服务单元文件。如果你需要覆盖默认设置或添加新的服务配置，应该将你的单元文件放在这里。
   
2. **/usr/lib/systemd/system/** 或 **/lib/systemd/system/**: 这些目录包含由软件包安装的服务单元文件。这些文件不应该被直接修改，因为它们会在软件包更新时被覆盖。

**单元文件的基本结构**

一个典型的`.service`单元文件包括以下几个部分：

- **[Unit]**：提供有关服务的基本信息，如描述、文档位置、依赖关系等。
  
  示例：
  ```ini
  [Unit]
  Description=Example service
  Documentation=http://example.com/docs
  After=network.target
  ```

  [Unit] 段主要用于定义服务元数据和依赖关系。
  
  - **Description**: 服务的描述。
  - **Documentation**: 文档链接。
  - **Requires**: 列出此单元所依赖的所有其他单元，如果其中任何一个失败，该单元也将无法启动。
  - **Wants**: 类似于 Requires，但不强求依赖单元成功启动。
  - **After**: 定义此单元应在哪些单元之后启动，但不创建依赖关系。
  - **Before**: 定义此单元应在哪些单元之前启动。
  - **Conflicts**: 指定与本单元冲突的单元，如果列出的单元正在运行，则本单元不能启动。
  - **Condition...**: 如 `ConditionPathExists`, `ConditionDirectoryNotEmpty` 等条件语句，当条件满足时才启动服务。
  
- **[Service]**：指定如何启动服务，以及服务运行时的行为。
  
  示例：
  ```ini
  [Service]
  ExecStart=/usr/bin/example-service
  Restart=always
  User=nobody
  Environment=SECRET_KEY=your_secret_key
  ```

  [Service] 段用于指定服务的具体行为。
  
  - **Type**: 定义启动过程的类型（simple, exec, forking, oneshot, notify, dbus）。
  - **ExecStart**: 启动服务时执行的命令或脚本。
  - **ExecStartPre** / **ExecStartPost**: 在启动服务前后执行的命令。
  - **ExecReload**: 重新加载服务时执行的命令。
  - **ExecStop**: 停止服务时执行的命令。
  - **Restart**: 定义在什么情况下重启服务（always, on-success, on-failure, on-abnormal, on-watchdog, on-abort）。
  - **User** / **Group**: 运行服务的用户和组。
  - **Environment** / **EnvironmentFile**: 设置环境变量或指定环境变量文件。
  - **WorkingDirectory**: 设定工作目录。
  - **StandardOutput** / **StandardError**: 定义标准输出和错误输出的位置。
  
- **[Install]**：定义服务如何被启用或禁用。它包含了服务在不同目标(target)中的行为。
  
  示例：
  ```ini
  [Install]
  WantedBy=multi-user.target
  ```
  
  [Install] 段用于定义如何启用服务。
  
  - **WantedBy**: 定义在哪个目标（target）下启用该服务，例如 `multi-user.target` 表示多用户模式下自动启动。
  - **RequiredBy**: 类似 WantedBy，但是表示该服务是必需的。
  - **Alias**: 提供一个别名，使得可以通过不同的名称来引用该服务。
  - **Also**: 当此服务被启用时，也同时启用列表中的其他服务。

**常用命令**

- **重新加载systemd配置**：当你修改了单元文件后，可以使用以下命令让systemd重新加载所有单元文件而无需重启系统。
  
  ```bash
  sudo systemctl daemon-reload
  ```
  
- **启用服务**：使服务开机自动启动。
  ```bash
  sudo systemctl enable example.service
  ```

- **启动服务**：立即启动服务。
  
  ```bash
  sudo systemctl start example.service
  ```
  
- **启动服务**：重新启动服务。

  ```bash
  systemctl restart <服务名>

- **查看服务状态**：检查服务当前的状态。

  ```bash
  sudo systemctl status example.service
  ```

- **停止服务**

  ```
  sudo systemctl stop <服务名>
  ```

- **查看失败的服务**

  ```bash
  systemctl --failed

- **列出所有服务**

  ```bash
  systemctl list-units --type=service

- **查看日志**

  ```bash
  journalctl -u <服务名>
  journalctl -u <服务名> -f

- **查看服务是否启用开机启动**

  ```bash
  systemctl is-enabled <服务名>

- **检查服务是否正在运行**

  ```bash
  systemctl is-active <服务名>

- **获取系统的整体状态以及所有单元的信息：**

  ```bash
  systemctl
  # 或者更详细的信息
  systemctl status

## 网络管理

**一、IP规划**

![](..\typoratuxiang/linux/wl1.png)

在 IP 地址中，**网络 ID** 和 **主机 ID** 是用来区分网络部分和主机部分的两个重要概念。它们是基于子网掩码（或 CIDR 表示法中的前缀长度）来划分的。

**网络 ID**

- **定义**: 网络 ID 是 IP 地址中用于标识一个网络的部分。
- **作用**: 它告诉路由器和其他网络设备哪些设备属于同一个网络。
- **特点**:
  - 网络 ID 是所有属于同一网络的设备共有的部分。
  - 在 IPv4 中，网络 ID 的位数由子网掩码决定。
  - 网络 ID 的所有主机位必须为 `0`。

示例：假设 IP 地址为 `192.168.1.10`，子网掩码为 `255.255.255.0`（即 `/24`），那么：

- 网络 ID 是 `192.168.1.0`，因为前 24 位是网络部分。

**主机 ID**

- **定义**: 主机 ID 是 IP 地址中用于标识网络内具体设备的部分。
- **作用**: 它用于区分同一网络中的不同主机。
- **特点**:
  - 主机 ID 是每个设备在同一个网络中唯一的部分。
  - 主机 ID 的位数由子网掩码剩余的位数决定。
  - 主机 ID 全为 `0` 或全为 `1` 的地址通常有特殊用途（如网络地址和广播地址）。

示例：继续上面的例子：

- IP 地址为 `192.168.1.10`，子网掩码为 `255.255.255.0`（即 `/24`）。
- 主机 ID 是 `0.0.0.10`，因为最后 8 位是主机部分。

**无类CIDR**

* 网络id与主机id不确定，使用netmask：表示32位2进制数，网络ID位数对应为1，主机ID位数对应0
* 表示方法`IP/网络ID位数`列`192.168.31.98/22`
* 网络计算公式
   * 网络（网段）数量=2^可变网络ID数量
   * 一个网络中的主机数量=2^主机ID位数^-2=2^(32-网络ID位数)^-2
* 两个网段进行通信，先看是否在同一个网段，再决定是否向上路由器寻找
* 查看是否在同一网段查看子网掩码是否相同，相同就在同一网段

**二、子网划分**

* 将大网络划（主机多=主机ID位数多，网络ID位数少）分为多个小网络（主机少=主机ID位数少，网络ID位数多）
* 划分子网，网络ID为向主机ID位借位，划分为2^n^个小网络
* 合并超网：将多个小网合并为一个大网；主机 ID 位向网络 ID 位借位

**三、跨网通信**

* 跨网通信：路由`route -n`查看和管理网络路由表
* 路由分类：
  * 主机路由
  * 网络路由
  * 默认路由
* 优先级：精度越高，优先级越高
* 路由表的构成
  * 目标（Destination）：数据包发送的目标路径
  * 子网掩码（Genmask ）:
  * 路由接口（Iface）:本路由器的出口
  * 网关（Gateway）:
    1. 直连：不需要配置
    2. 非直连：下一个路由器邻近本路由器的接口地址
* 加网关是为了加默认路由

### 网卡配置

配置IP地址有两种方式：1.自动获取；2.自己设置固定地址

* 将 Linux 主机接入到网络，需要配置网络相关设置。
  * 主机各
  * IP/netmask
  * 路由：默认网关
  * DNS 服务器
    * 主DNS服务器、次DNS服务、第三DNS服务器

* 查看主机名：`hostname`

* 配置了网络服务需要重新加载网络服务`systemctl restart NetworkManager`

* 接口命名方式：就是更改eth，ifconfig查询出来的名字

* 查看网卡

  * `dmesg | grep —i eth`
  * `ethtool -i eth0`

* 卸载网卡驱动

  * `modprobe  -r e1000`
  * `rmmod e1000`

* 装载网卡驱动

  * `modprobe e1000`

* 静态指定

  * `ifconfig、route, netstat、ip:object{link,addr,route}、ss、tc、system-config-network-tui、setup、配置文件`

* 动态分配

  * `DHCP: Dynamic Host Configuration Protocol`

* `ifconfig`

  * up	启用网络接口`ifconfig eth0 up`
  * down	禁用网络接口`ifconfig eth0 down`
  * inet	设置 IPv4 地址`ifconfig eth0 192.168.1.100 netmask 255.255.255.0`
  * netmask	设置子网掩码`ifconfig eth0:1 192.168.1.101 netmask 255.255.255.0`
  * broadcast	设置广播地址`ifconfig eth0 broadcast 192.168.1.255`
  * mtu	设置最大传输单元`ifconfig eth0 mtu 1400`
  * promisc	进入混杂模式`ifconfig eth0 promisc`、退出`ifconfig eth0 -promisc`

* `route` 命令

  * 路由管理命令

  * 查看：`route -n`

  * 添加：`route add`

    ```shell
    # 语法：route add [-net|-host] target [netmask Nm] [gw Gw] [[dev] If]
    # 目标： 192.168.1.3 网关：172.16.0.1
    route add -host 192.168.1.3 gw 172.16.0.1 dev eth0
    ```

  * 删除`route del default gw 172.20.0.1`

* 配置动态路由

  * 通过守护进程获取动态路由
  
  * 安装 quagga 包
  
  * 支持多种路由协议：RIP、OSPF 和 BGP
  
  * 命令 vtysh 配置
  
     ```shell
     # 安装
     yum install quagga
     # 输出 quagga 包安装的所有文件及其完整路径
     rpm -ql quagga
     # 启动
     systemctl start ospfd
     # 查看对应端口是否启动
     ss -ntl
     ss -ntlp
     # 将配置文件放到配置文件目录
     cp /usr/share/doc/quagga-0.99.22.4/ospfd.conf.sample /etc/quagga/ospfd.conf
     # 查看文件
     cat /etc/quagga/ospfd.conf
     # 启动
     systemctl start ospfd
     # 登录
     vtysh
     # 使用思科命令操作
     ```

###  **IP 转发** 功能来启用路由功能

* 检查当前的 IP 转发状态`cat /proc/sys/net/ipv4/ip_forward`

   * 如果输出为 `1`：表示 IP 转发已启用。
   * 如果输出为 `0`：表示 IP 转发未启用。

* 临时启用 IP 转发；可以通过修改 `/proc` 文件系统中的参数来临时启用 IP 转发。此更改会在系统重启后失效。

   * 运行以下命令启用 IP 转发：`echo 1 > /proc/sys/net/ipv4/ip_forward`
   * 如果需要禁用 IP 转发，可以运行：`echo 0 > /proc/sys/net/ipv4/ip_forward`

* 永久启用 IP 转发

   * 编辑 sysctl 配置文件 `/etc/sysctl.conf` 文件：`nano /etc/sysctl.conf`
   * 找到以下行（如果没有则添加）：`net.ipv4.ip_forward = 1`
   *  应用配置`sysctl -p`

* 配置防火墙规则（可选）：如果启用了防火墙（如 `iptables` 或 `firewalld`），需要添加规则以允许数据包转发。

   * 使用 iptables

      * 运行以下命令允许所有流量转发：`sudo iptables -A FORWARD -j ACCEPT`
      * 如果需要启用 NAT（网络地址转换），可以添加以下规则：`sudo iptables -t nat -A POSTROUTING -o <外网接口> -j MASQUERADE`
      * 保存 iptables 规则（具体命令可能因发行版而异）。例如，在 CentOS 上可以使用：`sudo service iptables save`

   * 使用 firewalld

      ```bash
      sudo firewall-cmd --add-masquerade --permanent
      sudo firewall-cmd --direct --add-rule ipv4 filter FORWARD 0 -j ACCEPT
      sudo firewall-cmd --reload
      ```

* 验证路由转发功能

   * 查看 IP 转发的统计信息`cat /proc/net/netstat | grep IpForward`

## Linux实用操作

### 各类快捷键

* 强制停止:`ctrl+c`
* 退出、登出:`ctrl+d`
* 历史命令搜索
   1. `history`
   2. ==`！`命令前缀，自动执行上一次匹配前缀的命令==
   3. `ctrl+r`:输入内容去匹配历史命令
      * 回车键可以直接执行
      * 键盘左右键，可以得到此命令（不执行）
* 光标移动
   1. ctrl + a, 跳到命令开头
   2. ctrl + e, 跳到命令结尾
   3. ctrl +键盘左键，向左跳一个单词
   4. ctrl +腱盘右键，向右跳一个单词
* 清屏
   1. 通过快捷键 ctrl + l, 可以清空终端内容
   2. 通过命令 clear 得到同样效果

### 软件安装(yum、apt)

* 使用 yum 为 CentOS 系统安装软件
   * yum 命令
   * yum: RPM 包软件管理器，用于自动化安装配置 Linux软件，并可以自动解决依赖问题。
   * 语法： `yum [-y ] (install | remove | search] 软件名称`
   * 选项：`-y`自动确认，无需手动确认安装或卸载过程
   * install: 安装
   * remove: 卸载
   * search: 搜索
   * yum 命令需要 root 权限哦，可以 su 切换到 root, 或使用 sudo 提权。yum 命令需要朕网
* 使用 apt 为 Ubuntu 安装软件（扩展）
   * 语法： `apt [-y ] (install | remove | search] 软件名称`

### 控制软件启动关闭 systemctl

* Linu ×系统很多软件（内置或第三方）均支持使用 systemctl 命令控制：启动、停止、开机自启
* 能够被 systemctl 管理的软件，一般也称之为：服务
* 语法： `systemctl [start | stop | status | enable | disable] 服务名`
* `start 启动`、`stop 关闭`、`status 查看状态`、`enable 开启开机自启`、`disable 关闭开机自启`
* 系统内置的服务比较多，比如：
   * NetworkManager, 主网络服务
   * network, 副网络服务
   * firewalld, 防火墙服务
   * sshd, ssh 服务（ Fina [ Shell 远程登录 Linu ×使用的就是这个服务）

### 软链接 ln

* 使用 ln 命令创建软连接
* 在系统中创建软链接，可以将文件、文件夹链接到其它位置。类似 Windows 系统中的《快捷方式》
* 语法： `ln -s 参数1 参数2`
   * -s 选项，创建软连接
   * 参数 1 ：被链接的文件或文件夹
   * 参数 2 ：要链接去的目的地

### 日期和时区(date、ntp 、time、cal、hwclock、timedatectl)

* `date` 命令查看日期时间

   * 通过 date 命令可以在命令行中查看系统的时间
   * 语法： `date [-d][+格式化字符串]`
   * d 按照给定的字符串显示日期，一般用于日期计算
   * 格式化字符串：通过特定的字符串标证来控制显示的日期格式
   * `%Y 年`、`%y 年份后两位数字（00..99）`、`%m 月份（01..12）`、`%d 日（01..31）`、`%H 小时（00..23）`、`%M 分钟（00..59）`、`%S 秒（00..60）`、`%s 自1970-01-01 00：00：00 UTC 到现在的秒数`

* 修改 Linux 系统的时区

   * 使用 root 权限，执行如下命令，修改时区为东八区时区

      ```
      rm -f /etc/localtime 
      ln -S /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
      ```

* 使用 ntp 进行时间同步和校准

   * 我们可以通过 ntp 程序自动校准系统时间
   * 安装 ntp: `yum -y install ntp`
   * 启动并设置开机自启：
      * `systemctl start ntpd`
      * `systemctl enable ntpd`
      * 当 ntpd 启动后会定期的帮助我们联网校准系统的时间
      * 也可以手动校准（需 root 权限）： `ntpdate -u ntp.aliyun.com`
      * 通过阿里云提供的服务网址配合 ntpdate （安装 ntp 后会附带这个命令）命令自动校准
   * `ntp`时间同步、centos8默认不在支持ntp软件包
      * 添加wlnmp源`rpm -ivh http://mirrors.wlnmp.com/centos/wlnmp-release-centos.noarch.rpm`
      * 安装ntp服务：`yum install wntp -y`
      * 时间同步`ntpdate ntp1.aliyun.com`

* `time`命令
  * `time` 是一个在 Unix 和类 Unix 操作系统（如 Linux）中用于测量命令执行时间的内置命令。它能够报告命令消耗的时间，包括实际时间（real time）、用户时间（user time）和系统时间（sys time）。
  * `time` 会输出三项时间信息：
    * real：指的是从命令开始执行到结束所经历的总时间，即挂钟时间（wall clock time）。这个时间包括了等待 I/O 完成、其他进程占用 CPU 等非活动时间
    * user：指的是在这个过程中花费在用户模式下的 CPU 时间总量。这是你的程序直接使用的 CPU 时间。
    * sys：指的是在这个过程中花费在内核模式下的 CPU 时间总量。当程序执行需要操作系统提供服务的操作（如磁盘 I/O、网络请求等）时，就会消耗这部分时间。
* `cal` 命令
  * `cal` 命令用于显示日历，默认情况下它会显示当前月份的日历。
* `hwclock` 命令
  * `hwclock` 命令用于查看和设置硬件时钟（也称为 RTC，实时时钟）。硬件时钟是系统中的一个独立时钟，即使系统关闭或重启，它也会继续运行。
  * `hwclock --show`：查看硬件时钟的时间
  * `sudo hwclock --systohc`：将系统时间写入硬件时钟
  * `sudo hwclock --hctosys`：将硬件时钟时间同步到系统时间
* `timedatectl` 命
  * `timedatectl` 是一个更现代的工具，用于管理系统的时间和日期配置。它可以显示当前的系统时间和时区信息，并且还可以用于配置 NTP（网络时间协议）同步。
  * `timedatectl`：查看当前时间和服务状态
  * 时区
    * 查看时区列表：`timedatectl list-timezones`
    * 设置时区中国标准时间（CST，即 `Asia/Shanghai`）：`timedatectl set-timezone Asia/Shanghai`
    * 安装 NTP 客户端（以 Ubuntu 为例）：`install ntp`
    * 启动 NTP 服务：`systemctl start ntp`
    * 检查 NTP 同步状态：`ntpq -p`

### IP地址和主机名

* IP 地址`ipconfig`
* 主机名`hostname`修改主机名`hostnamectl set-hostname 主机名，修改主机名`（需root）
* 域名解析

### 网络请求和下载(ping、wget、curl)

1. 使用 ping 命令检查服务器是否可联通
   * 可以通过 ping 命令，检查指定的网络服务器是否是可朕通状态
   * 语法： `ping [-c num] -p或主机名`
      * 选顶：-c，检查的次数，不使用-c选项，将无限次数持续检查
      * 参数： ip 或主机名，被检查的服务器的 ip 地址或主机名地址
2. 使用 wget 命令下载文件
   * wget 是非交互式的文件下载器，可以在命令行内下载网络文件
   * 语法：`wget [-b] url`
      * 选项： -b, 可选，后台下载，会将日志写入到当前工作目录的wget-log 文件
      * 参数：url, 下载链接
3. 使用 curl 命令发起网络请求
   * curl 可以发送 http 网络请求可用于：下载文件、获取信息等
   * 语法：`curl [-O] url`
      * 选项：-O ，用于下载文件，当 url 是下载链接时，可以使用此选项保存文件
      * 参数： url, 要发起请求的网络地址

### 阿里云yum和epel源

**阿里云地址**

```shell
https://developer.aliyun.com/mirror/
# 阿里云源
wget -O /etc/yum.repos.d/CentOS-Base.repo https://mirrors.aliyun.com/repo/Centos-vault-8.5.2111.repo
# 安装 epel 配置包
wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-8.repo
# 清理缓存
yum clean all
# 从新加载yum缓存
yum makecache
```

### 端口 netstat

* 端口的概念
   * 端口，是设备与外界通讯交流的出入口。端口可以分为：物理端口和虚拟端口两类
      * 物理端口：又可称之为接口，是可见的端口，如 USB 接口， RJ45 网 HDMI 端口等
      * 虚拟端口：是指计算机内部的端口，是不可见的，是用来操作系统和外部进行交互使用的
   * Linux系统是一个超大号小区，可以支持 65535 个端口，这 6 万多个端口分为 3 类进行使用：
      * 公认端口： 1~1023，通常用于一些系统内置或知名程序的预留使用，如 SSH 服务的 22 端口， HTTPS 服务的 443非特殊需要，不要占用这个范围的端口
      * 注册端口：1024~49151， 通常可以随意使用，用于松散的绑定一些程序\服务
      * 动态端口：54152~65535 通常不会固定绑定程序，而是当程序对外进行网络链接时，用于临时使用。
* netstat命令的基本使用
   * 使用 nmap 命令，安装 `nmap: yum -y install nmap`
   * 语法 `nmap 被查看的IP地址`
   * 可以通过 netstat 命令，查看指定端口的占用情况
   * 语法： `netstat -anp | grep 端口号`，安装 netstat: `yum -y install net-tools`
   * 查看所有被占用的端口`netstat -tunlp`

### 禁止远程IP

```shell
firewall-cmd --add-rich-rule='rule family=ipv4 source address="121.123.11.0/24" drop'
firewall-cmd --add-rich-rule='rule family=ipv4 source address="121.123.11.98" drop'
```

### 进程管理 (ps、kill)

1. 进程的概念
   * 程序运行在操作系统中，是被操作系统所管理的。
   * 为管理运行的程序，每一个程序在运行的时候，便被操作系统注册为系统中的一个：进程
   * 并会为每一个进程都分配一个独有的：进程旧（进程号）
   
2. 如何查看进程、关闭进程
   * 可以通过 ps 命令查看 Linux 系统中的进程信息
   
   * 语法： `PS [-e -f]`
   
   * 选项： `-e`, 显示出全部的进程
   
   * 选顶： `-f`, 以完全格式化的形式展示信息（展示全部信息）
   
   * ps：列出系统中正在运行的各种进程的状态信息，包括但不限于进程ID（PID）、父进程ID（PPID）、用户、内存使用情况、CPU占用率等。
   
      * `-a`：显示所有用户的进程（不包括会话领导进程）。
   
      * `-u`：根据用户名或UID显示进程。
   
      * `-x`：显示没有控制终端的进程。
   
      * `-f`：全格式输出，显示更详细的信息。
   
      * `-l`：长格式输出。
   
      * `-t`：指定终端显示进程。
   
      * `--forest`：以树状图显示进程之间的父子关系。
   
      * `--sort`：按照指定的字段排序输出结果。
   
        ```shell
        ps -ef | grep 进程名称 # 查看进程号
        ps aux --forest       # 列出所有用户的所有进程，并以树形结构显示
        ps aux --sort=-%mem   # 按照内存使用率降序排列进程
        ps -u username        # 显示特定用户的进程
        ```
   
   * 一般来兑固定用法就是： ps -ef 列出全部进程的全部信息
      * UDP 进程所属的用户ID
      * PID 进程的进程号 ID
      * PPID 进程的父 ID （启动此进程的其它进程）
      * C：此进程的CPU占用率（百分比）
      * STIME ：进程的启动时间
      * TTY ，启动此程的终端序号，加显示？，表示非终端启动
      * TIMF：进程占用CPU的时间
      * CMD：进程对应名称或启动路径或启动命令
      
   * 关闭进程语法`kill [-9] 进程ID`
   
      * `kill` 命令用于向进程发送信号。默认情况下，它会发送 `TERM` 信号，要求进程正常终止。根据需要，你可以通过 `kill` 命令发送不同类型的信号来指示进程执行特定的行为，例如强制终止。
      * 选顶：`-9`，表示强制关闭进程，不使用此选项会向进程发送信号要求其关闭，但是否关闭看进程自身的处理机制。
      * **`TERM` (15)**：默认信号，请求进程正常终止。
      * **`HUP` (1)**：挂起信号，通常用于通知进程重新加载配置文件。

### 主机状态监控（top、df、du、sar、free、htop、vmstat）

* 查看主机运行状态的监控命令

* `top`:查看 CPU 、内存使用情况；默认每 5 秒刷新一次，语法：直接输入 top 即可，按 q 或 ctrl + c 退出

   * 选项
   * -P：只显示某个进程的信息
   * -d：设置刷新时间，默认是 5s
   * -c：显示产生进程的完整命令，默认是进程名
   * -n：指定刷新次数，比如 top - n 3 ，刷新输出 3 次后退出 
   * -b：以非交互非全屏模式运行，以批次的方式执行 top ，一般配合 -n 指定输出几次统计信息，将输出重定向到指定文件，比如 top -b -n 3 > /tmp/top.tmp
   * -i：不显示任何闲置 (idle) 或无用 (zombie) 的进程
   * -u：查找特定用户启动的进程
   * top 交互式选项==当 top 以交互式运行（非． b 选项启动 ), 可以用以下交互式命令进行控制==
   * h键，按下 h 键，会显示帮助画而
   * c键，按下 c 键，会显示产生进程的完整命令，等同于 -c 参数，再次按下 c ，变为默认显示
   * f键，按下 f 键，可以选择需要展示的项目
   * M键，按下 M 键，根据驻留内存大小 (RES) 排序
   * P键，按下 P 键，根据 CPU 使用百分比大小进行排序
   * T键，按下 T 键，根据时间/累计时间进行排序
   * E键，按下 E 键，切换顶部内存显示单位
   * e键，按下 e 键，切换进程内存显示单位
   * l键，按下 l 键，切换显示平均负载和启动时间信息
   * i键，按下 i 键，不显示闲置或无用的进程，等同于-i参数，再次按下，变为默认显示
   * t键，按下 t 键，切换显示 CPU 态信息
   * m键，按下 m 键，切换显示内存信息

   ![image-20240329162540879](../typoratuxiang/linux/top.png)

   ![image-20240402160828567](../typoratuxiang/linux/top1.png)

* PID: 进程id

* USER: 进程所属户

* PR: 进程优先骁越小,越高

* NI：负值表示高优先级，正表示低优先级

* VIRT: 进程使用虚拟内存，单位 KB

* RES: 进程使用物理内存，单位 KB

* SHR: 进程使用共享内存，单位 KB

* S: 进程状态（ S 休眠， R 运行， Z 僵死状态， N 负数优先级，I空闲状态）

* %CPU: 进程占用（ CPU 率 ）

* %MEM: 进程占用内存率

* TIME+: 进程使用 CPU 时间总计，单位 10 毫秒

* COMMAND: 进程的命令或名称或程序文件路径

* **磁盘信息监控**

#### df

* 使用 df 命令可以查看硬盘的使用情况

   * 语法： `df [-h]`
   * 选顶： 
     * `-h` 或 `--human-readable`：以人类可读的格式（如 KB、MB、GB）显示磁盘空间。
     * `-H` 或 `--si`：类似于 `-h`，但使用 1000 而不是 1024 作为单位的基础。
     * `-T`：显示文件系统类型。
     * `-i`：显示 inode 使用情况。
     * `-t <type>`：仅显示指定类型的文件系统。
     * `-x <type>`：排除指定类型的文件系统。
     * `-a` 或 `--all`：包括伪文件系统、重复文件系统等所有文件系统。
     * `-l` 或 `--local`：仅显示本地文件系统。
* 使用 iostat 查看 CPU 、磁盘的相关信息

   * 语法： `iostat [-x] [num1] [num2]`

   * 选项：-x，显示更多信息
   * num1: 数字，刷新间隔， num2: 数字，刷新几次
* **网络信息监控**
* 使用 sar 命令查看网络的相关统计（ sar 命令非常复杂，这里仅简单用于统计网络）

   * 语法： `sar -n DEV numl num2`
   * 选项： -n, 查看网络，DEV 表示查看网络接口
   * num1: 刷新间隔〈不填就查看一次结束 ), num2: 查看次数（不填无限次数）

#### du

* `du` 是 Linux 系统中用于统计文件或目录磁盘使用情况的命令
* 基本语法:`du [选项] [文件或目录]`
* 常用选项
  * **-h, --human-readable**：以人类可读的格式（如 K、M、G）显示大小。
  * **-s, --summarize**：仅显示指定文件或目录的总大小，不递归显示子目录。
  * **-a, --all**：显示所有文件和目录的大小，包括隐藏文件。
  * **-c, --total**：在显示各文件或目录大小后，额外显示总和。
  * **-d, --max-depth=层数**：限制递归显示的目录层级深度。
  * **--exclude=模式**：排除符合指定模式的文件或目录。
  * **-x, --one-file-system**：仅统计指定文件或目录所在文件系统的使用情况，不跨文件系统统计。

#### df和du的区别

* du（Disk Usage）
  * 用途：计算指定文件或目录的磁盘使用量。
  * 工作原理：递归遍历目录，统计每个文件及子目录的大小，返回总和。
  * 关注点：特定文件或目录占用的磁盘空间。
* df（Disk Free）
  * 用途：显示文件系统的磁盘空间使用情况。
  * 工作原理：扫描文件系统，报告总容量、已用空间、可用空间等。
  * 关注点：整个文件系统的磁盘空间利用情况。

- **du**：关注具体文件或目录的磁盘使用量，帮助用户了解哪些文件占用了大量空间。
- **df**：关注文件系统整体的磁盘空间情况，帮助用户监控磁盘分区的使用情况。

#### free

* 格式`free [参数] `

  * 参数
  *  `-h` 参数可以将内存大小转换为更易读的单位（如 GB、MB）
  * `-t`仅显示总内存和空闲内存
  * `-s 2` 参数可以设置刷新间隔（秒），例如每 2 秒刷新一次
  *  `-w` 参数可以显示更详细的列信息

  ```bash
                 total        used        free      shared  buff/cache   available
  Mem:        8000000     2000000     3000000      500000     3000000     4500000
  Swap:       2000000           0     2000000
  ```

- 字段解释：
  - `total`：总内存大小。
  - `used`：已使用的内存。
  - `free`：完全未被占用的内存。
  - `shared`：多个进程共享的内存。
  - `buff/cache`：用于缓存和缓冲的内存。
  - `available`：估计可用的内存（操作系统可以分配给新进程的内存）。

#### htop

`htop` 是一个增强版的 `top` 命令，提供了更友好的交互式界面和更多的功能。相比 `top`，`htop` 更易用，支持鼠标操作，并且可以直观地显示系统资源的使用情况。

* `htop` 的主要功能
  * 动态显示进程信息：实时显示所有运行中的进程。
  * 颜色区分资源使用：通过颜色直观展示 CPU 和内存的占用情况。
  * 支持鼠标操作：可以用鼠标点击菜单或滚动查看进程。
  * 排序功能：按 F6 键可以选择按 CPU、内存或其他指标排序
  * 搜索进程：按 F3 键可以搜索特定的进程。
  * 终止进程：按 F9 键可以发送信号终止某个进程。
  * 树状视图：按 F5 键可以切换到树状视图，方便查看父子进程关系。

#### vmstat

`vmstat` 是一个用于报告系统虚拟内存统计信息的工具，同时也可以监控 CPU、内存、I/O 等资源的使用情况。

* 格式 `vmstat`
* 

### 环境变量 env

1. 在 Linux 系统中执行： env 命令即可查看当前系统中记录的环境变量
2. 在 Linux 系统中，`$`符号被用于取"变量“的值。`echo $`
3. 自行设置环境变量
   * Linux 环境变量可以用户自行设置，其中分为
      * 临时设置，语法：`export 变量名=变量值`
      * 永久生效
      * 针对当前用户生效，配置在当前用户的：~/.bashrc
      * 针对所有用户生效，配置在系的：/etc/profile 文件中
      * 并过通过语法`source 配置文件`，进行立刻生效、或重新录 FinalSheII生效
   * path环境变量添加
      * /etc/profile加入`export PATH=$PATH:/路径`

### Linux文件的上传和下载(scp、rz、sz)

1. scp命令

   * 拷贝本机/home/administrator/test整个目录至远程主机192.168.1.100的/root目录下代码如下:

      ```
      scp -r /home/administrator/test/ root@192.168.1.100:/root/
      ```

      2、拷贝单个文件至远程主机代码如下:

      ```
      scp /home/administrator/test/test.txt root@192.168.1.100:/root/
      ```

      ==其实上传文件和文件夹区别就在参数 -r， 跟cp, rm的参数使用差不多， 文加价多个 -r==

      3、远程文件/文件夹下载

      举例，把192.168.0.10上面的/root/文件夹，下载到本地的/home/administrator/new/下，使用远程端的root登陆代码如下:

      ```
      scp -r root@192.168.1.100:/root/ /home/administrator/new
      ```

   * scp命令详解

      语法：

      ```
      scp [-1246BCpqrv] [-c cipher] [-F ssh_config] [-i identity_file]
      [-l limit] [-o ssh_option] [-P port] [-S program]
      [[user@]host1:]file1 [...] [[user@]host2:]file2
      ```

   * 参数说明：

      * -1： 强制scp命令使用协议ssh1
      * -2： 强制scp命令使用协议ssh2
      * -4： 强制scp命令只使用IPv4寻址
      * -6： 强制scp命令只使用IPv6寻址
      * -B： 使用批处理模式（传输过程中不询问传输口令或短语）
      * -C： 允许压缩。（将-C标志传递给ssh，从而打开压缩功能）
      * -p：保留原文件的修改时间，访问时间和访问权限。
      * -q： 不显示传输进度条。
      * -r： 递归复制整个目录。
      * -v：详细方式显示输出。scp和ssh(1)会显示出整个过程的调试信息。这些信息用于调试连接，验证和配置问题。
      * -c cipher： 以cipher将数据传输进行加密，这个选项将直接传递给ssh。
      * -F ssh_config： 指定一个替代的ssh配置文件，此参数直接传递给ssh。
      * -i identity_file： 从指定文件中读取传输时使用的密钥文件，此参数直接传递给ssh。
      * -l limit： 限定用户所能使用的带宽，以Kbit/s为单位。
      * -o ssh_option： 如果习惯于使用ssh_config(5)中的参数传递方式，
      * -P port：注意是大写的P, port是指定数据传输用到的端口号
      * -S program： 指定加密传输时所使用的程序。此程序必须能够理解ssh(1)的选项

2. rz、sz

   * 需要安装`yum -y install lrzsz`
   * sz 下载文件名
   * rz 找到文件

### 压缩和解压(tar、gzip、unzip)

1. linux压缩格式tar、gzip
2. tar命令
   * .tar, 称之为 tarball, 归档文件，即简单的将文件组装到一个.tar 的文件内，并没有太多文件体积的减少，仅仅是简单的封装
   * .gz, 也常见为，`.tar.gz `，gzip 格式压缩文件，即使用 gzip 压缩算法将文件压缩到一个文件札可以极大的减少压缩后的体积
   * 针对这两种格式，使用 tar 命令均可以进行压缩和解压缩的操作
   * 语法：`tar [-c -v -x -f -z -C]参数1 参数2 ....参数N`
      * -c：创建压缩文件，用于压缩模式
      * -v：显示压缩、解压过程，用于查看进度
      * -x：解压模式
      * -f： 要创建的文件，或要解压的文件，-f 选项必须在所有选项中位置处于最后一个
      * -z：gzip 模式，不使用-z就是普通的tarball格式
      * -C：选择解压的目的地用于解压模式
   * **示例：**
   * 压缩
   * `tar -cvf test.tar 1.txt 2.txt 3.txt`
   * 将 1.txt 2.txt 3.txt 压缩到 test.tar 文件内
   * `tar -zcvf test.tar.gz 1.txt 2.txt 3.txt`
   * 将 1.txt 2.txt 3.txt 压缩到 test.tar.gz 文件内，使用 gzip 模式
   * 解压
   * `tar -xvf test.tar`
   * 解压 test.tar, 将文件解压至当前目录
   * `tar -xvf test.tar -C /home/itheima`
   * 解压 test.tar, 将文件解压至指定目录 (/home/itheima ）
   * `tar -zxvf test.tar.gz -C /home/itheima`
   * 以 Gzip 模式解压 test.tar.gz, 将文件解压至指定目录（ /home/itheima ）
3. zip 命令压缩文件
   * 使用 zip 命令，压缩文件为 zip 压缩包
   * 语法：`zip [-r] 参数1 参数2 ....参数N`
      * -r：被压缩的包含文件夹的时候，需要使用-r 选和 rm 、 cp 等命令的 -r 效果一致
   * **示例：**
   * `zip test.zip a.txt b.txt c.txt`
   * 将 a.txt b.txt c.txt 压缩到 test.zip 文件内
   * `zip -r test.zip test itheima a.txt`
   * 将 test 、 itheima 两个文件夹和 a.txt 文件，压缩到 test.zip文件内
4. unzip 命令解压文件
   * 使用 unzip 命令，可以方便的解压 zip 压缩包
   * 语法：`unzip [-d] 参数`
      * -d：指定要解压去的位置，同 tar 的 -C 选项
      * 参数，被解压的 zip 压缩包文件
   * **示例：**
   *  `unzip test.zip`, 将 test .zip 解压到当前目录
   * `unzip test.zip -d /home/itheima`, 将 test.zip 解压到指定文件夹内 (/home/itheima)

## 软件安装

安装软件需要==root==权限

### mysql

1. 检查是否安装mysql

   ```properties
   rpm -qa|grep mysql
   ```

2. 清理仓库的mysql软件包(查出来后有东西)

   ```properties
   ## 卸载mariadb，mariadb是mysql数据库的分支，mariadb和mysql一起安装会有冲突，所以需要卸载掉
   rpm -qa | grep mariadb
   rpm -e --nodeps mysql80-community-release-el8-3.noarch   #删除mysql的包
   ```

3. 因为mysql并不存在与yum的远程仓库，所以需要配置额外的yum仓库

   ```sh
   #更新密钥
   curl -O https://dev.mysql.com/repo/mysql80-community-release.gpg.key
   #安装mysql 的yum包
   rpm -Uvh https://dev.mysql.com/get/mysql80-community-release-el8-3.noarch.rpm
   #安装mysql源
   yum localinstall -y mysql80-community-release-el7-8.noarch.rpm
   #就可以安装MySQL
   yum -y install mysql80-community-server-<特定的版本号>26
   #使用 yum info 命令查看 MySQL 的详细信息，包括可用版本。
   yum info mysql-community-server
   ```

4. 更换数据源（更换 CentOS 的 YUM 源，以便使用阿里云的镜像源）

   ```properties
   #查看本机yum数据源
   yum repolist
   #备份
   mv /etc/yum.repos.d/ /etc/yum.repos.d_bak 
   #创建新的 YUM 配置文件夹
   mkdir /etc/yum.repos.d/
   #下载阿里云的 CentOS 8.5.2111 镜像源配置文件
   wget -O /etc/yum.repos.d/CentOS-Base.repo https://mirrors.aliyun.com/repo/Centos-vault-8.5.2111.repo
   #导入 MySQL 的 GPG 密钥
   rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql
   #或者禁用gpg
   yum -y install mysql-community-server --nogpgcheck
   ```

5. 清理并更新仓库(验证阿里源和清理yum缓存)

   ```sh
   #模块过滤可能会阻止某些包的显示。禁用模块过滤
   yum module disable mysql
   #清理缓存
   yum clean all
   #从新加载yum缓存
   yum makecache
   ```

6. 下载并安装 MySQL 官方的 Yum Repository（yum仓库）

   ```properties
   #用wget方式进行安装
   wget https://repo.mysql.com//mysql80-community-release-el7-1.noarch.rpm
   #用repo方式进行安装
   rpm -ivh https://repo.mysql.com/get/mysql80-community-release-el7-1.noarch.rpm
   ```

7. 完成后会(在这个目录下)产生两个文件

   ```properties
   cd /etc/yum.repos.d/
   ```

   ![image-20240913165224675](../typoratuxiang/linux/mysqlaz.png)

8. 使用yum安装mysql

   ```sh
   yum install mysql-community-server-8.0.*
   yum install mysql-server
   ```

9. 安装步骤

   ```bash
   # 检查是否安装mysql
   rpm -qa|grep mysql
   # 检查安装下载工具wget
   wget --version
   yum install -y wget
   # 备份 yum 源源文件
   mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.bak
   # 下载阿里云的 yum 源文件，里面的下载镜像网址全部为阿里云服务器
   wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
   # 清理yum缓存，重新生成
   yum clean all
   yum makecache
   # 下载 mysql 源安装包
   wget http://dev.mysql.com/get/mysql80-community-release-el7-8.noarch.rpm
   # 安装mysql源
   yum localinstall -y mysql80-community-release-el7-8.noarch.rpm
   # 检查源是否安装成功
   yum repolist enabled | grep mysql
   # 使用 yum 安装 mysql
   yum install -y mysql-community-server
   #禁用 mysql 模块
   yum module disable mysql
   # GPG密钥验证问题，禁掉GPG验证检查
   yum -y install mysql-community-server --nogpgcheck
   # 再次执行
   yum install -y mysql-community-server
   # 启动mysql
   systemctl start mysqld
   ```

10. 启动mysql并设置开机自启动

    ```bash
    systemctl start mysqld.service
    ```

11. 检查MySQL运行状态

    ```properties
    systemctl status mysqld.service
    ```

12. 查看进程

    ```properties
    ps -ef|grep mysqld
    ```

13. 进入终端、第一次不需要密码

    ```properties
    mysql -u root -p
    #找到临时密码 -----'root'@'localhost后面的是密码
    grep 'temporary password' /var/log/mysqld.log
    ```

14. 设置密码

    ```properties
    #进入数据库
    use user
    #修改密码
    ALTER USER '用户名'@'localhost' IDENTIFIED BY '密码';
    ```

    1. 修改mysql密码级别

       ```properties
       #编辑配置文件
       vi /etc/my.cnf
       #在 [mysqld] 部分
       validate_password.policy=LOW
       #查看密码策略
       SHOW VARIABLES LIKE 'validate_password%';
       # 密码级别
       set global validate_password.policy=low;
       # 密码长度
       set global validate_password.length=4;
       ```

15. 设置远程

    1. 开启防火墙

       ```properties
       查看防火墙状态  systemctl status firewalld
       开启防火墙      systemctl start firewalld  
       关闭防火墙      systemctl stop firewalld
       ```

    2. 开放端口

       ```properties
       添加指定需要开放的端口：
       firewall-cmd --zone=public --add-port=3306/tcp --permanent
       重载入添加的端口：
       firewall-cmd --reload
       查询指定端口是否开启成功：
       firewall-cmd --query-port=3306/tcp
       ```

    3. 远程链接授权

       1. 进入数据库后，使用mysql数据库

          ```sql
          use mysql;
          ```

       2. 查看用户表

          ```sql
          select 'Host','User' from user;
          ```

       3. 更新root用户；%表示为：允许任何ip都可登录

          ```sql
          UPDATE user SET Host= '%' WHERE User= 'root' LIMIT 1;
          ```

       4. 强制刷新权限

          ```sql
          flush privileges;
          ```

16. 更改端口

    1. 查找 MySQL 配置文件

       MySQL 的配置文件通常位于 `/etc/my.cnf` 或 `/etc/mysql/my.cnf`。你可以使用以下命令来查找配置文件的位置：

       ```sh
       find / -name my.cnf
       ```

       通常情况下，你应该关注 `/etc/my.cnf` 或 `/etc/mysql/my.cnf`。

    2. 修改配置文件

       打开 MySQL 的配置文件，编辑 `[mysqld]` 部分，添加或修改 `port` 选项。例如，如果你想将 MySQL 的端口更改为 3307：

       ```ini
       查看端口
       cat /etc/my.cnf | grep port
       [mysqld]
       port = 3307
       ```

       确保在 `[mysqld]` 段落中添加或修改这一行。

    3. 创建新的 socket 文件（如果需要）

       如果 MySQL 服务使用 Unix socket 文件进行本地连接，你也需要确保 socket 文件路径与新的端口号对应。可以在配置文件中指定 `socket` 的路径：

       ```ini
       [mysqld]
       socket = /var/lib/mysql/mysql.sock
       ```

       确保这个路径与你的系统配置相符。

    4. 重启 MySQL 服务

       保存配置文件后，需要重启 MySQL 服务以使新的配置生效：

       ```sh
       systemctl restart mysqld
       ```

    5. 检查 MySQL 服务状态

       确保 MySQL 服务已经成功重启，并且正在监听新的端口：

       ```sh
       netstat -tuln | grep 3307
       ```

       如果输出包含类似 `LISTEN` 的信息，说明 MySQL 已经开始监听新的端口。

    6. 测试 MySQL 连接

    7. 你可以使用 MySQL 客户端工具来测试新的端口是否可用：

       ```sh
       mysql -u root -p -P 3307
       ```

       输入密码后，你应该能够成功连接到 MySQL 服务器。

    7. 更新防火墙规则

       如果防火墙正在运行，你需要更新防火墙规则来允许新的端口：

       ```sh
       firewall-cmd --permanent --remove-port=3306/tcp
       firewall-cmd --permanent --add-port=3307/tcp
       firewall-cmd --reload
       ```

    8. 更新应用程序配置

       确保所有依赖 MySQL 的应用程序都更新了连接字符串，指明新的端口号。

17. 卸载

    卸载 MySQL 的过程涉及多个步骤，包括停止服务、删除相关文件和目录、以及删除系统中的包。以下是详细的步骤：

    步骤一：停止 MySQL 服务

    1. **停止 MySQL 服务**：
       
       ```bash
       sudo systemctl stop mysqld
       ```

    步骤二：删除 MySQL 包

    2. **删除 MySQL 相关的包**：
       使用 `yum` 或 `dnf`（取决于你的 Linux 发行版）来删除 MySQL 相关的包。

       对于 CentOS/RHEL：
       ```bash
       sudo yum remove mysql mysql-server mysql-client mysql-libs
       ```

       对于 Fedora：
       ```bash
       sudo dnf remove mysql mysql-server mysql-client mysql-libs
       ```

    步骤三：删除 MySQL 数据目录和配置文件

    3. **删除 MySQL 数据目录**：
       默认情况下，MySQL 的数据目录位于 `/var/lib/mysql`。

       ```bash
       sudo rm -rf /var/lib/mysql
       ```

    4. **删除 MySQL 配置文件**：
       删除 MySQL 的配置文件 `/etc/my.cnf` 和 `/etc/mysql/` 目录。

       ```bash
       sudo rm -f /etc/my.cnf
       sudo rm -rf /etc/mysql
       ```

    步骤四：删除 MySQL 用户和组

    5. **删除 MySQL 用户和组**：
       删除 MySQL 用户和组（如果存在）。

       ```bash
       sudo userdel mysql
       sudo groupdel mysql
       ```

    步骤五：清理残留文件

    6. **清理残留文件**：
       删除其他可能存在的 MySQL 相关文件和目录。

       ```bash
       sudo find / -name "mysql*" -exec rm -rf {} \;
       ```

    步骤六：验证卸载

    7. **验证 MySQL 是否已完全卸载**：
       检查 MySQL 是否已从系统中完全卸载。

       ```bash
       rpm -qa | grep mysql
       ```

### Tomcat

1. 安装JDK环境
   1. 外部下载linux版本jdk,后缀名为`tar.gz`

   2. 上传到home目录，root链接才能上传文件上传到root用户的home目录，就是点击root文件夹上传

   3. 新建文件夹存放解压文件，和以后安装文件目录

      ```bash
      # mkdir -p /路径/文件名 新建
      mkdir -p /export/server
      # 解压文件到新建文件夹
      tar -zxvf jdk-8u181-linux-x64.tar.gz -C /解压缩后存放位置
      ```
   
   4. 可以指定安装目录的所有文件地址都安装到这个地址`mkdir -p /export/server`
   
   5. 构建文件名软连接
   
      ```bash
      # 方便进入文件夹
      ln -s /export/server/jdk-17.0.12 /export/server/jdk17
      ```

   6. 查看当前目录下所有文件及文件夹所有信息
   
      ```
      ls -l
      ```

   7. 配置环境变量`vim /etc/profile`
   
      1. 全局目录，搜索目录，添加在文件的最后面

         ```properties
         export JAVA_HOME=/usr/local/jdk/jdk1.8.0_181
         export CLASSPATH=$:CLASSPATH:$JAVA_HOME/lib/
         export PATH=$PATH:$JAVA_HOME/bin
         ```
   
      2. 生效
   
         ```properties
         source /etc/profile
         ```
   
      3. 查看是否修改成功
   
         ```properties
         echo $PATH
         ```
   
      4. 删除系统自带的jdk
   
         ```properties
         # 查询系统自带的jdk位置
         which java
         #删除
         rm -f /usr/bin/java
         # 将自己安装的jdk放到/usr/bin/java目录下
         ln -s /export/server/jdk17/bin/java /usr/bin/java
         ```
   
2. 解压部署tomcat：建议使用非root用户安装

   1. 首先,放行toncat需要使用8080端口的外部访问权限：有两种方式

      1. 关闭防火墙
   
         ```bash
         systemctl Stop firewalld      #关闭防火墙
         systemctl disable firewalld   #停止防火墙开机自启动
         ```
   
      2. 配置防火墙放行端口
   
         ```bash
         # --add-port=8080/tcp表示放行8080端口的tcp访问，--permanent表示永久生效
         firewall-cmd --zone=public --add-port=8080/tcp --permanent
         #重新载入防火墙规则使其生效
         firewall-cmd --reload
         # 查询指定端口是否开启成功：
         firewall-cmd --query-port=8080/tcp
         ```
   
      3. 使用root账户创建账户
   
         ```bash
         # 创建用户名
         useradd 用户名
         创建密码
         passwd 密码
         ```
   
   2. 下载安装包
   
      ```properties
      # 下载tomcat
      wget https://dlcdn.apache.org/tomcat/tomcat-10/v10.1.33/bin/apache-tomcat-10.1.33.tar.gz
      #报错https,使用--no-check-certificate不检查证书
      wget --no-check-certificate https://archive.apache.org/dist/tomcat/tomcat-10/v10.0.21/bin/apache-tomcat-10.0.21.tar.gz
      # 也可以外部下载上传
      ```
   
   3. 解压文件到安装文件的文件夹
   
      ```bash
      # 切换回root账户解压
      logout或者exit
      # 解压到指定文件夹
      tar -zxvf apache-tomcat-10.1.33.tar.gz -C /export/server
      ```
   
   4. 构建软连接方便进入文件夹
   
      ```bash
      ln -s /export/server/apache-tomcat-10.1.33 /export/server/tomcat
      ```
   
   5. 修改tomcat的所属者（对用户进行赋权，变更操作者）
   
      ```bash
      chown -R 用户：用户组 文件夹
      chown -R lisuxing:lisuxing tomcat
      chown -R lisuxing:lisuxing apache-tomcat-10.1.33
      ```
   
   6. 切换用户启动tomcat
   
      ```bash
      # 切换用户
      su lisuxing
      # 启动
      /export/server/tomcat/bin/startup.sh         启动./startup.sh
      ```
   
   7. 检查8080端口是否启动成功
   
      ```
      netstat -anp|grep 8080
      ```
