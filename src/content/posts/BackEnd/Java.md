---
title: Java
published: 2024-12-19
description: 'The basics for Java Language'
image: ''
tags: ["Java"]
category: 'Language'
draft: false 
lang: 'zh_CN'
---

## JDK

在 Java 后端开发中，JDK 是 Java Development Kit 的缩写，它提供了编译器、JVM 环境以支持 Java程序的运行。若我们需要安装 JDK，使用搜索引擎 google 搜索，在[Java Downloads | Oracle](https://www.oracle.com/java/technologies/downloads/)下载所需的 JDK 版本。之后，设置环境变量：JAVA_HOME 环境变量设置为 JDK 安装目录；JAVA_HOME 的 bin 目录 添加到系统环境变量 PATH。在安装完成后可以使用 java --version 测试 JDK 安装。

注：对于 Linux、Mac 可以使用，export JAVA_HOME=`/usr/libexec/java_home -v 23` 以及 export PATH=\$JAVA_HOME/bin:\$PATH。

## Maven

Maven 是 Java 的项目管理工具，包括项目结构、依赖管理、构建流程等一整套机制。首先，从 [Maven](https://maven.apache.org/) 官网下载所需的 Maven 版本。同样的，我们需要设置环境变量 M2_HOME 为 Maven 的安装目录，并把 bin 目录添加到系统环境变量中。对于 Maven 的安装测试，我们可以使用 mvn --version 来进行测试判断。

Maven 在管理依赖时，当导入了相关依赖后，会自动导入依赖的依赖，而无需用户进行手动添加。在 Maven 管理的依赖关系中，主要有四种，即 compile、test、runtime、provided。

在实际使用时，Maven 可以配置国内的镜像网站来加快下载依赖的速度。此外，对于第三方组件，可以在 [Maven Central Repository Search](https://search.maven.org/) 中进行查询。

Maven 的 lifecycle 是用一系列的 phase 构成，我们可以通过 maven 指令直接运行 Java 项目的整个流程，如编译、测试、安装、部署等。

Maven 对于整个流程的运行是基于插件实现的，如编译则是基于 compiler 插件，如果需要自定义相关的插件，则需要额外的配置。

## classpath

在 Java 中，classpath 是 JVM 需要使用到的环境变量，即指示 JVM 如何找到编译后的 class 文件。一般而言，不推荐在电脑 PC 的系统环境变量中添加 classpath，可能会导致混乱和污染；我们主要通过 `java -cp classpath class_file`的方式来使用命令行指定 classpath。
