---
title: MySQL
published: 2024-12-19
description: 'The basics for MySQL Database'
image: ''
tags: ["MySQL"]
category: 'DataBase'
draft: false 
lang: 'zh_CN'
---

## 数据库概述

数据库总共有三种模型，即层次模型、网状模型、关系模型。

SQL 是结构化查询语言的缩写，用来访问和操作数据库系统；SQL 定义了三种操作数据库的能力：DDL(Data Definition Language) 允许用户定义数据，由数据库管理员执行；DML(Data Manipulation Language) 允许用户对数据库进行日常的处理；DQL(Data Query Language) 允许用户查询数据。

SQL 语言关键词不区分大小写，但不同数据库的实现可能对于实际数据的大小写不同；

## MySQL 安装

安装 MySQL 首先在官网下载社区版 [MySQL :: Download MySQL Community Server](https://dev.mysql.com/downloads/mysql/) ；在安装过程中，MySQL 会创建一个 root 用户，并提示输入 root 口令；在 Linux 安装 MySQL，可以使用发行版的包管理器，即 `apt install mysql-server`  以安装 MySQL 的最新版本。

在安装完成后，MySQL 会自动在后台允许；通过 `mysql` 命令连接 MySQL 服务器，以验证 MySQL 的安装是否正确；注，还需要将 MySQL 的 bin 目录添加到系统的环境变量。
