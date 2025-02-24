[toc]

# MySql

## 基础

* 本机MySQL用户名：root  密码：219798
* mysql --version,`select version()`：查看Mysql的版本号
* 查看数据库创建位置 `show variables like '%datadir%';`

## 基本操作

1. 服务启动关闭

   * 启动
     * 鼠标右击计算机-->管理-->服务和应用程序-->服务-->Mysql**MySQL服务名称**
     * 快捷键**win+r**-->cmd-->services.msc-->Mysql**MySQL服务名称**
     * 快捷键**win+r** 管理员启动-->cmd-->net start mysql**MySQL服务名称**
   * 关闭
     * 快捷键**win+r** 管理员启动-->cmd-->net stop mysql**MySQL服务名称**

2. 登录退出

   * 登录
     * cmd输入：mysql -u root -p **mysql -u 用户名 -p **--->密码
     * cmd输入：mysql -u root -p密码**mysql -u 用户名 -p密码**
     * 同网络下的其他电脑的MYSQL；cmd输入:mysql -h ip**连谁写谁的ip** -u 用户名 -p**链接的密码**
     * cmd输入：mysql --host=ip -user=用户名 -password=密码 
   * 退出
     * exit
     * quit

3. SQL基本概念

   * SQL：结构化操作语言
   * 查看数据库端口号：`show global variables like 'port';`

4. SQL通用语法

   1. 可以有单行或多行书写，以**；**结尾

   2. 以空格和缩进增加可读性

   3. 不区分大小写

      **注释**

      * -- 
      * # 
      * /* */

5. Navicat连接mysql报错 1251错误

   * 出现这个原因是mysql8 之前的版本中加密规则是mysql_native_password,而在mysql8之后,加密规则是caching_sha2_password
      解决办法：把mysql用户登录密码加密规则还原成mysql_native_password.

   1. 修改加密规则

      * 将加密方式改为mysql_native_password

      * `ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '12345';`

   2. 更新用户的密码

      * 这里将密码更改为password，如果想要更改其他密码，把password替换掉即可
      * `ALTER USER 'root'@'localhost' IDENTIFIED BY 'password' PASSWORD EXPIRE NEVER;`

   3.  进行刷新。

      * `FLUSH PRIVILEGES;`

6. SQL分类

   1. DDL(Data Definition Language)数据定义语言用来定义数据库对象:数据库,表，列等。关键字:create,drop,alter等
   2. DML(Data Manipulation Language)数据操作语言用来对数据库中表的数据进行增删改。关键字:insert, delete, update等3
   3. DQL(Data Query Language)数据查询语言用来查询数据库中表的记录(数据)。关键字:select, where 等
   4. DCL(Data Control Language)数据控制语言(了解) I

## 基本操作

1. c(Create):创建
   * 创建数据库: `create database 数据库名称;`
   * 创建数据库，判断不存在，再创建： `create database if not exists 数据库名称;`
   * 创建数据库，并指定字符集: `create database 数据库名称 character set 字符集名;`
   * 练习：创建db4数据库，判断是否存在，并制定字符集为gbk：`create database if not exists db4 character set gbk`
2. R(Retrieve): 查询
   * 查询所有数据库的名称：`show databases;`
   * 查询某个数据库的字符集:查询某个数据库的创建语句: `show create database 数据库名称;`
3.  U(Update):修改
   * 修改数据库的字符集:`alter database 数据库名称 character set 字符集名称;`
4.  D(Delete):删除
   * 删除数据库: `drop database 数据库名称;`
   * 判断数据库存在，存在再刪除: `drop database if exists 数据库名称;`
5. 使用数据库
   * 查询当前正在使用的数据库名称:`select database();`
   * 使用数据库:`use 数据库名称；`I

### 操作表

