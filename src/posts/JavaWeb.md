---
title: JavaWeb
date: 2023-09-09
cover: https://cdn.jsdelivr.net/gh/czlifetime/img/javaweb.jpeg
tag:
  - Java
---

# JavaWeb

## JavaWeb的概念

是指，所有通过Java语言编写可以通过浏览器访问的程序的总称

是基于<strong>请求</strong>和<strong>响应</strong>开发的

+ 请求：客户端给服务器发送数据，Request
+ 响应：服务器给客户端回传数据，Response
+ 响应与请求的关系：成对出现

## Web资源的分类

+ 静态资源：html、css、js、txt、mp4、jpg
+ 动态资源：jsp页面，Servlet程序

## 反射：框架设计的灵魂

+ 框架：半成品软件，可以在框架的基础上进行软件的开发，简化代码

+ 反射：将类的各个组成部分封装为其他对象

  ![](https://cdn.jsdelivr.net/gh/czlifetime/img/JavaWeb%E5%8F%8D%E5%B0%84.png)

  + 好处：
    1. 可以在程序运行的过程中，操作这些对象
    2. 可以解耦，提高程序的可扩展性

## Maven

Maven是专门用于管理和构建Java项目的工具，它的主要功能有

+ 提供了一套标准化的项目结构
+ 提供了一套标准化的构建流程 (编译，测试，打包，发布......)
+ 提供了一套依赖管理机制

<strong>常用命令</strong>

+ compile
+ clean 
+ test
+ package
+ install

### maven坐标

+ 是资源的唯一标识
+ 使用坐标来定义项目或引入项目中的依赖

<strong>组成</strong>

+ groupID：定义当前Maven项目隶属组织名称
+ artifactID：定义当前Maven项目名称
+ version：定义当前项目版本号

### <strong>依赖</strong>

需要使用到的相关jar包

<strong>依赖范围</strong>

\<scope>\</scope>

通过设置坐标的依赖范围（scope），可以设置对应jar包的作用范围：编译环境、测试环境、运行环境

![](https://cdn.jsdelivr.net/gh/czlifetime/img/maven%20%E4%BE%9D%E8%B5%96%E8%8C%83%E5%9B%B4.jpg)

<strong>排除依赖</strong>

\<exclusiom>\</exclusion>

<strong>生命周期</strong>

3套相互独立的生命周期

+ clean：清理工作
+ default:核心工作(编译、测试、打包、安装、部署)
+ site:生成报告。发布站点

![](https://cdn.jsdelivr.net/gh/czlifetime/img/Maven%20%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E7%9A%84%E9%98%B6%E6%AE%B5.jpg)

> 在同一套生命周期中，当运行后面的阶段时，前面的阶段都会运行





## SSM框架

SSM框架是spring、spring MVC和mybatis框架的整合，是标准的MVC模式。标准的SSM框架有四层，分别是DAO(Mapper)层、Service层、Controller层和View层。使用spring实现业务对象管理，使用spring MVC负责请求的转发和视图管理，mybatis作为数据对象的持久化引擎

### 持久层(Mapper/DAO)

主要是做数据持久层的工作，负责与数据库进行联络的一些任务都封装在此。

+ Dao层首先设计的是接口，然后再Spring的配置文件中定义接口的实现类
+ 然后可以在模块中进行接口的调用来进行数据业务的处理。 (不在关心接口的实现类是哪个类)
+ 数据源的配置以及有关数据库连接的参数都在Spring的配置文件中进行配置

### 业务层(Service)

业务模块的逻辑应用设计

+ 先设计接口然后再设计实类，然后再在Spring的配置文件中配置其实现的关联。(业务逻辑层的实现具体要调用到自己已经定义好的Dao的接口上)这样就可以在应用中调用Service接口来进行业务处理。
+ 建立好Dao之后再建立service层，service层又要在controler层之下，因为既要调用Dao层的接口又要提供接口给controller层。每模型都有一个service接口，每个接口分别封装各自的业务处理的方法。

### 表现层(Controller)

负责具体的业务模块流程控制

+ 配置也同样是在Spring的配置文件里面进行的
+ 调用Service层提供的接口来控制业务流程
+ 业务流程的不同会有不同的控制器，在具体的开发中可以将我们的流程进行抽象的归纳，设计出可以重复利用的子单元流程模块

#### View层

主要和控制层紧密结合，主要负责前台jsp页面的表示

### 三层架构

+ Controller：控制层，接收前端发送的请求，对请求进行处理，并响应数据
+ Service：业务逻辑层，处理具体的业务逻辑
+ Dao：数据访问层(Data Access Object)(持久层)，负责数据访问操作，包括数据的增、删、改、查

![](https://cdn.jsdelivr.net/gh/czlifetime/img/JavaWeb%E4%B8%89%E5%B1%82%E6%9E%B6%E6%9E%84.png)

### Spring

1. IOC(控制反转Inversion of Control)

   不是技术，是一种设计思想。意味着，将设计好的对象，交给容器控制，而不是传统的在对象内部直接控制

2. AOP(面向切面Aspect Oriented Programming)

   也是一种程序设计规范，旨在将横切关注点与业务逻辑分离

#### 分层解耦

+ 内聚：软件中各个功能模块内部的功能练习

+ 耦合：衡量软件中各个层/模块之间的依赖、关联的程度

  > 软件设计原则：高内聚、低耦合

#### 

#### IOC& DI入门

+ IOC->控制反转：对象的创建控制权由程序自身转移到外部(容器),这种思想称为控制反转
+ DI->依赖注入：容器为应用程序提供运行时，所依赖的资源，称之为依赖注入
+ Bean对象：IOC容器中创建、管理的对象，称之为bean

#### IOC详解

#### DI详解

### MyBatis

<strong>[MyBatis教程](https://mybatis.org/mybatis-3/zh/getting-started.html)</Strong>

是一款优秀的持久层框架，用于简化JDBC开发

<strong>持久层</strong>

+ 负责将数据保存大数据库的那一层代码
+ JavaEE三层架构：表现层、业务层、持久层

<strong>框架</strong>

+ 是一个半成品软件，是一套可重用、通用的、软件基础代码模型
+ 在框架的基础上构建软件更加高效、规范、通用、可拓展。

#### 快速入门

```java
package org.lifetime.pojo;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;
import java.io.InputStream;
import java.util.List;

public class test {
    public static void main(String[] args) throws IOException {
        
        //1. 加载核心配置文件，获取SQLSessionFactory对象
        String resource = "mybatis-config.xml";
        InputStream inputStream = Resources.getResourceAsStream(resource);
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);

        //2. 获取SQLSession对象
        SqlSession sqlSession = sqlSessionFactory.openSession();

        //3. 执行SQL语句
        List<User> users = sqlSession.selectList("test.selectAll");
        System.out.println(users);
        
        //4. 释放资源
        sqlSession.close();
    }
}

```



#### Mapper代理开发

<strong>目的</strong>

+ 解决原生方式中的硬编码
+ 简化后期执行SQL

<strong>Mapper代理步骤：</strong>

1. 定义SQL映射文件同名的Map普洱接口，并且将Mapper接口和SQL映射文件方式在同一目录下
2. 设置SQL映射文件的namespace属性为Mapper接口全限定名
3. 在Mapper接口中定义方法，方法名就是SQL映射文件中SQL语句的ID，并保持参数类型和返回值类型一致
4. 编码：
   1. 通过SqlSession的getMapper方法获取Mapper接口的代理对象
   2. 调用对应方法完成SQL的执行

#### MyBatis核心配置文件

```sql
# 配置数据库的连接信息 -- 四要素
# 驱动类名称
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
# 数据库连接的url
spring.datasource.url=jdbc:mysql://localhost:3306/mybatis
# 连接数据库的用户名
spring.datasource.username=root
# 连接数据库的密码
spring.datasource.password=1234
```

#### lombok

+ Lombok是一个使用的Java类库，能通过注解的形式自动生成构造器getter/setter、equals、hashcode、toString等方法，并可以自动化生成日志变量，简化Java开发、提高效率

| 注解                | 作用                                                         |
| ------------------- | ------------------------------------------------------------ |
| @Getter/@Setter     | 为所有的属性提供get/set方法                                  |
| @ToString           | 会根据类自动生成易阅读的toString方法                         |
| @EqualsAndHashCode  | 根据类所拥有的非静态字段自动重写equals方法和hashCode方法     |
| @Data               | 提供更综合的生成代码功能(@Getter+@Setter+@ToString+@EqualsAndHashCode) |
| @NoArgsConstructor  | 为实体类生成无参的构造方法                                   |
| @AllArgsConstructor | 为实体类生成除了static修饰的字段之外带有各参数的构造器方法   |

#### 注解完成增删改查(RUID)

##### Delete

+ 预编译SQL

  + 性能更高

  + 更安全、防止SQL注入

    + SQL注入：通过操作输入的数据来修改事先定义好的SQL语句，以达到执行代码对服务器进行攻击的方法`password = ' or '1' = '1`

      > 参数占位符：
      >
      > + `#{...}`
      >   + 执行SQL时，会将`#{...}`替换为？，生成预编译SQL，会自动设置参数值
      >   + 使用时机：参数传递，都使用`#{...}`
      > + `${…}`
      >   + 拼接SQL。直接将参数拼接在SQL语句中，存在SQL注入问题
      >   + 使用时机：如果对表名、列表进行动态设置使用

##### Insert

##### Update

##### Select

+ 当SQL的字段与实体类的属性不一致

  + 给字段起别名，让别名与实体类属性一致

    ![](https://cdn.jsdelivr.net/gh/czlifetime/img/JavaWeb%E6%9F%A5%E8%AF%A2%E4%B8%BA%E7%A9%BA%E6%97%B61.png)

  + 通过`@Results`,手动映射封装

    ![](https://cdn.jsdelivr.net/gh/czlifetime/img/JavaWeb%E6%9F%A5%E8%AF%A2%E4%B8%BA%E7%A9%BA%E6%97%B62.png)

  + 打开mybatis的驼峰命名自动映射开关

    `application.properties`文件中：`mybatis.configuration.map-underscore-to-camel-case=true`

```java
//根据ID删除数据
    @Delete("delete from emp where id = #{id}")
    public void delete(Integer id);
    //public int delete(Integer id);

    //新增员工
    @Options(useGeneratedKeys = true, keyProperty = "id")
    @Insert("insert into emp(username, name, gender, image, job, entrydate, dept_id, create_time, update_time)" +
            " values (#{username},#{name},#{gender},#{image},#{job},#{entrydate},#{deptId},#{createTime},#{updateTime})")
    public void insert(Emp emp);

    //更新员工
    @Update("update emp set username = #{username}, name = #{name}, gender = #{gender}, image = #{image}," +
            " job = #{job}, entrydate = #{entrydate}, dept_id = #{deptId},update_time = #{updateTime} where id = #{id}")
    public void update(Emp emp);
```

#### 配置文件完成增删改查(XML)

+ XML映射文件的名称与Mapper接口名称一致，并且将XML映射文件和Mapper接口放置在相同包下(同包同名)
+ XML映射文件的namespace属性为Mapper接口全限定名一致
+ XML映射文件中的SQL语句的id与Mapper接口中的方法名一致，并保持返回类型一致

#### Mybatis动态SQL

+ \<if>：用于判断条件是否成立。使用test属性进行条件判断，如果条件为true，则拼接SQL

  ![](https://cdn.jsdelivr.net/gh/czlifetime/img/JavaWeb%20mybatis%20if.png)

+ \<where>：只会在子元素有内容的情况下才会插入where子句。而且会自动去除子句的开头的AND或OR

+ \<set>：动态地在行首插入set关键字，并会删除掉额外的逗号(用在Update语句中)

+ \<foreach>

  + collection：遍历的集合
  + item：遍历出来的元素
  + separator：分隔符
  + opean：遍历开始前拼接的SQL片段
  + close：遍历结束后拼接的SQL片段

+ \<sql>：定义可重用的SQL片段

+ \<include>：通过属性refid，指定包含的SQL片段

## SpringBoot

### SpringBootWeb入门

1. 创建springboot工程，并勾选web开发相关依赖。
2. 定义HelloController类，添加方法 hello，并添加注解
3. 运行测试

### HTTP协议

#### 概述

`Hyper Text Transfer Protocol`，超文本传输协议，规定了浏览器和服务器之间数据传输的规则

特点：

+ 基于TCP协议：面向连接，安全
+ 基于请求-响应模型的：一次请求对应一次相应
+ HTTP协议是无状态的协议：对于事务处理没有记忆能力
  + 缺点：多次请求之间不能共享数据
  + 优点：速度快

#### 请求协议

> 请求数据的格式

![](https://cdn.jsdelivr.net/gh/czlifetime/img/http%E8%AF%B7%E6%B1%82%E6%95%B0%E6%8D%AE%E6%A1%88%E4%BE%8B.jpg)

还有请求体

| Host            | 请求的主机名                                           |
| --------------- | ------------------------------------------------------ |
| User-Agent      | 浏览器版本                                             |
| Accept          | 表示浏览器能接收到的资源类型                           |
| Accept-Language | 表示浏览器偏好的语言，服务器可以据此返回不同语言的网页 |
| Accept-Encoding | 表示浏览器可以支持的压缩类型                           |
| Content-Type    | 请求主体的数据类型                                     |
| Content-Length  | 请求主体的大小                                         |

例如：

![](https://cdn.jsdelivr.net/gh/czlifetime/img/%E7%BD%91%E5%9D%80%E8%AF%B7%E6%B1%82.png)

#### 相应协议

![](https://cdn.jsdelivr.net/gh/czlifetime/img/http%E7%9B%B8%E5%BA%94%E6%A0%BC%E5%BC%8F.jpg)

![](https://cdn.jsdelivr.net/gh/czlifetime/img/http%E7%9B%B8%E5%BA%94%E5%A4%B4.jpg)

常见状态码：

+ 200： 客户端请求成功
+ 404： 请求资源不存在
+ 500： 服务器发生不可预期的错误

#### 协议解析

http(Hyper Text Transfer Protocol)超文本传输协议

### Web服务器

是一个软件程序，对HTTP协议的操作进行封装，使得程序员不必直接对协议进行操作，让Web开发更加便捷。主要的功能是“提供网上信息浏览服务”

#### 请求（各类请求参数的接收和封装）

> HTTP的八种请求方式
>
> 1. GET：向服务器请求指定的资源
> 2. POST：向服务器提交数据请求处理，数据被包含在请求体中
> 3. HEAD：返回服务器上对指定资源数据的HTTP请求头，在不需要2返回全部数据的地方
> 4. OPTIONS：返回服务器对指定资源数据支持的HTTP请求方法，一般用于测试服务器功能的可用性
> 5. PUT：向服务器上传指定的数据
> 6. DELETE：向服务器发送请求删除指定数据
> 7. TRANCE：回显服务器收到的请求，主要进行功能测试诊断
> 8. CONNECT：HTTP1.1协议中预留请求方式，可以将连接改为管道方式的代理服务器
>
> 常见的请求方式：
>
> 1. POST：添加
> 2. GET：查询
> 3. DELETE：删除
> 4. PUT：修改
>
> > <strong><mark>注解</mark></strong>
>
> > `@RequestBody`注解的主要作用是接收前端的参数，当我们使用POST请求是，会将参数放在Request Body中，此时我们就需要再Controller的方法参数面前加上@RequestBody用来接收到前端传过来的RequestBody的值
> >
> > ```java
> > @Controller
> > @RequestMapping（“/test”）
> > public class test{
> >  
> > public void testMethod(@RequestBody String string)"{
> >  
> >        System.out.println("测试");
> >   
> >   }
> > }
> > ```
> >
> > > 注意：
> > >
> > > 1. 一个请求只能有一个RequestBody，也就是说，当一个方法中有两个参数的时候，最多只能有一个参数加@RequestBody注解用来
> > > 2. @RequestBody接收的参数是来自requestbody中，也就是请求体
> >
> > `@RequestParam`接收的参数是来自Request header中，即请求头中。通常用于GET请求
> >
> > ```java
> > @Controller
> > @RequesMapping（“/api”）
> > public class test{
> >  
> > public void testMethod(@RequestParam(value="name",required=false,defaultValue="雷神")String name,@RequestParam(value="age")Int age){
> >  
> >     System.out.println("年仅"+age+“岁肥宅”+name);
> >  
> > }
> >  
> > }
> > ```
> >
> > 

+ 简单参数
+ 实体参数
+ 数组集合参数
+ 日期参数
+ Json参数
+ 路径参数 

```java
package com.lifetime.springbootwebrespreq.controller;

import com.lifetime.springbootwebrespreq.pojo.Address;
import com.lifetime.springbootwebrespreq.pojo.Hobby;
import com.lifetime.springbootwebrespreq.pojo.User;
import org.springframework.format.annotation.DateTimeFormat;
import org.springframework.web.bind.annotation.*;

import java.lang.reflect.Array;
import java.time.LocalDateTime;
import java.util.Arrays;
import java.util.List;

@RestController
public class RequestController {

    @RequestMapping("/testRequest")
    public String testRequest(@RequestParam(name = "name",required = false) String username,Integer age){
        System.out.println(username + age);
        return "OK";
    }

    @RequestMapping("/test")
    public String test(){
        return "hello world" ;
    }

    @RequestMapping("/simplePojo")
    public String simplePojo(User user){
        System.out.println(user.toString());
        return "ok";
    }

    //信息中包含信息
    @RequestMapping("/simplePojo1")
    public String simplePojo1(User user, Address address){
        System.out.println("有地址的访问");
        return "ok";
    }

    //同一个类型，多个值(数组、集合)
    @RequestMapping("array")
    public String array(String[] hobby){
        System.out.println("接收的hobby有(数组)" + Arrays.toString(hobby));
        return "OK";
    }
    //使用集合
    @RequestMapping("ListParam")
    public String ListParam(@RequestParam List<String> hobby){
        System.out.println("接收的Hobby(集合)" + hobby);
        return "OK";
    }

    //日期参数
    @RequestMapping("/dateParam")
    public String dateParam(@DateTimeFormat(pattern = "yyyy-MM-dd HH:mm:ss")LocalDateTime updateTime){
        System.out.println("时间为" + updateTime);
        return "OK";
    }

    //json参数
    @RequestMapping("jsonParam")
    public String jsonParam(@RequestBody User user){
        System.out.println(user);
        return "OK";
    }

    //路径参数
    @RequestMapping("/path/{id}")
    public String pathParam(@PathVariable Integer id){
        System.out.println(id);
        return "OK";
    }
}

```

#### 响应

使用到`@ResponseBody`

+ 类型：方法注解、类注解
+ 位置：Controller方法/类上
+ 作用：将方法返回值直接响应，如返回值类型是实体对象/集合，将会转换为JSON响应对象
+ `@RestController = @Controlller + @ResponseBody`

```java
package com.lifetime.springbootwebrespreq.controller;

import com.lifetime.springbootwebrespreq.pojo.Address;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.ArrayList;
import java.util.List;

@RestController
public class ResponseController {

    @RequestMapping("/hello")
    public String hello(){
        System.out.println("Hello world!");
        return "OK";
    }
    @RequestMapping("getAddress")
    public Address getAddress(){
        Address address = new Address();
        address.setCity("邳州市");
        address.setProvince("江苏省");
        return address;
    }

    @RequestMapping("listAddress")
    public List<Address> listAddress(){
        List<Address> list = new ArrayList<>();

        Address address1 = new Address();
        address1.setProvince("台湾省");
        address1.setCity("台北市");

        Address address2 = new Address();
        address2.setCity("深圳市");
        address2.setProvince("广东省");

        list.add(address1);
        list.add(address2);
        return list;
    }
}

```



↑ 以上，如果数据过多，不容易处理

↓ 统一响应结果：

```java
public class Result{
    //响应码 1代表成功 2代表失败
 	private Integer code;
    //提示信息
    private String msg;
    //返回数据
    private Object data;
}
```

> 文件名：ResponseController.java

```java
package com.lifetime.springbootwebrespreq.controller;

import com.lifetime.springbootwebrespreq.pojo.Address;
import com.lifetime.springbootwebrespreq.pojo.Result;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.ArrayList;
import java.util.List;

@RestController
public class ResponseController {
    
    @RequestMapping("/hello")
    public Result hello(){
        return new Result(1,"success","hello world!");
    }
    @RequestMapping("getAddress")
    public Result getAddress(){
        Address address = new Address();
        address.setCity("邳州市");
        address.setProvince("江苏省");
        return Result.success(address);
    }

    @RequestMapping("listAddress")
    public Result listAddress(){
        List<Address> list = new ArrayList<>();

        Address address1 = new Address();
        address1.setProvince("台湾省");
        address1.setCity("台北市");

        Address address2 = new Address();
        address2.setCity("深圳市");
        address2.setProvince("广东省");

        list.add(address1);
        list.add(address2);
        return Result.success(list);
    }

}

```

> 文件名：Result.java

```java
package com.lifetime.springbootwebrespreq.pojo;

public class Result {
    private Integer code;
    private String msg;
    private Object data;

    public Result(){
    }
    public Result(Integer code,String msg,Object data){
        this.code = code;
        this.msg = msg;
        this.data = data;
    }
    public Integer getCode() {
        return code;
    }

    public void setCode(Integer code) {
        this.code = code;
    }

    public String getMsg() {
        return msg;
    }

    public void setMsg(String msg) {
        this.msg = msg;
    }

    public Object getData() {
        return data;
    }

    public void setData(Object data) {
        this.data = data;
    }
    public static Result success(Object data){
        return new Result(1,"sucess",data);
    }
    public static Result success(){
        return new Result(1,"success",null);
    }
    public static Result error(String msg){
        return new Result(0,msg,null);
    }

    @Override
    public String toString() {
        return "Result{" +
                "code=" + code +
                ", msg='" + msg + '\'' +
                ", data=" + data +
                '}';
    }
}

```



开始做项目：

----

---

+ 开发规范：基于当前最为流行的前后端分离模式进行开发

+ 前端与后端的交互：Restful

  + REST (REPresentational State Transfer)，表述性状态装换，是一种软件架构风格

  + > REST只是一种风格，可以打破

+ 开发流程：

  查看页面原型->阅读接口文档->思路分析->接口开发->接口测试->前后端联调



### 部门查询

![](https://cdn.jsdelivr.net/gh/czlifetime/img/%E6%9F%A5%E8%AF%A2%E9%83%A8%E9%97%A8%E6%80%9D%E8%B7%AF.png)
