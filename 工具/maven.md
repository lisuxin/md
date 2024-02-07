# maven自动化构建工具

官网：http://maven.apache.org/

[TOC]

#  简介

## 1.1 软技开发的阶段

需求分析：分析项目具体完成的功能，有什么要求，具体怎么实现。

设计阶段：根据分析结果，设计项目具体的使用什么项目，解决难点。

开发阶段：编码实现功能，编译代码，自我测试。

测试阶段：专业测试人员，测整个项目的功能是否符合设计要求，出一个测试报告。

##  1.2 maven能做什么

1. 项目的自动构建，帮助开发人员做项目代码的编译测试，打包，安装，部署等工作
2. 管理依赖

​    依赖：项目中需要使用的其他资源，常见的jar。

**构建**：项目的构建

构建是面向过程的，就是一些步骤，完成项目代码的编译，测试，运行，打包等等：maven支持的构建包括有

| 项目构建中的各个环节：清理、编译、测试、报告、打包、安装、部署 |
| :----------------------------------------------------------: |

1. 清理：把之前项目编译的东西删掉，为新编译的代码做准备
2. 编译：把程序源代码编译为可执行代码，`java-class` 文件批量的，maven可以同时把多个源文件编译为class文件，javac一次只能编译一个源文件。
3. 测试：maven可以执行测试程序代码，验证你的功能是否正确，maven可以同时执行多个测试文件。同时测试很多功能
4. 报告：生成测试结果的文件，测试通过没有
5. 打包：把你的项目中的所有的class文件，配置文件等所有资源放到一个压缩文件中，这个压缩文件就是项目的结果文件，通常java程序，压缩文件的扩展名是jar,对于web应用，压缩文件是.war
6. 安装：把5生成的文件`.jar.war`安装到本机仓库
7. 部署：把程序安装好可执行。

 ## 1.3 Maven 中的的概念

1. `POM` ：一个文件`pom`项目对象模型
2. 约定的目录结构：项目的目录和文件位置都是规定的
3. 坐标：是唯一的字符串，用来表示资源的。
4. 依赖管理：管理你的项目可以使用的jar文件
5. 仓库管理：你的资源存放的位置
6. 生命周期：maven构建项目的过程
7. 插件和目标：执行maven构建时使用的工具是插件
8. 继承
9. 聚合

## 1.4 Maven获取安装

安装：

1. 下载.zip文件。确定JAVA_HOME 安装目录
2. 解压缩到一个文件目录中。路径不要有中文，不要有空格
3. 吧maven安装目录下BIN的路径添加到path中
4. 测试maven的安装。在命令行执行 ==`mvn -v`==

![1](D:\笔记\typoratuxiang\maven\测试结果.png)

###  1.4.1 maven解压后目录结构

![1](D:\笔记\typoratuxiang\maven\maven解压后目录结构.png)

`bin`：maven可执行文件，组要是`mvn.cmd`

`conf`：maven工具自己的配置文件,里面setting文件最重要

### 1.4.2 idea查看使用的maven是谁的，什么版本



# 2 maven的核心概念

## 2.1 约定的目录结构

maven大多数人遵循的目录结构，叫做约定目录结构。

一个maven项目是一个文件夹，比如项目叫做Hello。

```java
Hello 项目文件夹
    \src
         \main               叫做主程序目录（完成项目功能的代码和配置文件）
              \java          源代码（包和相关的类定义）
              \resources     配置文件
         \test...............放置测试程序代码的（开发人员自己写的测试代码）(可以没有)
              \java          测试代码的（junit）
              \resources     测试程序需要的配置文件
    \pom.xml                 maven的配置文件，核心文件（maven必须有的）
```

maven的使用方式

1) maven可以独立使用：创建项目，编译代码，测试程序，打包，部署等等
2)  maven和idea一起使用：通过idea借助maven，实现编码，测试，打包等等

编译main目录下所有的Java代码 `mvn compile`在根目录下使用;执行时需要在classes目录下面执行cmd

