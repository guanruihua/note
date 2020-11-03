---
title: Spring
date: 2020-09-08 21:33:25
tags: 
	- spring
	- java
---


# Spring

SpringDemo1    3-8

## 前言

> -  Spring是一个开源框架
> - Spring 为简化企业级应用开发而生. 使用Spring可以使简单的JavaBean实现以前只有EJB才能实现的功能
> - Spring 是JavaSE/EE的一站式框架

## 优点

- 方便解耦, 简化开发

  - Spring就是一个大工厂,可以将所有对象创建和依赖关系维护, 交给Spring管理

- AOP变成的支持

  - Spring提供蜜蜡线切面编程, 可以方便的实现对程序进行权限拦截、运行监控等功能

- 声明式事务的支持

  - 只需要通过配置就可以完成对事务的管理, 而无需手动编程

- 方便程序的测试

  - Spring对Junit4支持, 可以通过注解方便的测试Spring程序

- 方便继承各种优秀框架

  - Spring不排斥各种优秀的开源框架,其内部提供对各种优秀的框架(Struts、Hibernate、MyBatis等）的直接支持

- 降低JavaEE API的使用难度

  - Spring对JavaEE开发中非常难用的一些API（JDBC、JavaMail、远程调用等），都提供了封装，使这些API应用难度大大降低

  

  ## 模块

  <img src="https://images.gitee.com/uploads/images/2020/0711/133424_2ed6aec0_6545143.png" style="zoom:50%;" />

  

## Spring IOC的底层原理

## 导入Spring核心开发包到创建工程

> commons-logging-xxx.jar
>
> spring-beans-x.x.x.RELEASE.jar
>
> spring-context-x.x.x.RELEASE.jar
>
> spring-core-x.x.x.RELEASE.jar
>
> spring-expression-x.x.x.RELEASE.jar

```xml
<dependency>
  <groupId>log4j</groupId>
  <artifactId>log4j</artifactId>
  <version>1.2.17</version>
</dependency>

<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-core</artifactId>
  <version>4.2.4.RELEASE</version>
</dependency>
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-context</artifactId>
  <version>4.2.4.RELEASE</version>
</dependency>
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-beans</artifactId>
  <version>4.2.4.RELEASE</version>
</dependency>
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-expression</artifactId>
  <version>4.2.4.RELEASE</version>
</dependency>
```

## 概念

>  Spring IOC
>
> - IOC Inverse of Control 反转控制的概念, 就是将原本在程序中手动创建UserService对象的控制权, 交由Spring框架管理
> - 就是将创建UserService对象控制权反转到Spring框架
> - DI Dependency Injection **依赖注入**的概念, 就是在创建这个对象的过程中, 将这个对象所依赖的属性注入进去

```java
/**
     * Spring的方式实现
     */
    @Test
    public void demo2(){
        //创建Spring的公厂
        ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
        //通过工厂获得类
        UserService userService = (UserService) applicationContext.getBean("userService");
        userService.sayHello();
    }

    @Test
    /**
     * 读取磁盘系统中的配置文件
     */
    public void demo3(){
        //创建Spring的工厂类
        //读取c盘的配置文件
        ApplicationContext applicationContext = new FileSystemXmlApplicationContext("c:\\applicationContext.xml");
        UserService userService = (UserService) applicationContext.getBean("userService");
        userService.sayHello();
    }

    @Test
    /**
     * 传统方式的工厂类: BeanFactory
     */
    public void demo4(){
        BeanFactory beanFactory = new XmlBeanFactory(new ClassPathResource("applicationContext.xml"));
        UserService userService = (UserService) beanFactory.getBean("userService");
        userService.sayHello();
    }

    @Test
    /**
     * 传统方式的工厂类: BeanFactory
     */
    public void demo5(){
        BeanFactory beanFactory = new XmlBeanFactory(new FileSystemResource("C:\\applicationContext.xml"));
        UserService userService = (UserService) beanFactory.getBean("userService");
        userService.sayHello();
    }
```

## Bean

### 三种实例化Bean的方式

#### 类构造器实例化(默认无参数)

applicationContext.xml

```xml
<!--第一种: 无参构造器的方式-->
    <bean id="bean1" class="com.ioc.demo2.Bean1"></bean>
```

javaclass
```java
 
public void demo1(){
        //创建工厂
        ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
        //通过工厂类获得类的实例
        Bean1 bean1 = (Bean1) applicationContext.getBean("bean1");

    }
```

#### 静态工厂方法实例化(简单工厂模式)

applicationContext.xml

```xml
<!--第二种: 静态工厂的方式-->
    <bean id="bean2" class="com.ioc.demo2.Bean2Factory" factory-method="createBean2"></bean>
```

javaclass
```java
 
public void demo1(){
        //创建工厂
        ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
        //通过工厂类获得类的实例
        Bean1 bean1 = (Bean1) applicationContext.getBean("bean1");

    }
```



#### 使用实例工厂方法实例化(工厂方法模式)

```xml
<!--第三种: 实例工厂的方式-->
    <bean id="bean3Factory" class="com.ioc.demo2.Bean3Factory"></bean>
    <bean id="bean3" factory-bean="bean3Factory" factory-method="createBean3"/>
```

javaclass
```java
 
public void demo1(){
        //创建工厂
        ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
        //通过工厂类获得类的实例
        Bean1 bean1 = (Bean1) applicationContext.getBean("bean1");

    }
```

### id和name的作用区别

> name可以使用特殊字符

### Bean的作用域

<img src="https://images.gitee.com/uploads/images/2020/0802/144827_2c930c4b_6545143.png" style="zoom:50%;" />

### Bean的生命周期

第一步:MAN被实例化了..., instantiate bean对象实例化
第一步:设置属性..., populate properties 封装属性
第三步,设置Bean的名称man, 如果Bean实现了BeanNameAware 执行 setBeanName
第四步,了解工厂的信息,如果Bean实现BeanFactoryAware 或者 ApplicationContextAware 设置工厂
第五步,初始化前方法, 如果存在BeanPostProcessor(后处理Bean), 执行postProcessBeforeInitialization
第六步,属性设置后, 如果Bean实现了InitializingBean 执行afterPropertiesSet

第七步:MAN被初始化了.... , 调用`<bean init-mothod="init">`
第八步,初始化后的方法, 如果存在类实现 BeanPostProcessor ( 处理Bean ) , 执行postProcessAfterInitialization
第九步: 执行业务方法, 执行业务处理
第十步: 执行Spring的销毁方法, 如果Bean实现DisposableBean 执行 destory

第十一步: MAN被销毁了....  , 掉用`<bean destroy-method="customerDestroy">`执行销毁方法customerDestroy

> 最重要的是第五步和第八步: 可以增强类的方法

> Spring
>
> ```xml
> <bean id="man" class="com.ioc.demo3.Man" init-method="setup" destroy-method="manDestory">
> ```
>
> - 初始化bean会触发init-method="functionName"
> - bean销毁时触发destory-method = "destoryFunctionName"