1. c(Create):创建

   * 语法

     ```mysql
     create table  /*表名*/)
     -- 列名1 数据类型1，
     -- 列名2 数据类型2，
     -- ·
     -- ·
     -- 列名n 数据类型n
     );
     -- 最后一行不加`,`
     ```
     
   * 例

     ```mysql
      create table student(
          user char(50),
          Telephonenumber varchar(120),
          password varchar(120),
          studentnumber char(50)
         );
     ```

   * 复制表结构

     ```mysql
     create table 新表名 like 原表名;
     ```

2. R(Retrieve):查询

   1. 查询某个数据库中所有的表名称:`show tables;`
   2. 查询表结构:`desc 表名;`、`DESCRIBE 表名` 或 `SHOW COLUMNS from 表名` 命令来查看表结构。
   2. `SHOW CREATE TABLE 表名` 命令会以 SQL 语句的形式来展示表信息。和 DESCRIBE 相比，SHOW CREATE TABLE 展示的内容更加丰富，它可以查看表的存储引擎和字符编码；另外，你还可以通过`\g`或者`\G`参数来控制展示格式。

3. U(Update):修改

   * 修改表名:

     ```mysql
     alter table 表名 rename to 新的表名;
     ```

   * 修改表的字符集:

     ```mysql
     alter table 表名character set字符集名称;
     ```

   * 添加一列:

     ```mysql
     alter table 表名 add 列名 数据类型;
     ```

   * 调整字段顺序

     ```mysql
     alter table 表名 change 字段名 新字段名 字段类型 默认值 after 字段名(跳到哪个字段之后)
     将id放在最前面字段
     alter table student modify id int(10) unsigned auto_increment first;
     ```

   * 修改列名称 类型:

     ```mysql
     alter table 表名 change 列名 新列名 新数据类型;
     alter table 表名 modify 列名 新数据类型;
     ```

   * 删除列

     ```mysql
     alter table 表名 drop 列名;
     ```

4. D(Delete):删除

   1. drop 是直接删除表信息，速度最快，但是无法找回数据：`drop table 表名`
   2. 判断是否纯在在删除：`drop table if exists 表名`
   3. if exists：是否存在；if not exists:不存在
   3. truncate 是删除表数据，不删除表的结构，速度排第二，但不能与where一起使用:`truncate table 表名;`

### 对数据的操作

1. 增加数据

   * 语法

     ```sql
     insert into student(列名,列名, 列名,列名)value (于列名相对应的数据，于列名相对应的数据，于列名相对应的数据，于列名相对应的数据);
     * 除了数字数据类型取余都需要使用''框起来
     ```

2. 删除数据

   * 语法

     ```sql
     delete from 表名 [where 条件]
     ```
     
   * 如果不加条件，则删除表中所有记录。

   * 如果要删除所有记录

     * delete from 表名；--不推荐使用。有多少条记录就会执行多少次删除操作
     * TRUNCATE TASLE 表名；--推荐使用，效率更高 先删除表，然后再创建一张一样的表。

3. 修改数据

   * ```sql
     update 表名 set 列名1 = 值1，列名2 = 值2，....[where 条件]；
     ```

   * 如果不加任何条件，则表中的数据全部被修改

