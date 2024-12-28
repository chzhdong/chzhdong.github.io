---
title: 四数相加II
published: 2024-12-26
description: 'LeetCode 454 Medium'
image: ''
tags: ["LeetCode"]
category: 'Coding'
draft: false 
lang: 'zh_CN'
---

## 题目链接

[454. 四数相加II - 力扣（LeetCode）](https://leetcode.cn/problems/4sum-ii/description/)

## 题目描述

给你四个整数数组 nums1、nums2、nums3 和 nums4 ，数组长度都是 n ，请你计算有多少个元组 (i, j, k, l) 能满足：
- 0 <= i, j, k, l < n
- nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0

## 解题方法

对于本题而言，最关键的是超时问题，因此需要记录已经访问过的元素。此外，由于两数之和相同存在多种可能，因此使用哈希表保存每两个数组可能和及其对应的数量。之后，在分别访问这两个哈希表，如果存在两数之和恰好为零，则在元组数量上加上其数量乘积。

### 解题代码
```java
class Solution {
    public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {
        HashMap<Integer, Integer> mapa = new HashMap<>();
        HashMap<Integer, Integer> mapb = new HashMap<>();

        for(int i = 0;i < nums1.length;i++) {
            for(int j = 0;j < nums2.length;j++) {
                if(mapa.containsKey(nums1[i] + nums2[j])) {
                    mapa.compute(nums1[i] + nums2[j], (key, value) -> value + 1);
                } else {
                    mapa.put(nums1[i] + nums2[j], 1);
                }

                if(mapb.containsKey(nums3[i] + nums4[j])) {
                    mapb.compute(nums3[i] + nums4[j], (key, value) -> value + 1);
                } else {
                    mapb.put(nums3[i] + nums4[j], 1);
                }
            }
        }

        int total = 0;
        for(Map.Entry<Integer, Integer> entrya : mapa.entrySet()) {
            for(Map.Entry<Integer, Integer> entryb : mapb.entrySet()) { 
                if(entrya.getKey() + entryb.getKey() == 0) {
                    total += entrya.getValue() * entryb.getValue();
                }
            }
        }
        return total;
    }
}
```
