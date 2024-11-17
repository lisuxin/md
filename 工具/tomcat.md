# tomcat

[toc]

## 基础

### 下载

### 安装：解压及安装

### 目录结构

* bin：可执行文件
* config：配置文件
* lib：依赖资源包
* logs：日志
* temp：临时文件
* webapps：web项目
* work：运行时数据

### 配置环境

1. **新建CATALINA_BASE变量**
   1. 变量名：CATALINA_BASE
   2. 变量值:（填Tomcat的安装目录,刚刚复制好的目录）
2. **新建CATALINA_HOME变量**
   1. 变量名：CATALINA_HOME
   2. 变量值:（填Tomcat的安装目录,刚刚复制好的目录)
3. **新建CATALINA_TMPDIR变量**
   1. 变量名：CATALINA_TMPDIR
   2. 变量值:（填Tomcat的安装目录,刚刚复制好的目录后面加上\temp）
4. **找到Path变量，点击编辑**
   1. 变量名：Path
   2. 变量值:（填Tomcat的安装目录,刚刚复制好的目录后面加上\bin）

### 启动检测

1. startup.bat：启动检测
2. 启动：localhost:8080
3. 启动闪退：替换文件`setclasspath.bat`
4. conf/server.xml可以更改端口号：http默认端口号80

### 关闭

1. shutdown.bat
2. ctrl+c

### 与IDEA集成

1. run：运行
2. edit Configurations：编辑配置
3. Defaults
4. Tomcat Server
5. Local：本地
6. Configurations
   * Tomcat Home：Tomcat安装目录
7. Update：可以热部署

### 部署方式

1. 直接放在tomcat的webapps目录下
   1. 将项目直接放在目录下
   2. 将项目打包为war，将war放置在webapps目录下：war包会自动解压
2. 配置conf/server.xml
   1. 在xml中的`<Host>`加上`<context docBacs="项目实际路径" path="虚拟目录/或者访问路径"/>`
      * 虚拟目录/或者访问路径：虚拟目录
3. 在`conf\Catalina\localhost`目录下创建`虚拟目录.xml`的文件
   * 在xml中添加`<context docBacs="项目实际路径"/>`
   * 访问路径为xml文件名称

### 解决控制台中文乱码

1. 9版本以下的在tomcat中conf里面的server.xml，在Connector中加上`URIEncoding="UTF-8" `
2. 还是不行的在tomcat的bin目录下的catalina.bat加如下一条语句`set JAVA_OPTS=-Xms512m -Xmx1024m -XX:MaxPermSize=1024m -Dfile.encoding=UTF-8  `
2. 10以上版本在conf文件夹下logging.properties文件中注释掉`java.util.logging.ConsoleHandler.encoding = UTF-8`

**解决Tomcat10控制台中文乱码的问题，可以尝试以下几种方法：**

1. 修改`logging.properties`文件：
   - 找到Tomcat安装目录下的`conf/logging.properties`文件。
   - 在文件中查找与编码相关的设置，如`java.util.logging.ConsoleHandler.encoding`。
   - 如果存在该设置并且值为`UTF-8`，尝试将其改为`GBK`，或者如果该行前面有`#`注释符号，尝试取消注释并修改为`GBK`。反之，如果原本是`GBK`，尝试改为`UTF-8`看是否解决问题。示例：
     ```
     java.util.logging.ConsoleHandler.encoding = GBK
     ```
   - 保存更改后，重启Tomcat服务。

2. 调整IDE或终端的编码设置：
   - 如果您是在IDE（如IntelliJ IDEA、Eclipse等）中运行Tomcat，需要检查并设置IDE控制台的编码为与`logging.properties`中一致的编码（GBK或UTF-8）。例如，在IntelliJ IDEA中，可以在“Run/Debug Configuration”中设置控制台的编码为GBK。
   - 如果是直接在Windows命令提示符或Linux终端中运行Tomcat，确保终端的编码也是正确的。对于Windows，可以通过更改命令提示符的属性来调整代码页（例如，使用`chcp 65001`命令切换到UTF-8编码）。

3. 使用VM选项设置JVM编码：
   - 如果上述方法无效，尝试在启动Tomcat时通过VM参数指定文件编码。在Tomcat的启动脚本或IDE的运行配置中，添加如下VM选项：
     ```
     -Dfile.encoding=UTF-8
     ```
   - 注意，这种方法有时可能不会影响到控制台输出的编码，特别是当IDE或操作系统控制台有自己的编码设置时。

4. 检查系统和环境变量：
   - 确保系统环境变量（如`JAVA_TOOL_OPTIONS`或`MAVEN_OPTS`）中没有冲突的编码设置。
