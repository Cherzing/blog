---
title: MySQL
tag: 
  - SQL
date: 2023-09-08
cover: https://cdn.jsdelivr.net/gh/czlifetime/img/MySQL.png
---



# MySQL

服务启动与关闭：`net start mysql`,`net stop mysql`

连接到MySQL服务的指令：`mysql -h localhost -P 3306 -u root -pcz`

表的一行称之为一条记录，在java中，一行记录往往使用对象表示

## MySQL结构:

<strong>数据库的三层结构</strong>

+ 数据库管理系统(DBMS)
+ 数据库
+ 表

![](https://cdn.jsdelivr.net/gh/czlifetime/img/MySQL%E7%BB%93%E6%9E%84.jpg)

<strong>SQL语句的分类</strong>

+ DDL：数据定义语句[create]
+ DML：数据操作语句[增加insert，修改update，删除delete]
+ DQL：数据查询语句[select]
+ DCL：数据控制语句[管理数据库]

## 数据库

### 创建数据库

`CREATE DATABASE [IF NOT EXISTS];`

> 1. [DEFAULT] CHARACTER SET ：指定数据库采用的字符集，如果不指定字符集，默认utf-8
>
> 2. COLLATE：指定数据库字符集的校对规则（常用的utf8_bin(区分大小写)、utf8_general_ci(不区分大小写)）

### 筛选

`SELECT * FROM dbtest WHERE NAME = 'tom';`

### 查看、删除数据库

+ 显示数据库语句：

  `SHOW DATABASES`

+ 显示数据库创建语句：

  `SHOW CREATE DATABASE db_name;`

+ 数据库删除语句：

  `DROP DATABASE [IF EXITS] db_name;`

### 备份恢复数据库

+ 备份数据库(DOS命令行)

  `mysqldump -u 用户名 -p -B 数据库1 数据库2 数据库n > 文件名.sql`	

+ 恢复数据库

  `Sourse 文件名.sql`

## 表

### 创建

`CREATE TABLE table_name(`

`	field1 datatype,`	

`	field2 datatype,`

`	field3 datatype`

`)``character set 字符集 collate 校对规则 engine 存储引擎`

field:指定列名 

datatype: 指定列类型(字段类型)

character set:不指定为所在数据库字符集

collate：不指定为所在数据库校对规则

engine：引擎

### 删除&&修改

![](https://cdn.jsdelivr.net/gh/czlifetime/img/sql%20%E4%BF%AE%E6%94%B9%E8%A1%A8.jpg)

## MySql数据类型(列类型)

![](https://cdn.jsdelivr.net/gh/czlifetime/img/MySQl%E5%88%97%E6%95%B0%E6%8D%AE.png)

### 列类型的基本使用

#### 整型

1. 在满足需求的情况下，尽量选择占用空间小的类型

2. 如何定义一个无符号的整数

   unsigned

```sql
create table test01(
id tinyint
);

CREATE TABLE test02(
id tinyint unsigned
);

insert into test01 values(-128);
insert into test02 values(128);

select * from test01;
select * from test02;
```

#### bit

1. bit(m)，m在1~64之间
2. 添加数据范围
3. 显示按照bit

```sql
create table test03 (num bit (8));
insert into test03 values(255);
select * from test03;
```

#### 小数型

1. Float、double{}[unsigned]
2. decimal[M,D]\[unsigned]
   + 可以支持更加精确的小数位：M是小数位数（精度）的总和，D是小数点(标度)后面的位数
   + D=0，没有小数点或分数部分。
   + M最大为65，D最大是30
   + D被省略，为0，M被省略，默认是10

```sql
CREATE TABLE test04(
num1 FLOAT,
num2 DOUBLE,
num3 DECIMAL(20,10)
);
INSERT INTO test04 VALUE(1234567890.1234567890,1234567890.1234567890,1234567890.1234567890);
SELECT * FROM test04;
```

#### 字符串

+ 字符串的基本使用

  + CHAR(size)

    固定长度字符串，最大255字符

  + VARCHAR(size)

    可变长度字符串，最大65532字节

```sql
CREATE TABLE test05 (
	'name' CHAR(255));
```

细节：<mark>不区分是字符还是字节，具体的字节数要根据编码格式进行计算</mark>

+ `char(4)`，4表示字符数（最大255），不是字节数
+ `varchar(4)`，4表示字符数

> 细节：

> 1. 不管是中文还是英文，都是最多存放4个，是按照字符来存放
>2. <mark>`char(4)`是定长</mark>，不管插入几个字符，只会分配4个字符
> 3. <mark>`varchar(4)`是变长</mark>，按照实际占用的空间来分配
>+ `varchar`本身还需要占用1-3个字节来记录存放内容长度
> 4. + 如果数据是定长，推荐使用char，比如md5的密码,邮编，手机号，身份证号码等.char(32)
>   + 如果一个字段的长度是不确定，我们使用varchar ，比如留言，文章.
>    + 查询速度：char > varchar 
>5. 在存放文本时，也可以使用Text 数据类型.可以将TEXT列视为VARCHAR列,注意 Text 不能有默认值.大小 0-2^16 字节。如果希望存放更多字符，可以选择MEDIUMTEXT(0-2^24) 或者 LONGTEXT(0-2^32)

#### 日期

```sql
CREATE TABLE t1 (
  birthday DATE,
  job_time DATETIME,
  login_time TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
) ;

SELECT * FROM t1;
INSERT INTO t1(birthday,job_time) VALUE('2003-4-24','2026-3-1');
```



## CRUD(create、read、update、delete)

### Insert

![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20insert.jpg)

1. 插入的数据应与宁段的数据类型相同。
   比如 把 abo’ 添加到 int 类型会错误
2. 数据的长度应在列的规定范围内，例如: 不能将一个长度为80的字符串加入到长度为40的列中
3. 在values中列出的数据位置必须与被加入的列的排列位置相对应。
   字符和日期型数据应包含在单引号中。
4. 列可以插入空值[前提是该字段允许为空]，insert into table value (null)
5. insert into tab name (列名..) values (),),() 形式添加多条记录
6. 如果是给表中的所有字段添加数据，可以不写前面的字段名称
7. 默认值的使用，当不给某个字段值时，如果有默认值就会添加，否则报错

### Update

![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20update.jpg)

### Delete

![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20delete.jpg)

### Select

```sql
select [all|distinct]<目标列表达式>[,<目标列表达式>]
from <表名或视图名> [,<表名或视图名>]
[where <条件表达式>]
[group by<列名1>[having <条件表达式>]]
[order by<列名2>[ASC|DESC]]
```



#### 单表查询

1. 

![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQLselect1.jpg)

准备：

```sql 
 CREATE TABLE student(
id INT NOT NULL DEFAULT 1,
`name` VARCHAR(20) NOT NULL DEFAULT '',
chinese FLOAT NOT NULL DEFAULT 0.0,
English FLOAT NOT NULL DEFAULT 0.0,
Math FLOAT NOT NULL DEFAULT 0.0 
 );
 
INSERT INTO student (id,`name`,chinese,English,Math)VALUES(1,'曹志',99,99,99);
INSERT INTO student (id,`name`,chinese,English,Math)VALUES(2,'张三',89,78,86);
INSERT INTO student (id,`name`,chinese,English,Math)VALUES(3,'李四',76,87,56);
INSERT INTO student (id,`name`,chinese,English,Math)VALUES(4,'王五',87,56,76);
INSERT INTO student (id,`name`,chinese,English,Math)VALUES(5,'熊大',81,83,80);
INSERT INTO student (id,`name`,chinese,English,Math)VALUES(6,'熊二',71,72,73);
INSERT INTO student (id,`name`,chinese,English,Math)VALUES(7,'Tom',7,74,75);
```

select：

```sql
# 查询表中所有学生的信息
select * from student;
# 查询表中所有学生的姓名和对应的英语成绩
select `name`,English from student;
# 过滤表中重复数据 distinct
select distinct * from student;
```

2. 

使用表达式对查询的列进行运算

![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20select2-1.jpg)

在select语句中可使用as语句

![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20select2-2.jpg)

```sql
# 统计每个学生的总分
SELECT `name`, (English+Math+chinese) FROM student;
# 在所有学生总分加十分的情况
SELECT `name`, (English + Math + chinese + 10) FROM student;
# 使用别名表示学生分数
SELECT `name`, (English + Math + chinese + 10) AS `total` FROM student;
```

3. 

![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20select3-1.jpg)

```sql
# 查询姓名为赵云的学生成绩
SELECT * FROM student
	WHERE `name` = '张三';
# 查询英语成绩大于90分的同学
SELECT * FROM student 
	WHERE English > 90;
# 查询总分大于200分的所有同学
SELECT * FROM student
	WHERE (English+Math+chinese) > 200;
```

```sql
# 查询math大于60 并且(AND) id大于90的学生成绩
SELECT * FROM student
	WHERE Math > 60 AND id > 90;
# 查询英语成绩大于语文成绩的同学
SELECT *FROM student
	WHERE English > chinese;
# 查询总分大于200分 并且 数学成绩小于等于语文成绩，姓曹的学生.
SELECT * FROM student 
	WHERE (English+Math+chinese) > 200 AND Math <= chinese AND `name` LIKE '曹%';
```

#### 连接查询

#### 嵌套查询

#### 集合查询

#### 基于派生表的查询



##### 多表关系

项目开发中，在进行数据库表结构设计时，会根据业务需求及业务模块之间的关系，分析并设计表结构，由于业务之间相互关联，所
以各个表结构之间也存在着各种联系，基本上分为三种:

+ 一对多（多对一）
+ 多对多
+ 一对一

##### 多表查询概述

+ 笛卡尔积：

  笛卡尔乘积是指在数学中，两个集合A集合和 B集合的所有组合情况。(在多表查询时，需要消除无效的笛卡尔积)

##### 多表查询的分类

+ 连接查询

  + 内连接：相当于查询A、B交集部分数据

    + 隐式内连接：

      ![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20%E9%9A%90%E5%BC%8F%E5%86%85%E8%BF%9E%E6%8E%A5.jpg)

    + 显示内连接：

      ![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20%E6%98%BE%E7%A4%BA%E5%86%85%E8%BF%9E%E6%8E%A5.jpg)

  + 外连接

    ![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20%E5%A4%96%E8%BF%9E%E6%8E%A5%E6%9F%A5%E8%AF%A2.jpg)

    + 左外连接：查询左表所有数据，以及两张表交集部分数据
    + 右外连接：查询右表所有数据，以及两张表交集部分数据

  + 自连接：当前与自身的连接查询，自连接必须使用表别

    ![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20%E8%87%AA%E8%BF%9E%E6%8E%A5.jpg)

+ 子查询

  SQL语句中嵌套select语句，称为嵌套查询，又叫子查询

  ![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20%E5%AD%90%E6%9F%A5%E8%AF%A2.jpg)

  子查询外部的语句可以是insert、update、delete、select的任意一个

  + 标量子查询

    子查询返回的结果是单个值(数字、字符串、日期)，最简单的形式，这种子查询称为标量子查询

  + 列子查询

    子查询返回的结果是一列(可以是多行)

    > 操作符：
    >
    > IN、NOT IN、ANY、SOME、ALL
    >
    > ![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20%E5%88%97%E5%AD%90%E6%9F%A5%E8%AF%A2%E6%93%8D%E4%BD%9C%E7%AC%A6.jpg)

  + 行子查询

    子查询返回的结果是一行

  + 表子查询

    子查询返回的结果是多行多列

## 函数

### 统计函数

1. 合计/统计函数

   ![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20count.jpg)

   –> 返回行的总数 

```sql
# 函数
-- 合计函数
-- 统计一个班级共有多少学生
SELECT COUNT(*) FROM student;
-- 统计数学成绩大于90的学生有多少个
SELECT COUNT(*) FROM student
	WHERE Math > 90;
-- 统计总分大于250的人数有多少
SELECT COUNT(*) FROM student
	WHERE (English + Math + chinese) > 250;
-- count(*)和count(列)的区别
-- count(*) 返回满足条件的记录的行数
-- count(列): 统计满足条件的某列有多少个，但是会排除 为null
```

2. sum

![](https://cdn.jsdelivr.net/gh/czlifetime/img/sql%20sum.jpg)

![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20sum%E7%9A%84%E4%BD%BF%E7%94%A8.jpg)

3. avg

![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20avg.jpg)

![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20AVG%E7%9A%84%E4%BD%BF%E7%94%A8.jpg)

4. 合计函数

![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20min%E3%80%81max.jpg)

![](https://cdn.jsdelivr.net/gh/czlifetime/img/sql%20min%E3%80%81max%E7%9A%84%E4%BD%BF%E7%94%A8.jpg)

5. group by

![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20group%20by.jpg)

### 字符串函数

![](https://cdn.jsdelivr.net/gh/czlifetime/img/sql%20%E5%AD%97%E7%AC%A6%E4%B8%B2%E5%87%BD%E6%95%B0.jpg)

### 数学函数

![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20%E6%95%B0%E5%AD%A6.jpg)

### 时间日期

![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20%E6%97%B6%E9%97%B4%E6%97%A5%E6%9C%9F.jpg)

![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20%E6%97%B6%E9%97%B4%E6%97%A5%E6%9C%9F2.jpg)

### 加密和系统函数

![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20%E5%8A%A0%E5%AF%86%E5%92%8C%E7%B3%BB%E7%BB%9F%E5%87%BD%E6%95%B0.jpg)

### 流程控制

![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6%E5%87%BD%E6%95%B0.jpg)

## 约束

![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20%E7%BA%A6%E6%9D%9F%E7%9A%84%E5%88%86%E7%B1%BB.jpg)

<strong>外键约束</strong>

外键用来让两张表的数据之间建立连接，从而保证数据的一致性和完整性

<strong>添加外键约束的语法</strong>：

添加外键：

![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20%E5%A4%96%E9%94%AE%E8%AF%AD%E6%B3%95.jpg)

添加主键：

![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20%E5%88%A0%E9%99%A4%E5%A4%96%E9%94%AE.jpg)





外键的删除和更新行为

![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20%E5%A4%96%E9%94%AE%E7%9A%84%E5%88%A0%E9%99%A4%E5%92%8C%E6%9B%B4%E6%96%B0%E8%A1%8C%E4%B8%BA.jpg)

![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20%E7%BA%A6%E6%9D%9F%E8%A1%8C%E4%B8%BA%E6%93%8D%E4%BD%9C.jpg)

## 事务

### 事务简介

事务 是一组操作的集合，它是一个不可分割的工作单位，事务会把所有的操作作为一个整体一起向系统提交或撤销操作请求，即这些操作要么同时成功，要么同时失败

> 例：转账

### 事务操作

<strong>方式一</strong>

+ 查看/设置事务提交方式

  ```sql
  SELECT @@autocommit;
  SET @@autocommit = 0;
  ```

+ 提交事务

  ```sql 
  COMMIT;
  ```

+ 回滚事务

  ```sql
  ROLLBACK;
  ```

<strong>方式二</strong>

+ 开启事务

  ```sql 
  START TRANSACTION 或 BEGIN;
  ```

  

+ 提交事务

  ```sql 
  COMMIT;
  ```

  

+ 回滚事务

  ```sql
  ROLLBACK;
  ```

  

### 事务四大特性(ACID)

+ 原子性 (Atomicity): 事务是不可分割的最小操作单元，要么全部成功，要么全部失败。
+ 一致性(Consistency): 事务完成时，必须使所有的数据都保持一致状态。
+ 隔离性(lsolation): 数据库系统提供的隔离机制，保证事务在不受外部并发操作影响的独立环境下运行
+ 持久性 (Durability): 事务一旦提交或回滚，它对数据库中的数据的改变就是永久的。

### 并发事务问题

![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20%E5%B9%B6%E5%8F%91%E4%BA%8B%E5%8A%A1%E9%97%AE%E9%A2%98.jpg)

### 事务隔离级别

![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20%E4%BA%8B%E5%8A%A1%E9%9A%94%E7%A6%BB%E7%BA%A7%E5%88%AB.jpg)

```sql
查看事务隔离级别
SELECT @@TRANSACTION_ISOLATION
设置事务隔离级别
SET [SESSION|GLOBAL] TRANSACTION ISLATION LEVEL {READ UNCOMMITTED | READ COMMITTED | REPEATABLE READ | SERIALIZABLE}
```











> 附：
>
> ![](https://cdn.jsdelivr.net/gh/czlifetime/img/MySQL%E5%9F%BA%E7%A1%80%E5%AD%A6%E4%B9%A0%E5%A4%A7%E7%BA%B2.jpg)
>
> ![](https://cdn.jsdelivr.net/gh/czlifetime/img/MySQL%20%E9%AB%98%E7%BA%A7%E5%AD%A6%E4%B9%A0%E5%A4%A7%E7%BA%B2.jpg)