4. 查询数据

   * 查询表中所有数据

     ```sql
     select * from 表名
     ```

   * 排序查询
   
     ```mysql
     select *from 表名 order by 排序字段1排序方式1,排序字段1排序方式1,....
     ```
   
     * 排序方式：升序，ASC，默认；降序DESC
     * 第一个排序字段一样按照第二个排序
   
   * 聚合函数：将一列数据作为一个整体，进行纵向的计算。
   
     聚合函数计算会排除null值
   
     1. count：计算个数
   
        `select count(字段名) from 表名；`
   
        `ifnull`非空
   
     2. max:计算最大值
   
        `select max(字段名) from 表名；`
   
     3. min :计算最小值
   
        `select min(字段名) from 表名；`
   
     4. sum：计算和
   
        `select sum(字段名) from 表名；`
   
     5. avg： 计算平均值
   
        `select avg(字段名) from 表名；`
   
   * 分组查询
   
     ```mysql
     select 分组后的字段，聚合函数 from 表名 Group by 分组字段；
     ```
   
     * where在分组之前限定，后不可以跟聚合函数；having在分组之后进行限定
   
   * 分页查询
   
     ```mysql
     select * from student limit 开始的索引，每页查询条数；
     例：
     select * from student limit （页码-1）*查询条数，3；
     ```
   
   * 基础查询
   
     ```mysql
     select 字段列表 from 表名列表 where 条件列表 group by 分组字段 having 分组之后的条件 order by 排序 limit 分页限定
     ```
   
     * 去除重复结果集
   
       `select DISTINCT 字段名 from 表名`DISTINCT去别名
   
     * 起别名
   
       `select DISTINCT 字段名 AS 别名 from 表名`字段名后面加AS后面跟别名
   
   * 条件查询
   
     where子句后跟条件
   
     运算符
   
     <、<=、>=、=、<>
   
     BETWEEN...AND：在之间的
   
     IN（ 集合）：里面有的
   
     LIKE：模糊查询
   
     IS NULL ：是空的，IS NOT NULL :不是空的
   
     and 或 && ：什么和什么
   
     or 或 || ：什么或者什么
   
     not 或 ！不相等的
   
   * 模糊查询
   
     like:模糊查询
   
     占位符`_`:占单个字符`%`：占多个字符
   
     ```mysql
     select * from 表名 like '_%';
     ```

### 约束

> 概念:对表中的数据进行限定,保证数据的正确性、有效性和完整性。

1. 主键约束: primary key

   含义：非空且唯一;一张表只能有一个字段为主键;主键就是表中记录的唯一标识

   * 在创建表时直接添加在字段后面呢
   * 删除非空约束：修改该字段`alter table 表名 drop primary key`
   * 创建表完成后添加`alter table 表名 modify 字段名 数据类型 primary key`

   自动增长:概念:如果某一列是数值类型的,使用 auto_increment可以来完成值得自动增长

   * 在创建表时直接添加在字段后面呢
   * 自动增长删除`alter table 表名 modify 字段名 数据类型`
   * 创建表完成后添加`alter table 表名 modify 字段名 数据类型 auto_increment`
   * PRI：主键约束；UNI：唯一约束；MUL可以重复。

2. 非空约束: not null

   * 在创建表时直接添加在字段后面呢
   * 删除非空约束：修改该字段`alter table 表名 modify 字段名 数据类型`
   * 创建表完成后添加`alter table 表名 modify 字段名 数据类型 not null`

3. 唯一约束:unique

   委员约束；唯一索引

   * 在创建表时直接添加在字段后面呢
   * 删除唯一约束：修改该字段`alter table 表名 drop index 字段名`
   * 创建表完成后添加`alter table 表名 modify 字段名 数据类型 unique`

4. 外键约束: foreign keyl

   ```mysql
   create table 表名（
   ......
   外键列 
   constraint 外键名称 foreign key (外键列名称) references 主表名称(主表列名称)
   );
   
   -- 添加外键
   ALTER TABLE `ese` ADD FOREIGN KEY (student_id) REFERENCES student (id);
   
   
   create table 表名（
   name char(11)  REFERENCES　user(id), -- 添加外键
   );
   ```
   
   * 删除外键`ALTER TABLE 表名 DRO P FOREIGN KEY 外键名称;`
   * 创建表之后,添加外键`ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (外键字段名称) REFERENCES 主表名称(主表列名称);`
   * 在创建外键时可以进行级联更新，级联删除
   * 直接写在后面：级联更新：ON UPDATE CASCADE；级联删除：ON DELETE CASCADE
   
5. 其他约束

   * 设置输入的字符只能说男或女`sex nvarchar(2) CHECK(student.sex=N'男' or student.sex=N'女');`

     　

### 多表联查

