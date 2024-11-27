[toc]

1. redis

   ==Redis 是一个基于内存的 key-value 键值存储的、可持久化的数据库，并目提供了非常丰富的数据结构，同时还支持非常丰富的功能==

# 部署

==在linux环境下安装Redis==

Redis多种部署模式，每种模式特定的用途和优缺点。

**单机部署**

* **定义**：
   * 单机部署是指在一个单独的服务器上运行一个Redis实例。
   * **特点**：
   * **简单**：配置简单，易于管理和维护。
   * **性能**：性能较高，因为没有额外的网络开销。
   * **可靠性**：可靠性较低，一旦该服务器出现故障，整个系统将不可用。
   * **扩展性**：难以水平扩展，存储容量和处理能力受限于单台服务器。
   * **适用场景**：
   * 适用于小型项目或测试环境，对数据可靠性和高可用性要求不高。

**主从部署**

* **定义**：
   * 主从部署是指一个主节点（Master）和一个或多个从节点（Slave）的部署模式。主节点负责写操作，从节点负责读操作。
   * **特点**：
   * **读写分离**：主节点处理写操作，从节点处理读操作，可以分担读取压力。
   * **数据备份**：从节点可以作为数据备份，提高数据的可靠性。
   * **故障恢复**：主节点故障时，可以通过手动或自动切换到从节点继续服务。
   * **复杂度**：配置相对简单，但需要管理主从同步和故障切换。
   * **适用场景**：
   * 适用于中型项目，对读性能有一定要求，但对高可用性和数据一致性要求不是特别高的场景。

**哨兵部署**

* **定义**：
   * 哨兵部署是在主从部署的基础上，引入哨兵（Sentinel）来实现自动故障检测和恢复。
   * **特点**：
   * **自动故障检测**：哨兵会持续监控主从节点的健康状态，检测故障。
   * **自动故障转移**：当主节点故障时，哨兵会自动将其中一个从节点提升为主节点，保证服务的连续性。
   * **高可用性**：提高了系统的高可用性，减少了人工干预。
   * **复杂度**：配置和管理相对复杂，需要配置哨兵节点和主从节点。
   * **适用场景**：
   * 适用于对高可用性要求较高的场景，特别是在主节点故障时需要快速恢复服务的情况。

**集群部署**

* **定义**：
   * 集群部署是指多个Redis节点组成的分布式系统，每个节点负责一部分数据，通过分片（Sharding）实现数据的水平扩展。
   * **特点**：
   * **水平扩展**：可以通过增加节点来扩展存储容量和处理能力。
   * **高可用性**：每个分片都有多个副本，可以实现数据冗余和故障恢复。
   * **复杂度**：配置和管理较为复杂，需要处理数据分片、节点通信和故障恢复等问题。
   * **性能**：在网络良好的情况下，性能较好，但在跨节点操作时可能会有额外的网络开销。
   * **适用场景**：
   * 适用于大型项目，对数据容量和处理能力有高要求，且需要高可用性的场景。

**总结**

- **单机部署**：简单易用，适合小规模或测试环境。
- **主从部署**：读写分离，提高读性能，适合中型项目。
- **哨兵部署**：自动故障检测和恢复，提高高可用性，适合对高可用性有较高要求的场景。
- **集群部署**：水平扩展，高可用性，适合大规模项目。

## 防火墙

在生产环境中，建议不要直接卸载防火墙，而是应该适当地配置防火墙规则，以允许Redis服务所需的端口（默认为6379）通过。这样做可以确保你的Redis实例既能够对外提供服务，又不会因为开放了不必要的端口而增加安全风险。

以下是在不同类型的防火墙中开放Redis端口的基本步骤：

**对于`iptables`防火墙：**

1. 打开终端。
2. 输入命令来添加新的规则，允许Redis的默认端口6379：
   ```
   sudo iptables -A INPUT -p tcp --dport 6379 -j ACCEPT
   ```
3. 保存iptables规则：
   - 在某些发行版中，可以使用 `sudo service iptables save` 或者 `sudo iptables-save > /etc/iptables/rules.v4`。
4. 重启iptables服务以应用更改：
   ```
   sudo systemctl restart iptables
   ```

**对于`firewalld`防火墙：**

1. 打开终端。
2. 使用以下命令来添加端口到公共区域：
   ```
   sudo firewall-cmd --zone=public --add-port=6379/tcp --permanent
   ```
3. 重新加载firewalld配置以使更改生效：
   ```
   sudo firewall-cmd --reload
   ```

通过以上步骤，你可以确保Redis能够在保持防火墙开启的情况下正常运行，同时减少潜在的安全威胁。

## 单机部署

### 检查安装gcc环境

==Redis是由C语言编写，它的运行环境需要C环境,因此需要安装gcc==

```bash
--关闭防火墙
systemctl stop firewalld.service
--状态
firewall-cmd --state
--卸载防火墙
yum remove firewalld(测试环境)

--检查版本
gcc --version
--安装gcc
yum install gcc
```

