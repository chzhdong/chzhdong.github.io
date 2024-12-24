---
title: 环形链表II
published: 2024-12-24
description: 'LeetCode 142 Medium'
image: ''
tags: ["LeetCode"]
category: 'Coding'
draft: false 
lang: 'zh_CN'
---

## 题目链接

[142. 环形链表II - 力扣（LeetCode）](https://leetcode.cn/problems/linked-list-cycle-ii/description/)

## 题目描述

给定一个链表的头节点  head ，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。

## 解题方法

本题需要使用快慢指针，即快指针一次移动两个结点，则快慢指针最终会相遇；通过数学计算，两者相遇的位置，将慢指针重新置为头指针，两者同时运动，相遇点为环入口。

### 解题代码
```java
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode fast = head;
        ListNode slow = head;
        while(fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
            if(fast == slow) {
                slow = head;
                while(fast != slow) {
                    fast = fast.next;
                    slow = slow.next;
                }
                return slow;
            }
        }
        return null;
    }
}
```
