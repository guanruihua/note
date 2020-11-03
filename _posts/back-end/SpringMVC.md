---
title: SpringMVC 
date: 2020-10-13 21:31:23 
---

# SpringMVC

> - [Spring官网](https://spring.io/)
> - [SpringMVC](https://docs.spring.io/spring-framework/docs/current/spring-framework-reference/web.html)
> - Spring体系的轻量级web mvc框架
>
> - 核心Controller控制器, 用于处理请求, 产生响应
> - 基于SpringIOC容器运行, 所有对象被IOC管理

版本变化

> Spring 5.x最低要求JDK8余J2EE 7(Servlet 3.1 / Tomcat 8.5+)
>
> 支持响应式编程



## 入门

### 环境搭建

#### Maven依赖spring-webmvc

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.example</groupId>
    <artifactId>SpringMVC_DEMO1</artifactId>
    <version>1.0-SNAPSHOT</version>
<!--    添加阿里云的镜像路径, 方便下载依赖-->
    <repositories>
        <repository>
            <id>aliyun</id>
            <name>aliyun</name>
            <url>https://maven.aliyun.com/repository/public</url>
        </repository>
    </repositories>

    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.1.9.RELEASE</version>
        </dependency>
    </dependencies>
</project>
```



#### web.xml配置DispatcherServlet

#### 配置applicationContext的mvc标记

#### 开发Controller控制器

## 数据绑定

## Restful开发风格

## 拦截器