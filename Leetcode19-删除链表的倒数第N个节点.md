---
title: Leetcode19.删除链表的倒数第N个节点
date: 2020-10-18 09:14:02
categories: Leetcode
tags:
  - 链表
  - 双指针
---

## Leetcode19.删除链表的倒数第N个节点

给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。

[题目链接](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list)

<!--more-->

示例：

```
给定一个链表: 1->2->3->4->5, 和 n = 2.

当删除了倒数第二个节点后，链表变为 1->2->3->5.
```



说明：

给定的 n 保证是有效的。

进阶：

你能尝试使用一趟扫描实现吗？



### 思路

使用快慢指针`slow`和`fast`来一次遍历，创建虚拟头节点`dummyHead`。

初始时快慢指针都指向`dummyHead`，首先将快指针移动`n`次，再将快慢指针同步向后移动，直到快指针到达最后一个节点，此时`slow`指针就指向要删除结点的前一个节点。



### 代码实现

```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummyHead = new ListNode(-1);
        dummyHead.next = head;
        ListNode fast = dummyHead;
        ListNode slow = dummyHead;
        for(int i = 0;i<n;i++){
            fast = fast.next;
        }
        while(fast.next!=null){
            fast = fast.next;
            slow = slow.next;
        }
        ListNode next = slow.next;
        slow.next = next.next;
        next.next = null;
        return dummyHead.next;
    }
}
```