执行maven时会下载一些东西，因为maven工具执行的操做需要很多插件（下载的都是Java类），.jar文件在maven中叫做插件，插件是完成某些功能的，下载的东西默认存放在C:\Users\登录系统的用户名\\.m2\repository

中央仓库文件地址：Downloading

```
 https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-resources-plugin/2.6/maven-resources-plugin-2.6.jar
```

出现BUILD SUCCESS表示插件下载成功

执行mvn compile结果在项目的根目录下生成target目录（结果目录）；maven编译的Java程序，最后的class文件都放在target目录中

## 2.2 修改本地仓库地址

1. 修改maven的配置文件，maven安装目录/conf/setting.xml
2. 先备份setstring.xml
3. 修改localRepository指定你的目录(不要中文目录)

```xml
<!-- 配置本地仓库-->
  <localRepository>D:/maven/mavenwarehouse</localRepository>
<!--D:/maven/mavenwarehouse本地仓库地址-->
```

## 2.3 仓库概念

1. 什么是仓库：仓库就是存放东西的，存放maven使用的jar和我们项目使用的jar

> > maven使用的插件（各种jar）
> >
> > 我项目使用的jar（第三方的工具）

2. 仓库的分类：

本地仓库，就是你的个人计算机上的文件夹，存放的各种jar

远程仓库，就是在互联网上的，需要使用网络才能使用的仓库

1. 中央仓库：最权威的，所有开发人员都共享的一个集中的仓库`http://repo.maven.apache.org`中央仓库地址
2. 中央仓库镜像：就是中央仓库的备份,在各大洲，重要城市都是镜像
3. 私服：在公司内部，在局域网中使用，不对外使用的。

仓库的使用：maven的使用不需要人为的参与

比如开发人员需要使用mysql驱动----->maven先查本地仓库（有就使用，没有就逐级向上查找）-------->私服(私服有就下载到本地仓库然后使用，没有就在相上查找)--------->镜像（镜像有就下载到私服在下载到本地仓库然后使用，没有就在相上查找）------------>中央仓库（中央仓库有就下载到镜像在下载到私服在下载到本地仓库然后使用）

## 2.4 `POM` 文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.bjpowernode</groupId>
    <artifactId>ch01-maven</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <dependencies>
         <dependency>
              <groupId>junit</groupId>
              <artifactId>junit</artifactId>
              <version>4.11</version>
         </dependency>
    </dependencies>
<build>
     <!--配置插件-->
     <plugins>
          <!--配置具体的插件-->
          <plugin>
              <groupId>org.apache.maven.plugins</groupId>
              <!--插件的名称-->
              <artifactId>maven-compiler-plugin</artifactId>
              <!--插件的版本-->
              <version>3.8.1</version>
              <!--配置插件的信息-->
              <configuration>
                   <!--告诉Maven我们写的代码是在jdk1.8上编译的-->
                   <source>1.8</source>
                   <!--我们的程序应该运行在1.8的jdk上-->
                   <target>1.8</target>
              </configuration>
          </plugin>
     </plugins>
