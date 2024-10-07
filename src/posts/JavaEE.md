---
title: JavaEE企业级开发实验1
date: 2024-10-7
cover: https://mybatis.net.cn/Application/Home/View/Public/img/mybatis-logo.png
tag:
  - JavaEE
  - 实验
  - MyBatis
---

工程目录

```plain
│  .gitignore
│  pom.xml
│
├─.idea
│
├─src
│  ├─main
│  │  ├─java
│  │  │  └─cn
│  │  │      └─cherzing
│  │  │          ├─pojo
│  │  │          │      Employee.java
│  │  │          │
│  │  │          └─util
│  │  │                  MybatisUtils.java
│  │  │
│  │  └─resources
│  │      │  db.properties
│  │      │  mybatis-config.xml
│  │      │
│  │      └─mapper
│  │              EmployeeMapper.xml
│  │
│  └─test
│      └─java
│              TestSelect.java
│
└─target
    ├─classes
    │  │  db.properties
    │  │  mybatis-config.xml
    │  │
    │  ├─cn
    │  │  └─cherzing
    │  │      ├─pojo
    │  │      │      Employee.class
    │  │      │
    │  │      └─util
    │  │              MybatisUtils.class
    │  │
    │  └─mapper
    │          EmployeeMapper.xml
    │
    ├─generated-sources
    │  └─annotations
    ├─generated-test-sources
    │  └─test-annotations
    └─test-classes
            TestSelect.class
```

Employee.java

```java
package cn.cherzing.pojo;

/**
 * @author Cherzing
 * @date 2024/09/28 0028 19:54
 * @description Employee
 */
public class Employee {
    private int id;
    private String name;
    private int age;
    private String position;

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getPosition() {
        return position;
    }

    public void setPosition(String position) {
        this.position = position;
    }

    @Override
    public String toString() {
        return "Employee{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", age=" + age +
                ", position='" + position + '\'' +
                '}';
    }
}

```

MyBatisUtils.java:

```JAVA
package cn.cherzing.util;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;
import java.io.InputStream;

/**
 * @author Cherzing
 * @date 2024/10/07 0007 13:49
 * @description MybatisUtils
 */
public class MybatisUtils {
    private static SqlSessionFactory sqlSessionFactory = null;
    static InputStream inputStream;

    static {
        try {
            inputStream = Resources.getResourceAsStream("mybatis-config.xml");
            sqlSessionFactory =
                    new SqlSessionFactoryBuilder().build(inputStream);
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }
    public static SqlSession getSqlSession(){
        return sqlSessionFactory.openSession();
    }
    public static void commitAndCloseSqlSession(SqlSession sqlSession){
        sqlSession.commit();
        sqlSession.close();
    }
}
```

EmployeeMapper.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="cn.cherzing.dao.EmployeeMapper">

    <select id="getEmployeeById" resultType="cn.cherzing.pojo.Employee">
        select * from employee where id = #{id}
    </select>

    <insert id="insertInfoEmployee" parameterType="cn.cherzing.pojo.Employee">
        insert into employee(name,age,position) values(#{name},#{age},#{position})
    </insert>

    <update id="updateEmployee" parameterType="cn.cherzing.pojo.Employee">
        update employee set name = #{name},age = #{age},position = #{position} where id = #{id}
    </update>

    <delete id="deleteEmployeeById" parameterType="Integer">
        delete from employee where id = #{id}
    </delete>
</mapper>
```

db.properties:

```plain
jdbc.driver=com.mysql.cj.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/test_mybates?serverTimezone=UTC
jdbc.username=root
jdbc.password=123456
```

mybatis-config.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
  PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <properties resource="db.properties"/>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="${jdbc.driver}"/>
                <property name="url" value="${jdbc.url}"/>
                <property name="username" value="${jdbc.username}"/>
                <property name="password" value="${jdbc.password}"/>
            </dataSource>
        </environment>
    </environments>
    <mappers>
        <mapper resource="mapper/EmployeeMapper.xml"/>
    </mappers>
</configuration>
```

