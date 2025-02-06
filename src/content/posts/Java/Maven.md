---
title: Maven
published: 2025-01-08
description: 'Maven Tutorial'
image: ''
tags: ["Maven"]
category: 'Java'
draft: false 
lang: 'zh_CN'
---

## Maven

Maven 是 Java 的项目管理工具，包括项目结构、依赖管理、构建流程等一整套机制。

从 [Maven](https://maven.apache.org/) 官网下载所需的 Maven 版本，需要设置环境变量 M2_HOME 为 Maven 的安装目录，并把 bin 目录添加到系统环境变量中。

对于 Maven 的安装测试，我们可以使用 mvn --version 来进行测试判断。

Maven 在管理依赖时，当导入了相关依赖后，会自动导入依赖的依赖，而无需用户进行手动添加；在 Maven 管理的依赖关系中，主要有四种，即 compile、test、runtime、provided。

在实际使用时，Maven 可以配置国内的镜像网站来加快下载依赖的速度，可以在 [Maven Central Repository Search](https://search.maven.org/) 中进行查询第三方组件。

Maven 的 lifecycle 是用一系列的 phase 构成，我们可以通过 maven 指令直接运行 Java 项目的整个流程，如编译、测试、安装、部署等。

Maven 对于整个流程的运行是基于插件实现的，如编译则是基于 compiler 插件，如果需要自定义相关的插件，则需要额外的配置。