</build>
</project>
```

即Project Object Model项目对象模型,maven把项目当作模型处理，是一个pom.xml文件pom.xml是maven的灵魂

`pom`初识

<table>
    <tr><td colspan="3">基本信息</td></tr>
    <tr>
        <td>modelVersion</td>
        <td colspan="2">Mavem的版本，对于Maven2和Maven3来说他只能是4.0.0</td>
    </tr>
    <tr>
        <td>groupId</td>
        <td>组织id，一般为公司域名倒写。格式可以为：1.域名倒写。2.域名倒着写加项目名</td>
        <td rowspan="3">groupId、artifactId、version三个元素生成一个Maven的坐标，在众多Maven项目中可以唯一定位到某一个项目。坐标也决定着将来项目在仓库中的路径即名称
    </tr>
    <tr>
        <td>artifactId</td>
        <td>项目名称，也是模块名称，对应groupId中的子项目</td>
    </tr>
    <tr>
    <td>version</td>
    <td>项目的版本号。如果项目还在开发中，是不稳定版本，通常在版本后带—SNAPSHOTversion使用三位数字标识，例如1.1.0</td>
    </tr>
    <tr>
        <td>packaging</td>
        <td colspan="2">项目打包的类型，可以使jar、war、rar、ear、pom、默认jar</td>
    </tr>
    <tr><td colspan="3">依赖</td></tr>
    <tr>
        <td>dependencies和dependency</td>
        <td colspan="2">Maven的一个重要作用就是管理jar包,为了一个项目可以构建或运行,项目中不可避免的,会依赖很多其他的jar包,在Maven中,这些jar就被称为依赖,使用标签dependency来配置。而这种依赖的配置正是通过坐标来定位的,由此我们也不难看出,maven把所有的jar包也都视为项目存在了。</td>
    </tr>
    <tr><td colspan="3">配置属性</td></tr>
    <tr>
        <td>properties</td>
        <td colspan="2">properties 是用来定义-些配置属性的,例如project.build.sourceEncoding (项目构建源码编码方式),可以设置为,UTF-8,防止中文乱码,也可定义相关构建版本号,便于日后统一升级。</td>
    </tr>
    <tr><td colspan="3">构建</td></tr>
    <tr>
        <td>build</td>
        <td colspan="2">build表示与构建相关的配置,例如设置编译插件的jdk版本</td>
    </tr>
    <tr><td colspan="3">继承</td></tr>
    <tr>
        <td>packaging</td>
        <td colspan="2">项目打包的类型，可以使jar、war、rar、ear、pom、默认jar</td>
    </tr>
    <tr><td colspan="3">聚合</td></tr>
    <tr>
        <td>packaging</td>
        <td colspan="2">项目打包的类型，可以使jar、war、rar、ear、pom、默认jar</td>
    </tr>
</table>
**坐标**：唯一值吗，在互联网上唯一标识一个项目的 

```xml
<groupId>公司域名的倒写</groupId>
<artifactId>自定义项目名称</artifactId>
<version>自定义版本号</version>
```

`https://mvnrepository.com/`搜索使用的中央仓库，使用groupId或者artifactId做为搜索条件

packaging打包后的后缀名，默认jar

**依赖**：你的项目的中要使用的各种资源说明

```xml
<dependencies>
    <!--依赖相当于Java代码中的import-->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.9</version>
    </dependency>
</dependencies>
```

**properties**：设置属性

```xml
<properties><!--测试属性的-->
    <java.version>1.8</java.version>
    <!--告诉maven jdk 使用的版本-->
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
</properties>
```

**build**:maven在进行项目构建时配置信息，例如指定编译Java代码使用的jdk的版本

### 2.4.1 maven的生命周期

就是maven构建项目的过程，清理编译，测试，报告，打包，安装，部署，

### 2.4.2 maven的命令

maven独立使用，通过命令，完成maven生命周期的执行

maven可以使用命令完成项目的清理，编译，测试等等

* mvn clean`清理`:会删除原来编译和测试的目录，即target目录，但是已经install到仓库里的包不会删除
* mvn compile`编译主程序`:会在当前目录下生成一个target，里面存放编译主程序之后的字节码文件
* mvn test-compile`编译测试程序`:会在当前目录下生成一个target,里面存放编译测试程序之后生成的字节码文件
* mvn test`测试`:会生成一个目录surefire-reports,保存测试结果
* mvn package`打包主程序`:会编译、编译测试、测试、并且按照pom.xml配置把主程序打包生成jar或者是war包
* mvn install`安装主程序`:会把本工程打包，并按照本工程的坐标保存到本地仓库中
* mvn deploy`部署主程序`:会把本工程打包，按照工程的坐标保存到本地库中，并且还会保存到私服仓库中。还会自动把项目部署到web容器中

执行上述命令必须在命令行进入pom.xml所在目录

`mvn compile`只编译main/java下的目录`mvn test-compile`编译test/Java下的`mvn test`执行test/Java下的目录

