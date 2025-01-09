---
title: Java
published: 2024-12-19
description: 'Java Language'
image: ''
tags: ["Language"]
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

## classpath

在 Java 中，classpath 是 JVM 需要使用到的环境变量，即指示 JVM 如何找到编译后的 class 文件。一般而言，不推荐在电脑 PC 的系统环境变量中添加 classpath，可能会导致混乱和污染；我们主要通过 `java -cp classpath class_file`的方式来使用命令行指定 classpath。
