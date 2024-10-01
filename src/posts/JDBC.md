---
title: JDBC
tags: Java
data: 2023-9-9 10:40
cover: https://cdn.jsdelivr.net/gh/czlifetime/img/Java.jpg
---

# JDBC

## JDBC 简介

JDBC(<font color='red'>J</font>ava <font color='red'>D</font>ata<font color='red'>B</font>ase <font color='red'>C</font>onnectivity)(<font color='red'>Java数据库连接</font>)是java语言操作关系型数据库的一套API

## JDBC 入门

1. 创建工程，导入jar包

2. 注册驱动

   ```jav
   Class.forName("com.mysql.jdbc.Driver");
   ```

   

3. 获取连接

   ```java
   String url = "jdbc:mysql://127.0.0.1:3306/jdbc_test";
   String username = "root";
   String password = "cz";
   Connection conn = DriverManager.getConnection(url,username,password);
   ```

   

4. 定义SQL语句

   ```java
   String sql = "update account set money = 2000 where id =1";
   ```

   

5. 获取执行SQL对象

   ```java
   Statement statement = conn.createStatement();
   ```

   

6. 执行SQL

   ```java
   int count = statement.executeUpdate(sql);
   ```

   

7. 处理返回结果

   ```java
   System.out.println(count);
   ```

   

8. 释放资源

   ```java
   statement.close();
   conn.close();
   ```

   

## JDBC API 详解

### DriverManager

+ 作用
  + 注册驱动
  + 获取数据库连接

### Connection

+ 作用

  1. 获取执行SQL的对象

     + 普通执行SQL对象

        ```java
        Statement createStatement()
        ```

       

     + 预编译SQL的执行SQL对象：防止SQL注入

       ```java
       PreparedStatement prepareStatement(sql)
       ```

       

     + 执行存储过程的对象

       ```java
       CallableStatement prepaareCall(sql)
       ```

       

  2. 管理事务

     + MySQL事务管理

       ```SQL
       开启事务：BEGIN；/START TRANSACTION;
       提交事务：COMMIT;
       回滚事务：ROLLBACK;
       ```

       

     + JDBC事务管理

       ```java
       开启事务：setAutoCommit(boolean autoCommit):true为自动提交；FALSE为手动提交，几位开始事务
       提交事务:commit();
       回滚事务:rollback();
       ```

       

### Statement

+ 作用：

  1. 执行SQL语句

     ![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20statement.jpg)

### ResultSet

+ 封装了DQL语句查询结果

  ![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20resultset.jpg)

  ![](https://cdn.jsdelivr.net/gh/czlifetime/img/SQL%20result%E6%96%B9%E6%B3%95.jpg)

### PreparedStatement

未完：https://www.bilibili.com/video/BV1s3411K7jH?t=972.5&p=5

## 据库连接池

未完：https://www.bilibili.com/video/BV1s3411K7jH?t=972.5&p=5