==mvn compile编译main/java目录下的Java为class文件，同时把class拷贝到target/class目录下面，把main/resources目录下的所有文件都拷贝到target/classes目录下==

### 2.4.3 插件

maven命令执行时，真正完成功能的是插件，插件就是一些jar文件，一些类

**单元测试**（测试方法）：用的是junit，junit是一个专门测试的框架（工具）。

junit测试的内容：测试的是类中的方法，每一个方法都是独立测试的，方法是测试的基本单位（单元）。

maven是借助单元测试，批量的测试你类中的方法是否符合预期。

**使用步骤**：1. 加入依赖，在单元测试中加入单元测试依赖

```xml
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.11</version>
    <scope>test</scope>
</dependency>
```

2. 在maven项目中的src/test/java目录下，创建测试程序

推荐的创建类和方法的提示：

1. 测试类的名称 是Test+你要测试的类名
2. 测试的方法名称：Test + 方法名称

例如：你要测试HelloMaven

```java
//测试类
public class TestHelloMaven{
    @test
    public void TestaddNumber(){
        
    }
}
/**TestAdd叫做测试方法，他的定义规则
    1.方法是public的，必须的
    2.方法没有返回值，必须的
    3.方法名称是自定义的，推荐Test + 方法名称
    4.方法的上面要加入@test
    **/
```

mvn compile编译main/java

maven执行测试阶段时前面都执行

测试报告生成在：D:\Users\lisuxin\mavenwork\Holle\target\surefire-reports

打包：也就是压缩文件的制作过程，打包只有src/main下面的东西

安装：是部署到你的本地仓库中去了

**build**:maven构建项目的参数设置

==编译器插件的目标绑定到构建生命周期中的相应阶段。因此，要编译源代码，您只需要告诉专家，直到执行哪个生命周期。以下内容将编译您的源代码==

==如果您的源代码使用非默认编码，则可以使用 `sourceEncoding` 参数来告诉 Maven 在读取 java 源代码时要使用哪种编码。另请注意排除要忽略的源的功能。==

```xml
<!--控制配置maven构建项目参数的设置，设置jdk的版本-->
<build>
     <!--配置插件-->
     <plugins>
          <!--配置具体的插件-->
          <plugin>
              <groupId>org.apache.maven.plugins</groupId>
              <!--插件的名称-->
              <artifactId>maven-compiler-plugin</artifactId>
              <!--插件的版本-->
              <version>3.8.1</version>
              <!--配置插件的信息-->
              <configuration>
                   <!--告诉Maven我们写的代码是在jdk1.8上编译的-->
                   <source>1.8</source>
                   <!--我们的程序应该运行在1.8的jdk上-->
                   <target>1.8</target>
              </configuration>
          </plugin>
     </plugins>
</build>
```

配置jdk有两种方式

您可能需要将某个项目编译为与当前使用的版本不同的版本。`javac` 可以使用 `-source 和 -``target` 接受此类命令。编译器插件也可以配置为在编译期间提供这些选项。

例如，如果要使用 Java 8 语言功能部件 （`-source 1.8`），并且还希望编译的类与 JVM 1.8 （`-target 1.8`） 兼容，则可以添加以下两个属性，它们是插件参数的缺省属性名称：

一、

```xml
<configuration>
    <!--告诉Maven我们写的代码是在jdk1.8上编译的-->
    <source>1.8</source>
    <!--我们的程序应该运行在1.8的jdk上-->
    <target>1.8</target>
</configuration>
```

二、

```xml
<project>
  <properties>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
  </properties>
</project>
```

# 在IDEA中使用Maven

1. idea中内置了maven，一般不使用内置的，因为内置maven设置不方便，使用自己安装的maven，需要覆盖idae中的默认设置。让idea指定maven安装位置等信息。

配置入口file下

* Settings当前工程生效

* Othere Settings为以后工程生效

file------>Setting------->Build,Execution,Deployment------------->Bulid Tools----------->Maven

