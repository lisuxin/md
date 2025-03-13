[toc]

## 快捷键

1. 查看电脑WiFi密码
   * win+r"cmd"
   * `netsh wlan show profiles`:查看wifi接口上的配置文件
   * `netsh wlan show profiles WIFI名称 key=clear`：查看wifi接口上某个wifi的配置文件

2. 浏览器阅读模式：
   * 在地址栏前加==read==:

3. cd
   * cd到上级目录`cd ..`

4. dir
   * 查看当前目录结构

5. claen
   * 清屏

6. 环境变量
   * 如果把以 % 开头的path目录放到第一个，下次编辑 path 时，就无法显示编辑界面了，而是和win7 的环境变量下的 path 一样，只有一行长串。

7. 多余jdk配置文件位置
   * C:\Program Files (x86)\Common Files\Oracle\Java\javapath

8. 打开控制面板：
   * ctrl + i

9. github地址：
   * `https://docs.github.com/en/issues/trying-out-the-new-projects-experience`

10. cmd：
    * calc:打开计算器

11. 企业微信文件所在地址：`C:\Users\17252\Documents\WXWork\1688855539421386\Cache\File`

12. 开启远程访问

    1. 进入数据库

    2. 执行

       ```sql
       use mysql;
       update user set host = ‘%’ where user =‘root’;
       flush privileges;
       ```

    3. windows开放端口

       1. 控制面板（大图标）
       2. 系统和安全
       3. Windows Defender 防火墙
       4. 高级设置
       5. 入站规则
       6. 新建规则
       7. 规则类型——端口（下一步）
       8. 选择（tcp或者udp）作为传输协议——————选择特定端口或者所有端口（下一步）
       9. 允许连接（下一步）
       10. 选择运用规则在那个网络域下（下一步）
       11. 规则命名，描述

    4. 更改mysql的默认端口

## 账号密码

1. chatgpt
   * 账号：==syarakuryuusa39222@nekomail.link==
   * 密码：==ieOdnNEKUkTJ8==
2. Google;Gmail
   * 账号：==lsuxin186@gmail.com==
   * 密码：==9MN*ZUJqfy$4e*K==
   * Google
     * 账号：`97132312yp@gmail.com`
     * 密码：outtuqqwe1
3. linux虚拟机账号密码
   * 全名：lisuxin
   * 账号：lisuxin
   * 密码：219798
   * 虚拟机位置：D:\linux\CentOS 7 64 位
   * 备份原始镜像`cp /etc/yum.repos.d/CentOS-Linux-AppStream.repo /etc/yum.repos.d/CentOS-Linux-AppStream.repo.backup`
4. 国开行密码：Yp219798
5. oracle
   * 账号：`3183492819@qq.com`
   * 密码：Outt@@11
6. 软考
   * 密码：NiXKsNyaJ-k_4e5
7. todesk
   * 密码：219798Yp@
8. mysql存放数据的位置
   * C:\ProgramData\MySQL\MySQL Server 8.0\Data\
9. postman
   * 用户名：`passyang`
   * 密码：`219798@Qqwe`
   * 邮箱：`3183492819@qq.com`
10. 省考
    * 账号：身份证
    * 密码：`f-X2gWr2wq`
11. git
    * 邮箱：``3183492819@qq.com``
    * 用户：lisuxin
12. steam
    * 用户名：zaa923
    * 密码：outtuqqwe1
13. 小红帽
    * 用户名：lisuxin
    * 密码：kuT3RUX_Ed5!w6G
14. Registry登录密码
    * 用户名：阿里云账户全名 ：lisuxin
    * 密码：tk-(.<fA
15. docker客户端登录时使用的密码
    * 用户名：阿里云账户全名：lisuxin
    * 密码：w}+tK6UB
16. 云服务器ecs
    * 用户名：root
    * 密码：J2vEkF/H
17. 软考
    * 密码：NiXKsNyaJ-k_4e4

## 利用阿里云镜像仓库存储下载镜像

**成本**

所有涉及外部网络的操作都是有一定成本的，

免费，安全，快速。三者不可能都能达到，如果都能达到说明提供服务的人员承担了你的成本。

此方法拉取镜像的成本具体为0.129元/小时。如果你只需要拉一个镜像，也是这个成本。

**效果**

一个500M左右的镜像，推送到阿里云仓库2分钟以内。

之后本地从阿里云仓库下载也只需要2分钟左右。

**物理架构图**

