---
title: Array
published: 2024-12-20
description: 'Conclusion for Array'
image: ''
tags: ["Array"]
category: 'Algorithm'
draft: false
lang: 'zh_CN'
---

## 二分法

本类题主要考察对数组基本操作，主要需要考虑的是对二分法区间两端的开闭关系；

二分法的时间复杂度为：O(logN)；

主要就是坚持循环不变量，把握循环中区间的定义，考虑循环的细节。

## 双指针法

通过双指针法，即快慢指针来实现一个循环来实现两个循环的工作；

双指针法的时间复杂度：O(N)；

使用双指针法是由于数组的元素无法单一释放，只能进行全部释放。

## 滑动窗口

滑动窗口的时间复杂度为：O(N)；

滑动窗口主要是通过移动窗口的起始位置，再通过动态的调整窗口的大小，以找出满足要求的序列；

## 模拟行为

本类题目主要不考虑特别的算法，主要考虑对数组中循环不变量的管理。

## 前缀和

本题主要是计算前N个数组元素的和，来快速计算诸如某个区间序列的和等问题。