* Maven home directory:==Maven的安装目录==
* User setting file==用户的配置文件，就是maven安装目录下conf/setting.xml配置文件==
* Local repository==本地仓库的信息，本地仓库的目录位置==

Maven--->Runner

> > VM Options:archetpyteCatalog=internal//为了下载maven模板时速度更快
> >
> > jer:你项目的jdk

maven项目创建时，会联网下载模板文件，比较大，使用archetpyteCatalog=internal，不用下载，创建maven速度快

## 3.1 在idea中创建javase项目

使用模板创建项目

![image-20220530103011959](D:\笔记\typoratuxiang\zawu\maven配置.png)

![](D:\笔记\typoratuxiang\zawu\mave不用下载模板.png)

**-DarchetypeCatalog=internal**

**普通java项目的模板**

![image-20220530103956933](D:\笔记\typoratuxiang\zawu\普通javase模板.png)





## 3.2 在idea中创建web项目

1. 使用骨架方式

   1. 在idea中骨架创建的结构？

      1. 骨架可以更快速的给我们创建出项目结构，idea给我们提供了很多的骨架模板，这样说大家还是不太理解。通俗来说就是用它可以更快的生成项目项目结构：
      2. 我们用了骨架以后还是发现距离一个完整的项目结构还差了一些东西：Maven Web项目缺失的目录结构，没有java和resources目录，需要手动完成创建补齐

   2. 使用骨架方式步骤

      1. 创建Maven项目，给项目取好名字

      2. 选择自己下载的jdk版本

      3. 选择使用Web项目骨架

      4. 确认Maven相关的配置信息

      5. 完成项目创建

      6. 删除pom.xml中多余内容，只留下面的这些内容，注意打包方式 jar和war的区别

         ```java
         <?xml version="1.0" encoding="UTF-8"?>
         <project xmlns="http://maven.apache.org/POM/4.0.0"
                  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
             <modelVersion>4.0.0</modelVersion>
         
             <groupId>org.example</groupId>
             <artifactId>glwc</artifactId>
             <version>1.0-SNAPSHOT</version>
             <packaging>war</packaging>
         
             <properties>
                 <maven.compiler.source>17</maven.compiler.source>
                 <maven.compiler.target>17</maven.compiler.target>
             </properties>
         
         </project>
         ```

      7. 目录结果如下：

      8. 补齐Maven Web项目缺失的目录结构，默认没有java和resources目录

      9. 需要手动完成创建补齐

      10. 创建成功

2. 不使用骨架的方式

   1. 不选择骨架创建的结构？个人推荐使用不用骨架的创建方式
   2. 无骨架创建方式也是需要一些步骤去补全的，仅仅是上图并未完成一个完整的项目创建，下图是我经过操作以后创建成功的项目结构：
   3. 不使用骨架步骤
      1. 创建Maven项目
      2. 选择不使用Web项目骨架，选择本地的jdk
      3. 完成项目的创建
      4. 在pom.xml设置打包方式为war
      5. 补齐Maven Web项目缺失webapp的目录结构
      6. 补充完后，调整一下项目结构，最终的项目结构如下:



## maven报错

1. 使用Maven打包项目的时候，出现错误:`webxml attribute is required (or pre-existing WEB-INF/web.xml if executing in update)`

2. 解决方案

   1. 方案一：

      ```xml
      <!--maven打包war支持依赖-->
          <build>
              <plugins>
                  <plugin>
                      <groupId>org.apache.maven.plugins</groupId>
                      <artifactId>maven-war-plugin</artifactId>
                      <version>3.3.2</version>
                      <!--不检擦是否有web.xml-->
                      <configuration>
                          <failOnMissingWebXml>false</failOnMissingWebXml>
                      </configuration>
                  </plugin>
              </plugins>
          </build>
      ```
      
   
3. 中文乱码

   1. 在==Settings==-->==maven==--->==VM Option==添加以下

   ```xml
   -Dfile.encoding=GB2312
   ```

   
