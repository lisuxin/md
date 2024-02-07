# tomcat

[toc]

1. 下载
2. 配置环境
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
3. 启动检测
   1. startup：启动检测
   2. 启动：localhost:8080
4. 解决控制台中文乱码
   1. 9版本以下的在tomcat中conf里面的server.xml，在Connector中加上`URIEncoding="UTF-8" `
   2. 还是不行的在tomcat的bin目录下的catalina.bat加如下一条语句`set JAVA_OPTS=-Xms512m -Xmx1024m -XX:MaxPermSize=1024m -Dfile.encoding=UTF-8  `