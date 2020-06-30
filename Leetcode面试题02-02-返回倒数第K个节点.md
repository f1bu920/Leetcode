---
title: Leetcode面试题02.02.返回倒数第K个节点
date: 2020-06-30 08:58:02
categories: Leetcode
tags:
  - 链表
  - 双指针
---

## Leetcode面试题02.02.返回倒数第K个节点

实现一种算法，找出单向链表中倒数第 `k` 个节点。返回该节点的值。

注意：本题相对原题稍作改动

[题目链接](https://leetcode-cn.com/problems/kth-node-from-end-of-list-lcci)

<!--more-->

示例：

输入： 1->2->3->4->5 和 k = 2
输出： 4
说明：

给定的 k 保证是有效的。



### 思路

利用快慢指针，当快指针到达尾节点时，慢指针就是倒数第K个节点。



### 代码实现

```java
class Solution {
    public int kthToLast(ListNode head, int k) {
        ListNode cur = head;
        ListNode pre = head;
        while(k>=2){
            cur = cur.next;
            k--;
        }
        //cur.next!=null代表这是尾指针
        while(cur!=null&&cur.next!=null){
            cur = cur.next;
            pre = pre.next;
        }
        return pre.val;
    }
}
```

