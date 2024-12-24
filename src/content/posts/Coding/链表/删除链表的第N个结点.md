---
title: 删除链表的第N个结点
published: 2024-12-24
description: 'LeetCode 19 Medium'
image: ''
tags: ["LeetCode"]
category: 'Coding'
draft: false 
lang: 'zh_CN'
---

## 题目链接

[19. 删除链表的第N个结点 - 力扣（LeetCode）](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/description/)

## 题目描述

给你一个链表，删除链表的倒数第 n 个结点，并且返回链表的头结点。

## 解题方法

本题类似数组中的双指针方法，当快速节点遍历到第N个结点，在同时将快速节点和慢速节点向后遍历，慢速结点即为所需。

### 解题代码
```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode _dummy = new ListNode(-1);
        _dummy.next = head;
        ListNode front = _dummy;
        ListNode back = head;
        int frequency = 1;
        while(back.next != null) {
            if(frequency == n) {
                back = back.next;
                front = front.next;
            } else {
                back = back.next;
                frequency += 1;
            }
        }
        front.next = front.next.next;
        head = _dummy.next;
        return head;
    }
}
```
