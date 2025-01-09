---
title: HashTable
published: 2024-12-28
description: 'Conclusion of HashTable'
image: ''
tags: ["HashTable"]
category: 'Algorithm'
draft: false
lang: 'zh_CN'
---

## 数组

数组是哈希表的一种，数组的大小一般有限制，但是访问和管理都较为简单。

## 集合

集合主要需要针对考虑以前访问过的元素，并保存这些元素，同时对这些元素进行快速的查找。

## 图

图的主要使用方法是需要查找以前访问过的元素，并记录访问过的元素的相关信息。

## 注意事项

有些方法虽然需要使用已访问的元素，但是可能需要排除重复的元素等相关要求，可能直接使用哈希表并不合适；

例如 Leetcode 15 三数之和 以及 Leetcode 18 四数之和都推荐使用双指针法。
