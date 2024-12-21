---
title: 螺旋区间II
published: 2024-12-19
description: 'LeetCode 209 Medium'
image: ''
tags: ["LeetCode"]
category: 'Coding'
draft: false 
lang: 'zh_CN'
---

## 题目链接

[59. 螺旋矩阵 II - 力扣（LeetCode）](https://leetcode.cn/problems/spiral-matrix-ii/description/)

## 题目描述

给你一个正整数 `n` ，生成一个包含 `1` 到 `n2` 所有元素，且元素按顺时针顺序螺旋排列的 `n x n` 正方形矩阵 `matrix` 。

## 解题方法

本题并不考察算法设计，考察的内容主要是编程的严谨性；其实也就类似于二分查找中对数组区间的管理。本题中主要就是管理遍历二维数组的方向，保证整体的遍历没有重复，以及方向的正确性。

### 解题代码

```java
class Solution {
    public int[][] generateMatrix(int n) {
        int row = 0;
        int col = 0;
        int num = 1;
        int direct = 1;
        int[][] matrix = new int[n][n];
        while (num <= n*n) {
            if (direct == 1) {
                matrix[row][col] = num;
                num++;
                if ((col < n - 1) && (matrix[row][col + 1] == 0)) {
                    col = col + 1;
                } else {
                    row = row + 1;
                    direct = 2;
                }
            }
            else if (direct == 2) {
                matrix[row][col] = num;
                num++;
                if ((row < n - 1) && (matrix[row + 1][col] == 0)) {
                    row = row + 1;
                } else {
                    col = col - 1;
                    direct = 3;
                }
            }
            else if (direct == 3) {
                matrix[row][col] = num;
                num++;
                if ((col > 0) && (matrix[row][col - 1] == 0)) {
                    col = col - 1;
                } else {
                    row = row - 1;
                    direct = 4;
                }
            }
            else {
                matrix[row][col] = num;
                num++;
                if ((row > 0) && (matrix[row - 1][col] == 0)) {
                    row = row - 1;
                } else {
                    col = col + 1;
                    direct = 1;
                }
            }
        }
        return matrix;
    }
}
```