![图片](https://mmbiz.qpic.cn/mmbiz_png/QxFXFNUicBtE7pZo3qD6IKKHmVdETZPfF8jBL1aJsaEnZyQiawVXOiadpvZEibBzGwSzaSMfS6PIhWXhqobYqbhZkQ/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

开通一个最低配的海外机器，使用阿里云的海外区域的镜像仓库作为中转，使用海外机器推送镜像到上面。

之后本地机器从阿里云的海外镜像仓库下载镜像。

**步骤**

简单描述一下步骤

1.  开通一个按需付费的国外机器，1核0.5G，固定带宽1M。
2. 配置同区域的镜像仓库，并为镜像仓库设置固定密码。
3. 登录国外机器，编辑配置，填写镜像仓库地址、账号、密码
4. 复制代码到机器上，执行代码。
5. 镜像推送完后，本地机器拉取镜像。

之后是具体的操作步骤

 **创建按量付费的机器**

进入云服务ECS界面

![图片](https://mmbiz.qpic.cn/mmbiz_png/QxFXFNUicBtE7pZo3qD6IKKHmVdETZPfFEsH2szhj1J2aTkmUxGucB6l1suV4MaZgsjZzNJdSsvS0MIzKRciam1g/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

创建实例

![图片](https://mmbiz.qpic.cn/mmbiz_png/QxFXFNUicBtE7pZo3qD6IKKHmVdETZPfFPYQMt6PKwxHyDjBWsvVPMUibqOjCdUabA1flVKd52HuDUB6Sibk0PnTA/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

选择服务器配置

![图片](https://mmbiz.qpic.cn/mmbiz_png/QxFXFNUicBtE7pZo3qD6IKKHmVdETZPfFMNeh8JdQJictDcWfRfpG6Mdcy2Bcicd9whAnrWvWnciawbSIuqMfy5V0Q/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/QxFXFNUicBtE7pZo3qD6IKKHmVdETZPfFrkpibZcSIoyocSNAPCOMTHlice664TSZR7xFhuQDkRPqzuHzZ5oj3fBw/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



![图片](https://mmbiz.qpic.cn/mmbiz_png/QxFXFNUicBtE7pZo3qD6IKKHmVdETZPfFVrl2IMIME3Rbf5DAhREg9ewHuiciaRFibdrmAJrs02NicSS5Zptiauib0sLw/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/QxFXFNUicBtE7pZo3qD6IKKHmVdETZPfFKb1eOGqnbZyZKfpzNQjttngWkFLxRcpJQnGZAeZ94EO5854rAQDbWw/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/QxFXFNUicBtE7pZo3qD6IKKHmVdETZPfFksfrhdmCJQmYXcibKB2OaKPdeciciajMjsIQ7E3iaCqYQVJXUCe1pBLQKQ/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/QxFXFNUicBtE7pZo3qD6IKKHmVdETZPfFeQz3Ae58rUcy2NvTiavvhCVeEnAtGvI0IeVzO2NDTzuOFEHicRVURsJw/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/QxFXFNUicBtE7pZo3qD6IKKHmVdETZPfFpvDCFJsTH9CEkNOJHTQWpXJAXJnShlns6iaqLxaV1VSjyiagp3TVMjiaw/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



使用公网ip地址登录服务器

账号名为root

密码就是你上面设置的密码

**创建镜像仓库**

![图片](https://mmbiz.qpic.cn/mmbiz_png/QxFXFNUicBtE7pZo3qD6IKKHmVdETZPfFL3aaJfYHgs7dYrQYyOcYa5lEg4tkQiaWIK1mFE6cuQQznTCZ9P95G2Q/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/QxFXFNUicBtE7pZo3qD6IKKHmVdETZPfFtd0ib9kjLTwrGkcrAWRUL8meKiczAibM2cKoLTBB2KvbtaerOaX8TicWjA/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/QxFXFNUicBtE7pZo3qD6IKKHmVdETZPfFs2ldqSYxDuOFnnlmh0HKQBKzh4mrtD9u2npOEHjLRlzaE3iaVD7HfLQ/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



![图片](https://mmbiz.qpic.cn/mmbiz_png/QxFXFNUicBtE7pZo3qD6IKKHmVdETZPfF0cniaOkiaxibRq0EBXDu5t9yTHKAxzg72wxMwjdxhgcTbp6k5spwQI8wQ/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)



![图片](https://mmbiz.qpic.cn/mmbiz_png/QxFXFNUicBtE7pZo3qD6IKKHmVdETZPfFibbCfS3zSQ8hMcg7lv4G9VWRd3d7iatH5Or7aicxeVoH2HCpfdoUL0Kzg/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/QxFXFNUicBtE7pZo3qD6IKKHmVdETZPfF4ILoc2oKaAV8DHb7bZ5a8ia0zReCeMUSIwIYJFkgtZ7FCianwOErvxWA/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/QxFXFNUicBtE7pZo3qD6IKKHmVdETZPfFDohUdRw8V68nJUuezsshNSyMfGSScZBcen3Kic5M0Sn8P1LpfQwCT0w/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/QxFXFNUicBtE7pZo3qD6IKKHmVdETZPfFiaOuICK1cbtibDdub9uZXs5yT6UApmRzx8vYuJOyzOA5dzMIGicnp4Yzg/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

现在你有了一个镜像仓库地址，一个仓库用户名，一个仓库密码

```
仓库地址 registry-vpc.us-west-1.aliyuncs.com/ymyw
用户名 ymyw_net
密码 ********
```

 **登录服务器配置环境**

安装skopeo

```
apt update
apt install skopeo -y
```

创建配置文件`registry.json``，`填入仓库地址，用户名和仓库密码

```shell
{  
"registry":"registry-vpc.us-west-1.aliyuncs.com/ymyw",  
"name":"ymyw_net",  
"password": "********"
}
```

改为你自己的信息,这里的密码是镜像仓库的密码，不要填写成服务器的密码。

创建要下载的镜像列表文件`images.txt`,这里是我使用的部分镜像列表，需要改成你自己要下载的镜像。

```
docker.io/library/node:22docker.io/library/node:20docker.io/library/node:18docker.io/library/node:ltsdocker.io/library/ubuntu:22.04docker.io/library/ubuntu:latestdocker.io/library/nginx:1.27docker.io/library/nginx:1.26docker.io/library/nginx:latestdocker.io/library/mysql:latestdocker.io/library/mysql:8.4docker.io/library/mysql:5.7docker.io/library/golang:latestdocker.io/library/golang:1.22docker.io/library/golang:1.21docker.io/library/postgres:16.3docker.io/library/postgres:16docker.io/library/postgres:15docker.io/library/postgres:latestdocker.io/grafana/grafana:11.1.0docker.io/grafana/grafana:latestdocker.io/prom/prometheus:latestdocker.io/prom/prometheus:v2.53.0docker.io/sonatype/nexus3:3.69.0-java17docker.io/sonatype/nexus3:latestdocker.io/jenkins/jenkins:jdk21docker.io/jenkins/jenkins:latest-jdk21docker.io/jenkins/jenkins:2.464-jdk21docker.io/jenkins/jenkins:latestdocker.io/elastic/kibana:8.14.1docker.io/elastic/elasticsearch:8.14.1docker.io/elastic/logstash:8.14.1docker.io/elastic/filebeat:8.14.1docker.io/elastic/metricbeat:8.14.1docker.io/elastic/auditbeat:8.14.1docker.io/jenkins/jenkins:2.452.2-lts-jdk21docker.io/gitlab/gitlab-ee:17.1.1-ee.0docker.io/library/sonarqube:10.6.0-communitydocker.io/nacos/nacos-server:v2.3.2docker.io/library/redis:7.2.5docker.io/library/redis:latestdocker.io/library/busybox:1.36docker.io/library/busybox:latestdocker.io/library/python:latestdocker.io/library/python:3.12
```

python3代码文件`sync.py`

```python
import subprocessimport json
with open("registry.json", 'r') as f:    registry_dict = json.loads(f.read())harbor_addr = registry_dict['registry']username = registry_dict['name']passowrd = registry_dict['password']with open('images.txt', 'r') as f:    for image in f.readlines():        image_name = image.strip()        if not image_name:            continue        if image_name.startswith('docker.io/library'):            image_path = image_name.split("/")[-1]        elif image_name.startswith('docker.io'):            image_path = f'{image_name.split("/")[-1]}'        else:            image_path = image_name        command = [            '/usr/bin/skopeo', 'copy',            f'docker://{image_name}',            f'--dest-creds', f'{username}:{passowrd}',            f'--dest-tls-verify=false',            f'docker://{harbor_addr}/{image_path}'        ]        print(' '.join(command))        process = subprocess.Popen(command,                                   stdout=None,                                   stderr=None,                                   )        process.wait()        if process.returncode == 0:            print("\nDownload completed successfully.")        else:            print("\nDownload failed with errors.")
```

注意上面3个文件都要在同一个目录下。

**推镜像到镜像仓库**

如果只有几个镜像直接运行

```
python3 sync.py
```

如果镜像多，防止终端断开导致推送终止，可以使用screen。

```shell
screen -R sync
# 会进入一个新终端，在里面执行
python3 sync.py
# 如果网络端口或者终端被关闭力
# 使用命令能够再次进入终端，命令还在一直执行
screen -R sync
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/QxFXFNUicBtE7pZo3qD6IKKHmVdETZPfFkstC6rRypDvprPVYJTVibPVHuibjE6dMTyjia9qzaicOvtuJP9xOticJUqQ/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

逻辑上来说1个小时可以拉取30G左右的镜像。

**本地服务器拉取镜像**

再次查看阿里云上的镜像仓库，可以看到已经推送成功了一些镜像

![图片](https://mmbiz.qpic.cn/mmbiz_png/QxFXFNUicBtE7pZo3qD6IKKHmVdETZPfFKSGp0doYxxwibVVe7ImbaaI7ickSow2QXJ8x0TuyCQbwFC3HvS3JSwjA/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

随便找一个点击进去

![图片](https://mmbiz.qpic.cn/mmbiz_png/QxFXFNUicBtE7pZo3qD6IKKHmVdETZPfFzrIeBf6lwpVeoSqgVia0RkMQMII5RcO8eXCkbFF3gIxQLweD0F0rJTA/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

这里版本号为8.14.1

那么镜像下载命令就是

```
docker pull registry.us-west-1.aliyuncs.com/ymyw/logstash:8.14.1
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/QxFXFNUicBtE7pZo3qD6IKKHmVdETZPfFFgHkjZv5aIPKlq79ggV1tibYWIrffXFO1NERWNBIJnITjiaibojTKu9iaQ/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

好了，镜像可以下载到本地机器了。剩下的根据自己情况直接使用还是重新更改tag。
