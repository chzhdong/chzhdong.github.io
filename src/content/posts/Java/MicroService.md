---
title: MicroService
published: 2025-02-06
description: 'MicroService Conclusion'
image: ''
tags: ["MicroService"]
category: 'Java'
draft: false 
lang: 'zh_CN'
---

## 分布式事务

### CAP & BASE

在分布式事务中，主要存在主要的三个指标：

- **C**onsistency（一致性）：用户访问分布式系统中的任意节点，得到的数据必须一致。
- **A**vailability（可用性）：用户访问分布式系统时，读或写操作总能成功。
- **P**artition tolerance （分区容错性）：当分布式系统节点之间出现网络故障导致节点之间无法通信的情况。

通过总结系统设计经验，提出了以下的设计思想：

- **B**asically **A**vailable **（**基本可用**）**：分布式系统在出现故障时，允许损失部分可用性，即保证核心可用。
- **S**oft State**（**软状态**）：**在一定时间内，允许出现中间状态，比如临时的不一致状态。
- **Ev**entually Consistent**（**最终一致性**）**：虽然无法保证强一致性，但是在软状态结束后，最终达到数据一致。

### TCC

TCC模式与AT模式非常相似，每阶段都是独立事务，不同的是TCC通过人工编码来实现数据恢复。需要实现三个方法：

-  `try`：资源的检测和预留； 
-  `confirm`：完成资源操作业务；要求 `try` 成功 `confirm` 一定要能成功。 
-  `cancel`：预留资源释放，可以理解为try的反向操作。

## 服务保护

为了实现微服务的保护，主要的方式有以下四类：

- 线程隔离：主要的实现方法是线程池隔离和信号量隔离；
- 滑动窗口算法：即在一段窗口时间内，只允许有限数量的外部访问；
- 令牌桶算法：获取令牌，通过检查，但也会出现访问的波动情况；
- 漏桶算法：针对波动较大的服务场景，使用漏桶算法来消峰平谷。

