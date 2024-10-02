---
title: JMeter
date: 2023-09-29
tag: 软件测试
cover: https://cdn.jsdelivr.net/gh/czlifetime/img/logo.png
---

# JMeter

## 入门

### JMeter简介

1. 可以对于服务器。网络或对象模拟巨大的负载
2. 可以创建带有断言的脚本来验证程序是否能返回期望的结果

### 优缺点

优点：

1. 开源、免费
2. 跨平台
3. 支持多协议
4. 小巧
5. 功能强大

缺点：

1. 不支持IP欺骗
2. 使用JMeter无法验证JS程序，也无法验证页面UI，所以要和Selenium配合来完成Web2.0应用的测试

### JMeter基本使用

#### 两个特殊的线程组

+ setUp线程组：最优先执行的线程组
+ tearDown线程组：最后执行的线程组

#### 操作线程组

![](https://cdn.jsdelivr.net/gh/czlifetime/img/JMeter%E7%9A%84%E7%BA%BF%E7%A8%8B%E5%B1%9E%E6%80%A7.bmp)

#### http请求默认值

![](https://cdn.jsdelivr.net/gh/czlifetime/img/JMeter%20http%E8%AF%B7%E6%B1%82%E9%BB%98%E8%AE%A4%E5%80%BC.bmp)

![](https://cdn.jsdelivr.net/gh/czlifetime/img/JMeter%20http%E8%AF%B7%E6%B1%82%E9%BB%98%E8%AE%A4%E5%80%BC2.bmp)

#### 信息头管理器

新增修改实现时提交的数据时JSON格式的，需申明提交的数据的内容类型：

![](https://cdn.jsdelivr.net/gh/czlifetime/img/JMeter%20http%E4%BF%A1%E6%81%AF%E5%A4%B4%E7%AE%A1%E7%90%86%E5%99%A8.bmp)

![](https://cdn.jsdelivr.net/gh/czlifetime/img/JMeter%20http%E4%BF%A1%E6%81%AF%E5%A4%B4%E7%AE%A1%E7%90%86%E5%99%A82.bmp)

### 参数化

当提交的数据量较大，参数化可以动态的获取、设置或生成数据，是一种有程序驱动代替人工驱动的数据设计方案，提高脚本的编写效率以及编写质量

以下四种方式实现参数化：

1. 用户数据文件设置

   ![](https://cdn.jsdelivr.net/gh/czlifetime/img/JMeter%20%E7%94%A8%E6%88%B7%E5%AE%9A%E4%B9%89%E7%9A%84%E5%8F%98%E9%87%8F.bmp)

   ![](https://cdn.jsdelivr.net/gh/czlifetime/img/JMeter%20%E7%94%A8%E6%88%B7%E5%AE%9A%E4%B9%89%E7%9A%84%E5%8F%98%E9%87%8F2.bmp)

2. CSV数据文件设置

   CSV：逗号分隔符，是一种简洁且常见的数据存储格式

   实现步骤：

   1. 使用CSV文件存储测试数据
   2. 编写被复用的学院新增脚本模板(编码集使用UTF-8，无BOM格式)
   3. 关联脚本与数据(将文件数据倒入脚本)

3. 用户参数

4. 函数

### 直链数据库

### 断言

