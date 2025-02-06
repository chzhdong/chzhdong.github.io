---
title: SSM
published: 2024-12-19
description: 'SSM Framework'
image: ''
tags: ["SSM"]
category: 'Java'
draft: false 
lang: 'zh_CN'
---

## JDK

在 Java 后端开发中，JDK 是 Java Development Kit 的缩写，它提供了编译器、JVM 环境以支持 Java程序的运行。

若我们需要安装 JDK，使用搜索引擎 google 搜索，在[Java Downloads | Oracle](https://www.oracle.com/java/technologies/downloads/)下载所需的 JDK 版本。

设置环境变量：JAVA_HOME 环境变量设置为 JDK 安装目录；JAVA_HOME 的 bin 目录 添加到系统环境变量 PATH。

在安装完成后可以使用 java --version 测试 JDK 安装。

注：对于 Linux、Mac 可以使用，export JAVA_HOME=`/usr/libexec/java_home -v 23` 以及 export PATH=\$JAVA_HOME/bin:\$PATH。

## ClassPath

在 Java 中，classpath 是 JVM 需要使用到的环境变量，即指示 JVM 如何找到编译后的 class 文件。一般而言，不推荐在电脑 PC 的系统环境变量中添加 classpath，可能会导致混乱和污染；我们主要通过 `java -cp classpath class_file`的方式来使用命令行指定 classpath。

## SSM

在 Java 开发中，传统的使用SSM框架，即Spring、SpringMVC、Mybatis；其中，Spring主要用于管理Bean，SpringMVC则用于管理ModelAndView，即表示层，而Mybatis则是持久层，用于实现程序与数据库的交互。

### Spring

在目前的Spring框架中，主要涉及两个组件，即IOC (Inverse of Control) 和 AOP (Aspect-Oriented Programming)；IOC即为控制反转，将程序中Bean的创建和管理交给IOC而不是程序本身负责，这使得全局可以通用同一实例而不需要反复实例化，并且可以在使用时直接注入即可。AOP，即面向切片编程，其主要任务是分离核心业务逻辑和事务的联系，AOP 的实现方法就是通过对代理的 Java 类生成其对应的子类来实现对其的事务检查。注，AOP 代理的时候，是直接生成了对应代理类的子类的字节码，而并没有调用对应的超类的构造函数。所以对于代理类的变量无法直接通过子类对象进行访问，而需要通过对于的函数，函数一般会被子类进行覆写；注意，final 修饰的函数不会被覆写。

### SpringMVC

SpringMVC是Spring框架的内置框架，它对于Sevelet API进行封装，对于用户的请求，通过前端控制器对请求进行处理，分发到合适的handler (Controller) 处理，并返回相关的ModelAndView到前端进行渲染，并返回结果给用户。

### Mybatis

Mybatis是持久层的框架，对JDBC进行封装以实现简单易用的使用；通过定义相关的类使用sqlSession来和数据库进行交互，通过预定义的SQL代码来实现数据库数据的控制。这些SQL代码一般保存在XML文件中，在需要时直接访问即可。