1. 数据库设计：多表关系
   * 一对一：可以在任意一方添加唯一外键指向另一方的主键。
   * 一对多：在多的一方建立外键，指向一的一方的主键。
   * 多对多：多对多关系实现需要借助第三张中间表。中间表至少包含两个字段，这两个字段作为第三张表的外键，分别指向两张表的主键。
   
2. 设计范式
   * 设计数据库时，需要遵循的一些规范。要遵循后边的范式要求，必须先遵循前边的所有范式要求；目前关系数据库有六种范式:第一范式（1NF） 、第二范式（2NF） 、第三范式（3NF） 、巴斯-科德范式（BCNF）、第四范式（4NF）和第五范式（5NF,又称完美范式）。
   * 第一范式（1NF）:每一列都是不可分割的原子数据项
   * 第二范式（2NF）在1NF的基础上,非码属性必须完全依赖于候选码(在1NF基础上消除非主属性对主码的部分函数依赖)
     * 函数依赖：
     * **A-->B，如果通过Als性（u性组）的值，可以确定唯一Bl性的值。则称B依赖于A**
       * 例如：学号-->姓名。（学号，课程名称） -->分数
     * **完全函数依赖:A-->B， 如果A是一个u性组，则Bl性值行确定 要依赖于A性组中所有的M性值。**
       * 例如：（学号，课程名称）--> 分数
     * **部分函数依赖：A-->B， 如果A是一个k性组，则Bl性值行确定只要依赖于Au性组中某一些值即可。**
       * 例如：（学号，课程名称）--> 姓名
     * **传递函数依赖：A-->B， B-->C.如果通过Ab性(成性组）的值，可以确定唯一B性的值，在通过Bl性（u性组）的值可以确定唯一C性的值，则称C传递函数依赖于A**
       * 例如：学号-->系名，系名-->系主任
     * **码:如果在一张表中,一个 性或以性组,被其他所有 性所完全依赖,则称这个 性(1性组)为该表的码**
       * 例如：该表中码为：（学号，课程名称）主属性：码性组中的所有属性；非主属性：除过码质性组的属性
   * 第三范式(3NF) :在2NF基础上,任何非主属性不依赖于其它非主属性(在2NF基础上消除传递依赖)
   
3. 数据库的备份与还原

   * 命令行：备份：mysqldump -u 用户名 -p 密码 备份的数据库名字> 保存的路径；还原：登录数据库-->创建数据库-->使用数据库-->执行文件source文件路径

4. 多表联查概述

   ==笛卡尔积：有两个集合A，B.取这两个集合的所有组成情况。要完成多表查询,需要消除无用的数据==

   * 外连接查询

     * 左外链接

       ```mysql
       语法: select字段列表 from 表 left [outer] join 表2 on条件;
       查询的是左表所有数据以及其交集部分。
       ```

     * 右外链接

       ```mysql
       语法: select字段列表 from 表1 right [outer] join 表2 on条件;
       查询的是右表所有数据以及其交集部分。
       ```

   * 内链接查询:从哪些表中查询数;据条件是什么;查询哪些字段

     * 隐式内连接:使用where条件消除无用数据例子：

       ```mysql
       -- 查询所有员工信息和对应的部门信息 ：
       SELECT * FROM emp,dept WHERE emp.`dept_id` = dept.`id`;
       -- 查询员工表的名称，性别。部门表的名称
       SELECT emp.name,emp.gender,dept.name FROM emp,dept WHERE emp.`dept_id` = dept.`id`;
       -- 查询员工表的名称，性别。部门表的名称
       select 
             t1.name,   -- 员工表的名称
             t1.gender, -- 员工表的性别
             t2.name    -- 部门表的名称
       from
             emp t1,
             dept t2
       where
             t1.`dept_id` = t2.`id`;
       ```

     * 显式内连接：

       ```mysql
        select 字段列表 from 表名1 [inner] join 表名2 on 条件
        例如：
        SELECT * FROM emp INNER JOIN dept ON emp.`dept_id` = dept. `id`;
        SELECT * FROM emp JOIN dept ON emp.`dept_id` = dept.`id`;
       ```

   * 子查询:

     * 查询中嵌套查询，称嵌套查询为子查询。

       ```mysql
       SELECT * FROM emp WHERE emp.`salary(SELECT MAX(salary) FROM emp);
       ```

     * 子查询的结果是单行单列的：==子查询可以作为条件，使用运算符去判断。 运算符：>>= < <= ===

     * 子查询的结果是多行单列的：==子查询可以作为条件，使用运算符in来判断==

     * 子查询的结果是多行多列的：==子查询可以作为一张虚拟表参与查询==

## 事务

* 事务的基本介绍
  * 概念：如果一个包拿多个步骤的业务操作，被事务管理，那么这些操作要么同时成功，要么同时失败。
  * 操作：
    * 开启事务:`start transaction;`
    * 回滚:`rollback;`
    * 提交:`commit;`
    * MySQL数据库中事务默认自动提交事务提交的两种方式：
      * 自动提交：mysql就是自动提交的一条DML(增删改)语句会自动提交一次事务。
      * 手动提交：Onacle 数据库默认是手动提交事务需要先开启事务，再提交
    * 修改事务的默认提交方式：
      * 查看事务的默认提交方式：SELECT @@autocommit; --1 代表自动提交 。 代表手动提交修改默认提交方式 ： set @@autocommit = 0;
  * 事务的四大特征
    * 原子性:是不可分割的最小操作单位,要么同时成功,要么同时失败。
    * 持久性：当事务提交或回滚后，数据库会持久化的保存数据。
    * 隔离性：多个事务之间。相互独立。
    * 一致性:事务操作前后,数据总量不变
  * 事务的隔离级别
  * 概念：多个事务之间隔离的，相互独立的。但是如果多个事务操作同一批数据，则会引发一些问题，设置不同的隔离级别就可以解决这些问题。
  * 存在问题：
    * 脏读:一个事务，读取到另一个事务中没有提交的数据
    * 不可重复读(虚读) :在同一个事务中,两次读取到的数据不一样。
    * 幻读:一个事务操作(DML)数据表中所有记录,另一个事务添加了一条数据,则第一个事务查询不到自己的修改。
  * 隔离级别：
    1. read uncommitted:读未提交产生的问题：脏读、不可重复读、幻读
    2. read committed：读已提交（oracle）产生的问题：不可重复读、幻读
    3. repeatable read:可重复读 （MySQL默认)产生的问题：幻读
    4. serializable:串行化可以解决所有的问题注意：隔离级别从小到大安全性越来越高，但是效率越来越低数据库
  * 查询隔离级别：`select @@tx_isolation;`数据库设置隔离级别：`set global transaction isolation level 级别字符串;`I

## 管理用户、授权

* 管理用户

  1. 添加用户：

     ```mysql
     -- 语法：
     CREATE USER '用户名'@'主机名' IDENTIFIED BY '密码'；
     ```

  2. 删除用户：

     ```mysql
     -- 语法：
     DROP USER'用户名'@'主机名'
     ```

  3. 修改用户密码

     ```mysql
     UPDATE USER SET PASSWORD = PASSWORD('新密码') WHERE USER = '用户名';
     UPDATE USER SET PASSWORD = PASSWORD('abc') WHERE USER = 'lisi';
     SET PASSWORD FOR '用户名' @ '主机名' = PASSWORD('新密码');
     SET PASSWORD FOR 'root' @ 'localhost' = PASSWORD('123');
     ```

     忘记mysql管理员密码

     ```mysql
     -- 管理员打开cmd，停止mysql服务，使用无验证登录
     mysqld --skip-grant-tables
     -- 打开新的cmd窗口，直接输入mysql命令，敲回车。就可以登录成功
     use mysql;
     update user set password = password("你的新密码") where user = "root";
     -- 关闭两个窗口
     -- 打开任务管理器,手动结束mysqld.exe的进程
     -- 启动mysql服务
     -- 使用新密码登录。
     ```

  4. 查询用户

     ```mysql
     -- 1.切挟到mysq1数据库
     USE myql;
     -- 2. 查询user表
     SELECT * FROM USER;
     -- 通配符：％ 表示可以在任意主机使用用户登录数据库
     ```

* 授权

  ```mysql
  -- 查询权限：
  SHOW GRANTS FOR '用户名'@'主机名';
  SHOW GRANTS FOR 'lisi'@'%';
  -- 授予权限：
  grant 权限列表 on 数据库名.表名 to '用户名' @ '主机名';
  # 给张三用户授予所有权限，在任意数据库任意表上
  GRANT ALL ON *.* TO 'zhangsan' @ 'localhost';
  -- 撤销权限：
  revoke 权限列表 on 数据库名.表名 from '用户名' @ '主机名';
  ```



## 数据类型

主要包括以下五大类：

1. 整数类型：BIT、BOOL、TINY INT、SMALL INT、MEDIUM INT、 INT、 BIG INT

2. 浮点数类型：FLOAT、DOUBLE、DECIMAL

3. 字符串类型：CHAR、VARCHAR、TINY TEXT、TEXT、MEDIUM TEXT、LONGTEXT、TINY BLOB、BLOB、MEDIUM BLOB、LONG BLOB

4. 日期类型：Date、DateTime、TimeStamp、Time、Year

5. 其他数据类型：BINARY、VARBINARY、ENUM、SET、Geometry、Point、MultiPoint、LineString、MultiLineString、Polygon、GeometryCollection等

   > 使用原则

1. 在指定数据类型的时候一般是采用从小原则，比如能用TINY INT的最好就不用INT，能用FLOAT类型的就不用DOUBLE类型，这样会对MYSQL在运行效率上提高很大，尤其是大数据量测试条件下。
2. 不需要把数据表设计的太过复杂，功能模块上区分或许对于后期的维护更为方便，慎重出现大杂烩数据表
3. 数据表和字段的起名字也是一门学问
4. 设计数据表结构之前请先想象一下是你的房间，或许结果会更加合理、高效
5. 数据库的最后设计结果一定是效率和可扩展性的折中，偏向任何一方都是欠妥的

| 用途                       | 数据类型     | 大小                                                         |
| -------------------------- | ------------ | ------------------------------------------------------------ |
| 整数类型                   | TINY INT     | 1个字节 范围(-128~127)                                       |
|                            | smallint(m)  | 2个字节 范围(-32768~32767)                                   |
|                            | mediumint(m) | 3个字节 范围(-8388608~8388607)                               |
|                            | int(m)       | 4个字节 范围(-2147483648~2147483647)                         |
|                            | bigint(m)    | 8个字节 范围(+-9.22*10的18次方)                              |
|                            |              | 取值范围如果加了unsigned，则最大值翻倍，如tinyint unsigned的取值范围为(0~256)。int(m)里的m是表示SELECT查询结果集中的显示宽度，并不影响实际的取值范围，没有影响到显示的宽度，不知道这个m有什么用。 |
| 浮点型(float和double)      | float(m,d)   | 单精度浮点型  8位精度(4字节)   m总个数，d小数位              |
|                            | double(m,d)  | 双精度浮点型  16位精度(8字节)   m总个数，d小数位             |
|                            |              | 设一个字段定义为float(6,3)，如果插入一个数123.45678,实际数据库里存的是123.457，但总个数还以实际为准，即6位。整数部分最大是3位，如果插入数12.123456，存储的是12.1234，如果插入12.12，存储的是12.1200. |
| 定点数                     | decimal(m,d) | 参数m<65 是总个数，d<30且 d<m 是小数位。                     |
|                            |              | 浮点型在数据库中存放的是近似值，而定点类型在数据库中存放的是精确值。 |
| 字符串(char,varchar,_text) | char(n)      | 固定长度，最多255个字符                                      |
|                            | varchar(n)   | 固定长度，最多65535个字符                                    |
|                            | tinytext     | 可变长度，最多255个字符                                      |
|                            | text         | 可变长度，最多65535个字符                                    |
|                            | mediumtext   | 可变长度，最多2的24次方-1个字符                              |
|                            | longtext     | 可变长度，最多2的32次方-1个字符                              |
| 日期时间类型               | date         | 日期 '2008-12-2'                                             |
|                            | time         | 时间 '12:25:36'                                              |
|                            | datetime     | 日期时间 '2008-12-2 22:06:44'                                |
|                            | timestamp    | 自动存储记录修改时间                                         |
|                            |              | 若定义一个字段为timestamp，这个字段里的时间数据会随其他字段修改的时候自动刷新，所以这个数据类型的字段可以存放这条记录最后被修改的时间。 |

> char和varchar

1. char(n) 若存入字符数小于n，则以空格补于其后，查询之时再将空格去掉。所以char类型存储的字符串末尾不能有空格，varchar不限于此。 
2. char(n) 固定长度，char(4)不管是存入几个字符，都将占用4个字节，varchar是存入的实际字符数+1个字节（n<=255）或2个字节(n>255)，**所以varchar(4),存入3个字符将占用4个字节。** 
3. char类型的字符串检索速度要比varchar类型的快。

> varchar和text

1. varchar可指定n，text不能指定，内部存储varchar是存入的实际字符数+1个字节（n<=255）或2个字节(n>255)，text是实际字符数+2个字节。 
2. text类型不能有默认值。 
3. varchar可直接创建索引，text创建索引要指定前多少个字符。varchar查询速度快于text,在都创建索引的情况下，text的索引似乎不起作用。

>二进制数据(_Blob)

1. `_BLOB和_text`存储方式不同，`_TEXT`以文本方式存储，英文存储区分大小写，而`_Blob`是以二进制方式存储，不分大小写。
2. `_BLOB`存储的数据只能整体读出。 
3. `_TEXT`可以指定字符集，`_BLO`不用指定字符集。

# Mysql高级

## 索引

1. **为什么使用索引**
   * 在海量数据中进行查询某条记录的场景是经常发生的，那么如何提升查询性能，就跟要查询的数据字段是否有索引有关系。如果字段加了索引，那么查洵的性能就非常快！

2. **索引是什么**
   * 为数据库的某个字段创建索引，相当是为这个字段的内容创建了一个目录。通过这个目录可以快速的实现数据的定位，也就是通过索引能鸲快速的找到某条据所在磁盘的位置。

4. **索引存储位置**
   * 对于 mac 系统在`/usr/local/mysql`文件夹中，对于 win系统`c:/programdata/mysql(隐藏文件夹)`
     * InnoDB 存储引擎的表：将索引和数据存放在同一个文件里。`*.ibd`
     * MylSAM 存引擎的表：索引和数据分开两个文件来存储·索引：`*.MYI;数据:MYD`

5. **索引的分类**
   * 主键索引
   * 普通索引
   * 唯一索引
   * 组合索引
   * 全文索引

### InnoDB和MyISAM的区别

# 主从部署

**环境准备**

- **Master（主库）**: IP 地址为 `192.168.1.10`
- **Slave（从库）**: IP 地址为 `192.168.1.11`

确保两台服务器上已经安装了 MySQL，并且版本一致。

**配置 Master（主库）**

* 修改 MySQL 配置文件

* 编辑 MySQL 的配置文件（通常是 `/etc/my.cnf` 或 `/etc/mysql/my.cnf`），添加或修改以下内容：

   ```sql
   [mysqld]
   server-id=1                  # 设置唯一的 server-id
   log-bin=mysql-bin            # 开启二进制日志
   binlog-do-db=test_db         # 指定需要同步的数据库（可选）、如果需要同步所有数据库，可以省略 `binlog-do-db`。
   binlog-format=row            # 使用基于行的日志格式
   ```

* 保存后重启 MySQL 服务：

   ```bash
   systemctl restart mysql
   ```

* 创建用于复制的用户

* 在 Master 上创建一个专门用于主从复制的用户：

   ```sql
   CREATE USER 'repl'@'%' IDENTIFIED BY 'password';
   GRANT REPLICATION SLAVE ON *.* TO 'repl'@'%';
   FLUSH PRIVILEGES;
   ```

* 获取二进制日志位置

* 在 Master 上执行以下命令，获取当前的二进制日志文件名和位置：

   ```bash
   SHOW MASTER STATUS;
   # 输出示例：
   +------------------+----------+--------------+------------------+
   | File             | Position | Binlog_Do_DB | Binlog_Ignore_DB |
   +------------------+----------+--------------+------------------+
   | mysql-bin.000003 | 12345    | test_db      |                  |
   +------------------+----------+--------------+------------------+
   # 记录下 `File` 和 `Position` 的值，稍后在 Slave 上会用到。
   ```

 **配置 Slave（从库）**

* 修改 MySQL 配置文件

* 编辑 MySQL 的配置文件，添加或修改以下内容：

   ```sql
   [mysqld]
   server-id=2                  # 设置唯一的 server-id
   relay-log=mysql-relay-bin    # 开启中继日志
   log-slave-updates=1          # 允许从库写入二进制日志（可选）
   read-only=1                  # 设置从库为只读（可选）
   ```

* 保存后重启 MySQL 服务：

   ```bash
   systemctl restart mysql
   ```

*  配置主从关系

* 在 Slave 上执行以下 SQL 命令，配置主从关系：

   ```sql
   CHANGE MASTER TO
   MASTER_HOST='192.168.1.10',       -- Master 的 IP 地址
   MASTER_USER='repl',               -- 复制用户的用户名
   MASTER_PASSWORD='password',       -- 复制用户的密码
   MASTER_LOG_FILE='mysql-bin.000003', -- Master 的二进制日志文件名
   MASTER_LOG_POS=12345;             -- Master 的二进制日志位置
   ```

*  启动从库同步

* 启动从库的同步功能：

   ```sql
   START SLAVE;
   ```

* 检查同步状态：

   ```sql
   SHOW SLAVE STATUS\G
   # 重点关注以下字段：
   #  `Slave_IO_Running`: 应为 `Yes`。
   #  `Slave_SQL_Running`: 应为 `Yes`。
   #  `Last_Error`: 如果为空，则表示没有错误。
   ```

**测试主从同步**

* 在 Master 上插入一些数据，检查 Slave 是否能实时同步。

   ```sql
   # 在 Master 上：
   USE test_db;
   CREATE TABLE test_table (id INT, name VARCHAR(50));
   INSERT INTO test_table VALUES (1, 'Test');
   # 在 Slave 上：
   USE test_db;
   SELECT * FROM test_table;
   # 如果能够看到插入的数据，则说明主从同步成功。
   ```

**常见问题及解决方法**

1. 问题 1: `Slave_IO_Running` 或 `Slave_SQL_Running` 为 `No`

   * 检查 Master 和 Slave 的网络连接是否正常。
   * 检查 `SHOW SLAVE STATUS\G` 中的 `Last_Error` 字段，根据错误信息进行排查。

2. 问题 2: 数据不一致

   * 确保 Master 和 Slave 的初始数据一致。可以通过备份 Master 的数据并导入到 Slave 来实现：

      ```sql
      mysqldump -u root -p --all-databases > backup.sql
      ```

   * 将 `backup.sql` 文件传输到 Slave 并导入：

      ```sql
      mysql -u root -p < backup.sql
      ```

   * 问题 3: 主从延迟：如果发现主从同步有延迟，可以优化网络、增加硬件资源，或者调整 MySQL 配置。

**扩展：读写分离**

为了进一步提高性能，可以结合读写分离技术，将写操作发送到 Master，读操作发送到 Slave。可以通过以下方式实现：
- 手动分配读写请求。
- 使用代理工具（如 ProxySQL 或 MaxScale）自动分发请求。



