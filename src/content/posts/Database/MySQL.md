---
title: MySQL
published: 2025-02-06
description: 'MySQL Database'
image: ''
tags: ["MySQL"]
category: 'DataBase'
draft: false 
lang: 'zh_CN'
---

## 概述

数据库总共有三种模型，即层次模型、网状模型、关系模型。

SQL 是结构化查询语言的缩写，用来访问和操作数据库系统；

DDL(Data Definition Language) 允许用户定义数据，由数据库管理员执行；DML(Data Manipulation Language) 允许用户对数据库进行日常的处理；DQL(Data Query Language) 允许用户查询数据。

SQL 语言关键词不区分大小写，但不同数据库的实现可能对于实际数据的大小写不同；

## 安装

官网下载社区版 [MySQL :: Download MySQL Community Server](https://dev.mysql.com/downloads/mysql/) ；

MySQL 会创建一个 root 用户，并提示输入 root 口令；

通过 `mysql` 命令连接 MySQL 服务器，以验证 MySQL 的安装是否正确;

MySQL 的 bin 目录添加到系统的环境变量；

## 索引

本部分将主要介绍 MySQL 中有关索引的知识详解，包括其底层的数据结构，实现细节以及相关的设计思想。

在 MySQL 中，其索引是基于 B+ 树进行实现的，没有使用常规的二叉树、红黑树是由于如果数据库中存储大量的数据会导致树的高度较高，查找的时长增加；而没有使用 HashTable 则是应为哈希表的查询时间是常数量级的，但是其不支持对于范围查找。

对于 B+ 树和 B- 树，其主要的区别就是树中是否存在重复的索引元素，在 B+ 树中其数据全部都位于叶节点中，而B-树的所有数据则分布在每一级的树节点中。

对于 MySQL 而言，其数据库引擎是基于每个表进行设置的，如 MyISam 或者 InnoDB；对于 MyISam 而言，其是非聚集索引也就是其索引和数据库数据存放在两个文件，索引存储的是数据文件中具体的数据存储位置；而 InnoDB 则是聚集索引，也就是索引和数据存储在一个文件中，索引直接查找到的就是对应的数据。

在 MySQL 使用 InnoDB 一般以主键作为索引，进行数据的查找；而如果设置了其他的索引，则该索引所查找到的是对应的主键，再通过主键查找到对应的数据，这样保障了数据的一致性；如果数据表中没有设置对应的索引，则 InnoDB 会查找符合要求的字段设置索引，如果没有查找到，那么数据库会自己创建一份字段用于构建索引。

在 MySQL 中，其底层的叶子节点会默认按照索引进行排序，即从左到右依次递增，以方便进行范围的查找；对于使用联合索引，那么需要依次对索引字段进行查找；如果出现字段跳过的情况，则会无法进行索引的查找。

## 事务

事务即是一组数据库操作，要么全部成功要么全部失败，保障数据的一致性；事务要求具备四种特性，即 ACID：

- Atomicity (原子性)：一组数据库操作同时成功或者同时失败，由 undo log 进行保障；
- Consistency (一致性)：事务的最终目的；
- Isolation (隔离性)：相互并发执行的事务之间互不干扰；
- Durability (持久性)：事务一旦提交，就应该是数据库中永久保存，由redo log进行保障。

### 隔离性

对于事务而言，其存在四种隔离级别：

- read uncommit (读未提交)：脏读问题，即当前事务读取的数据可能会被回滚；
- read commited (读已提交)：不可重复读问题，当前事务中不同读取语句查询结果不一致；
- repeatable read (可重复读)：幻读问题，即当前事务读取的数据都是第一个语句执行的快照，并非真实数据；
- serializable (串行)：无

### MVCC

对于 MySQL 而言，他是通过一个 MVCC (Mutil-Version Concurrency Control) 来实现对应的隔离级别的；对于一条数据库中的数据，在 undo log 中会维护一条快照链，也就是针对每次数据的修改维护一条快照，其中包括对于的 trx_id、roll_pointer 来指向对应的事务和回滚的快照。

那么基于这样的快照链或者回滚日志，read commited 总是读取最新的已提交的数据，而 repeatable read 则是读取当前事务所绑定的快照数据，来实现可重复读；注意，当前事务绑定了对应的快照数据，但是更新等数据库操作还是操作最新的数据库数据。

### 持久性

为了实现持久性，MySQL 中加入了 BufferPool 和 redo log，也就是 MySQL 实现数据操作，那么会先进入到内存的 BufferPool 进行缓存而并非直接写入磁盘中；之后，BufferPool 会在 redo log 中记录这次数据操作，即可认为数据操作成功；即使宕机，数据依然可以按照 redo log 的记录完成数据的存储和操作；此外，使用 redo log 的原因的是因为对磁盘的随机性性能较低，而基于 redo log 对数据库操作进行一次性的顺序写，其性能较高，满足并发的要求。

## 锁

### 粒度

锁根据粒度可以划分为三类：

- 全局锁：对于数据库中所有表进行上锁；
- 表级锁：
  - 表锁：即对整个表进行上锁；
  - 元数据锁：隐式加锁，防止 DDL 和 DML 之间的冲突；
  - 意向锁：主要是标记表已经加锁，减少查询锁的时间；
- 行级锁：
  - 行锁：对数据库某一条行数据加锁；
  - 间隙锁：锁的是记录间的间隙；
  - 临键锁：锁的是当前记录和记录间的空隙；

上述的间隙锁和临键锁是为了解决幻读问题。

### 性质

锁根据性质又可以分为：

- 共享读锁；
- 独占写锁；
- 悲观锁；
- 乐观锁。

## 分库分表

为了解决由于单数据库或者单表的高并发而影响服务性能，所以设计了分库分表的思想；但是由于分库分表的复杂性，一般对于表中数据超过五百万或者大小超过 2GB 才会考虑分库分表；分库分表一般是由于单个数据库承载的 SQL 连接数有限或者单个数据表中数据量过大导致查询时间过长的问题。

对于分库分表 (Database Sharding)，一般可以分为两类，即纵向划分和横向划分；纵向划分一般是指对于业务层面的划分，例如数据库划分为用户数据库、订单数据库等；而横向划分则一般是由于数据过多，将数据划分以减小查询压力；横向一般又可以划分为取模划分以及范围划分，取模的优点是划分较为平均但是可以会扩宽面临数据迁移问题，而范围的划分则可能面临数据访问不平衡的问题。

为了实现分库分表，常见的方法主要有：ShardingJDBC 和 ShardingProxy 两种途径，一般 JDBC 的方法更为灵活。

对于 ShardingJDBC 方法，目前常用的四种方法：Inline、Standard、Complex、Hint；对于 Inline 方法，其实现的是对于单个分片键的精准查询；对于 Standard 方法，其实现的是对于单个分片键的精准查询和范围查询；对于 Complex 方法，其实现的是对于多个分片键的精准查询和范围查询；对于 Hint 方法，用户直接指定对于的 SQL 查询方法及路径。

对于以上的查询方法，其和业务逻辑是紧密耦合的，因此在设计系统时需要考虑仔细如何进行处理相关分库分表的问题。
