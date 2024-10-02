---
title: Junit
tag: 软件测试
cover: https://cdn.jsdelivr.net/gh/czlifetime/img/%E8%BD%AF%E4%BB%B6%E6%B5%8B%E8%AF%95.jpg
---

# Junit

- ## 简述

  JUnit 是一个 **Regression Testing Framework**被开发者用来在Java中实现单元测试，加快编程速度，提高代码质量。JUnit 框架可以轻松地与以下任一项集成 -

  - Eclipse
  - Ant
  - Maven

- **

  ## JUnit 测试框架的特点

  JUnit 测试框架提供以下重要功能 -

  - Fixtures
  - 测试套件
  - 测试运行器
  - JUnit 类

  ### Fixtures

  **Fixtures**是一组对象的固定状态，用作运行测试的基线。测试夹具的目的是确保有一个众所周知的固定环境来运行测试，以便结果是可重复的。它包括 -

  - setUp() 方法，在每次测试调用之前运行。
  - tearDown() 方法，在每个测试方法之后运行。

  让我们看一个例子 -

  ```java
  import junit.framework.*;
  public class JavaTest extends TestCase {
     protected int value1, value2;
     
     // assigning the values
     protected void setUp(){
        value1 = 3;
        value2 = 3;
     }
     // test method to add two values
     public void testAdd(){
        double result = value1 &plus value2;
        assertTrue(result == 6);
     }
  }
  ```

  复制

- 

  ## 测试套件

  一个测试套件捆绑了几个单元测试用例并将它们一起运行。在 JUnit 中，@RunWith 和 @Suite 注释都用于运行套件测试。下面给出了一个使用 TestJunit1 和 TestJunit2 测试类的示例。

  ```java
  import org.junit.runner.RunWith;
  import org.junit.runners.Suite;
  //JUnit Suite Test
  @RunWith(Suite.class)
  @Suite.SuiteClasses({ 
     TestJunit1.class ,TestJunit2.class
  })
  public class JunitTestSuite {
  }
  ```

  复制

  ```java
  import org.junit.Test;
  import org.junit.Ignore;
  import static org.junit.Assert.assertEquals;
  public class TestJunit1 {
     String message = "Robert"; 
     MessageUtil messageUtil = new MessageUtil(message);
     
     @Test
     public void testPrintMessage() {     
        System.out.println("Inside testPrintMessage()");    
        assertEquals(message, messageUtil.printMessage());     
     }
  }
  ```

  复制

  ```java
  import org.junit.Test;
  import org.junit.Ignore;
  import static org.junit.Assert.assertEquals;
  public class TestJunit2 {
     String message = "Robert"; 
     MessageUtil messageUtil = new MessageUtil(message);
   
     @Test
     public void testSalutationMessage() {
        System.out.println("Inside testSalutationMessage()");
        message = "Hi!" + "Robert";
        assertEquals(message,messageUtil.salutationMessage());
     }
  }
  ```

  复制

- 

  ## 测试运行器

  测试运行器用于执行测试用例。这是一个假设测试类的示例**TestJunit** 已经存在。

  ```java
  import org.junit.runner.JUnitCore;
  import org.junit.runner.Result;
  import org.junit.runner.notification.Failure;
  public class TestRunner {
     public static void main(String[] args) {
        Result result = JUnitCore.runClasses(TestJunit.class);
            
        for (Failure failure : result.getFailures()) {
           System.out.println(failure.toString());
        }
            
        System.out.println(result.wasSuccessful());
     }
  }
  ```

  复制

- **

  ## JUnit 类

  JUnit 类是重要的类，用于编写和测试 JUnit。一些重要的课程是 -

  - **Assert** - 包含一组断言方法。
  - **TestCase** − 包含一个测试用例，该用例定义了运行多个测试的夹具。
  - **TestResult** − 包含收集执行测试用例结果的方法。