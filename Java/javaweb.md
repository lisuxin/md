# javaweb

[toc]



## JDBC

定义了所有关系型数据库的规则（接口）

```java
package com.jdbc;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.Statement;

public class MysqlJdbc {
    public static void main(String[] args) throws Exception {
        //注册驱动,mysql5以后可以省略注册驱动
        Class.forName("com.mysql.cj.jdbc.Driver");
        //获取数据库连接对象
        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/test","root","219798");
        //定义sql语句
        String sql = "update student set user = '王八蛋' where Telephonenumber=123456789012345678";
        //获取执行sql的对象Ststement
        Statement stem = con.createStatement();
        //执行sql
        int count = stem.executeUpdate(sql);
        //释放资源
        stem.close();
        con.close();
    }
}
```

Java的JDBC（Java Database Connectivity）是一组用于执行SQL语句的Java API，它为多种数据库提供了统一的访问方式。以下是JDBC编程中常用的一些类和接口的简要说明：

### 1. `java.sql.DriverManager`

- **作用**：管理数据库驱动程序的加载与注册。它是JDBC的入口点，用于建立与数据库的连接。
- **常用方法**：
  - `getConnection(String url, String user, String password)`：根据给定的数据库URL、用户名和密码建立数据库连接。
  - url语法：`jdbc:mysql://ip:端口/数据库名称`
  - 本机MySQL服务端口是3306，可以省略ip和端口号：`jdbc:mysql:///数据库名称`

### 2. `java.sql.Connection`
- **作用**：代表与数据库的连接。所有与数据库交互的操作都是基于这个连接对象进行的。
- **常用方法**：
  - `createStatement()`：创建一个`Statement`对象，用于执行静态SQL语句。
  - `prepareStatement(String sql)`：创建一个`PreparedStatement`对象，用于执行预编译的SQL语句。
  - `prepareCall(String sql)`：创建一个`CallableStatement`对象，用于调用数据库中的存储过程。
  - `close()`：关闭数据库连接。
  - `setAutoCommit(boolean autoCommit)`：开启事务
  - `commit()`：提交事务
  - `eollback()`：回滚事务

### 3. `java.sql.Statement`
- **作用**：用于执行静态SQL语句并返回结果的对象。
- **常用方法**：
  - `executeQuery(String sql)`：执行查询语句，并返回一个`ResultSet`对象。
  - `executeUpdate(String sql)`：执行INSERT、UPDATE或DELETE语句，返回受影响的行数。
  - `execute(String sql)`：执行SQL语句，根据不同的SQL类型返回不同的结果。

### 4. `java.sql.PreparedStatement`
- **作用**：预编译的`Statement`，比普通`Statement`更安全且性能更好，因为它允许参数化查询，防止SQL注入。
- **常用方法**与`Statement`类似，额外提供了设置参数的方法，如`setInt(int parameterIndex, int x)`等。

### 5. `java.sql.ResultSet`
- **作用**：保存查询结果的数据表，是一个游标指向型的数据集合。

- **常用方法**：
  - `next()`：移动到下一行。
  
  - `getString(int columnIndex)`、`getInt(int columnIndex)`等：获取当前行指定列的数据。
  
    ```java
    String sql1 = "select * from student";
    ResultSet set = stem.executeQuery(sql1);
    System.out.println(set.getString(2));
    System.out.println(set.getString("password"));
    ```
  
  - 遍历

### 6. `java.sql.SQLException`

- **作用**：JDBC操作中可能会抛出的异常，用于处理数据库访问过程中发生的错误。

### 7. `java.sql.CallableStatement`
- **作用**：用于调用数据库存储过程的接口，是`PreparedStatement`的子接口，具有预编译和参数化的特性。
- **常用方法**除了具备`PreparedStatement`的功能外，还提供了`registerOutParameter(int parameterIndex, int sqlType)`等方法来注册输出参数。