### 下载安装Redis

```bash
--安装文件归类
mkdir -p /opt/software/redis

--进入redis文件夹，使用wget下载
cd /opt/software/redis
wget https://download.redis.io/redis-stable.tar.gz

--解压下载的redis包
tar -xzf redis-stable.tar.gz

--进入redis-stable目录，然后使用make install编译并安装，安装完成后 /usr/local/bin会生成相应服务
cd redis-stable
make install

--检查是否成功生成
ll /usr/local/bin
```

* 文件介绍
   * `redis-benchmark`：性能测试工具
   * `redis-check-aof`：修复有问题的aof文件
   * `redis-check-rdb`：修复有问题的rdb文件
   * `redis-sentinel`：redis集群使用
   * `redis-server`：Redis服务器启动命令
   * `redis-cli`：客户端操作入口

### 启动Redis

到这里其实我们可以在使用 /opt/software/redis/redis-stable/src 或者 /usr/local/bin 目录下的 `redis-server` 启动redis服务了

```bash
--Redis源码路径下启动
./src/redis-server

--使用usr/local/bin路径下启动（该目录下）
redis-server
```

1. 启动报错

   ```
   28779:C 26 Nov 2024 05:57:22.596 # WARNING Memory overcommit must be enabled! Without it, a background save or replication may fail under low memory condition. Being disabled, it can also cause failures without low memory condition, see https://github.com/jemalloc/jemalloc/issues/1328. To fix this issue add 'vm.overcommit_memory = 1' to /etc/sysctl.conf and then reboot or run the command 'sysctl vm.overcommit_memory=1' for this to take effect.
   28779:C 26 Nov 2024 05:57:22.596 * oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
   28779:C 26 Nov 2024 05:57:22.596 * Redis version=7.4.1, bits=64, commit=00000000, modified=0, pid=28779, just started
   28779:C 26 Nov 2024 05:57:22.596 # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
   28779:M 26 Nov 2024 05:57:22.596 # Failed to configure LOCALE for invalid locale name.
   ```

2. **方法一：**临时更改

   * 更改 `LC_COLLATE`，可以直接在命令行中设置环境变量。例如，将其更改为 `C`（默认排序方式）或者 `en_US.UTF-8`，可以使用如下命令：这种方法只对当前的 shell 会话有效，一旦关闭终端窗口或注销登录，设置就会失效。

     ```bash
     export LC_COLLATE=C
     或者
     export LC_COLLATE=en_US.UTF-8
     ```

3.  **方法二：**永久更改

   * 编辑 `~/.bashrc`这个文件中的设置仅影响特定用户的 shell 会话。

     ```bash
     使用文本编辑器打开 `~/.bashrc` 文件：
     vi ~/.bashrc
     在文件末尾添加：
     export LC_COLLATE=en_US.UTF-8
     保存并退出编辑器。
     让更改生效，可以重新加载 `.bashrc` 文件：
     source ~/.bashrc
     ```

   * 验证更改、无论选择哪种方法，都可以通过运行 `locale` 命令来验证更改是否成功：

     ```bash
     locale
     ```

### 配置Redis

前面的启动方式无法再后台运行，退出之后直接关闭了 Redis 服务，所以我们还需要针对 Redis 做一些设置。

```bash
--修改当前Redis目录下的Redis.conf文件
vim Redis.conf
```

需要修改的内容如下：如果大家使用 vim 打开后没有行号，可以在打开 vim 后输入：`": set number"`

```bash
bind * -::*                      #87行，修改bind项，* -::*支持远程链接
daemonize yes                    #309行，开启守护进程，后台运行
logfile /opt/software/redis/redis-stable/redis.log   #355行，指定日志文件目录
dir /opt/software/redis          #510行，指定工作目录
requirepass 密码                  #1044行，给默认用户设置密码，主要是使用redis-cli连接redis-server时，需要通过密码进行链接
protected-mode no                 #111行，允许远程连接       如果不设置密码必须将此设置关闭。
```

修改完成后，使用配置文件启动 Redis, 并使用 redis-cli 连接测试，需要注意由于前面我们配置了安全密码，所以连接后需要先验证密码，否则会报错。

```bash
--使用redis.conf配置文件的方式启动
redis-server redis.conf
--关闭redis
redis-cli shutdown
--远程链接
redis-cli -h redis所在地址 -p redis的端口（默认6379） -a 用户密码
```

## 主从部署（响度均衡）

## 哨兵部署（响度均衡）

## 集群部署（响度均衡）

# 客户端工具

## Redis insight 客户端工具

## Tiny RDM 客户端工具

## SpringBoot 连接 Redis

# 数据结构

## 字符串

## 列表

## 哈希

## 有序集合

## 位图

## 超日志

## 地理位置

# 其他

## 缓存穿透、击穿、雪崩问题

## Redis 数据库和缓存一致性问题

## Redis 事务

## Redis 持久化

# 实战