在实际开发中，使用JDBC进行数据库操作通常包括以下步骤：
1. 加载数据库驱动。
2. 通过`DriverManager.getConnection()`获取数据库连接。
3. 创建`Statement`、`PreparedStatement`或`CallableStatement`对象。
4. 执行SQL语句。
5. 处理`ResultSet`（如果有的话）。
6. 关闭资源（`ResultSet`、`Statement`、`Connection`）。

==注意，从Java 7开始，推荐使用try-with-resources语句来自动管理资源，确保即使在发生异常时也能正确关闭资源。==

```java
package com.jdbc;

import java.sql.*;

public class MysqlJdbc {
    public static void main(String[] args){
        Connection con =null;
        Statement stem = null;
        try {
            //注册驱动
            //Class.forName("com.mysql.cj.jdbc.Driver");
            //获取数据库连接对象
            con = DriverManager.getConnection("jdbc:mysql://localhost:3306/test", "root", "219798");
            //定义sql语句
            String sql = "update student set user = '王八' where Telephonenumber=123456789012345678";
            String sql1 = "select * from student";
            //获取执行sql的对象Ststement
            stem = con.createStatement();
            //执行sql
            //int count = stem.executeUpdate(sql);
            ResultSet set = stem.executeQuery(sql1);
            while (set.next()) {
                System.out.println(set.getString(2) + "-------" + set.getString("password"));
            }
            //释放资源
        } catch (SQLException e) {
            throw new RuntimeException(e);
        } finally {
        if (stem != null){
            try {
                stem.close();
            } catch (SQLException e) {
                throw new RuntimeException(e);
            }
        }
            if (con != null) {
                try {
                    con.close();
                } catch (SQLException e) {
                    throw new RuntimeException(e);
                }
            }
        }
    }
}
```

### 数据库连接池



## xml

### 基础

**概念：**可扩展标记语言

* 存储数据
  1. 配置文件
  2. 在网络中传输 

**语法：**

1. xml文档的后缀名.xml
2. xml第一行必须定义为文档声明
3. xml文档中有且仅有一个根标签
4. 性值必须使用引号(单双都可)引起来
5. 标签必须正确关闭
6. xml标签名称区分大小写

**组成部分：**

1. **文档声明**

   1. 格式:`<?xml属性列表?>`
   2. 属性列表:
      * version :版本号,必须的属性
      * encoding :编码方式。告知解析引擎当前文档使用的字符集,默认值: ISO-8859-1
      * standalone : 是否独立*取值:* yes :不依赖其他文件*no:依赖其他文件

2. **指令(了解):结合css的**

   `<?xml-stylesheet type="text/css" href="a.css" ?>`

3. **标签:标签名称自定义的**

   规则:

   1. 名称可以包含字母、数字以及其他的字符
   2. 名称不能以数字或者标点符号开始
   3. 名称不能以字母xml(或者XML、Xml等等)开始
   4. 名称不能包含空格

4. 属性:

   id属性值唯一

5. 文本:

   CDATA区:在该区域中的数据会被原样展示

   格式:`<![CDATA[数据]]>`

### 约束

规定xml文档的书写规则

* 作为框架的使用者(程序员)
  1. 能够在xml中引入约束文档
  2. 能够简单的读懂约束文档.

* 分类:
  1. DTD:一种简单的约束技术
  2. Schema:一种复杂的约束技术
* DTD :
  * 引入dtd文档到xml文档中
    * 内部dtd:将约束规则定义在xml文档中
    * 外部dtd:将约束的规则定义在外部的dtd文件中
      * 本地:`<!DOCTYPE 根标签名SYSTEM "dtd文件的位置">`
      *  网络:`<!DOCTYPE 根标签名PUBLIC "dtd文件名字”"dtd文件的位置URL">`

## Servlet

## Request

## Response

## ServletContext

## Session

## JSON

## AJAX

## redis

## Jedis

## Nginx
