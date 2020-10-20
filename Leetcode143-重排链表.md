---
title: Leetcode143.重排链表
date: 2020-10-20 14:36:00
categories: Leetcode
tags:
  - 链表
---

## Leetcode143.重排链表

给定一个单链表 L：L0→L1→…→Ln-1→Ln ，
将其重新排列后变为： L0→Ln→L1→Ln-1→L2→Ln-2→…

你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

[题目链接](https://leetcode-cn.com/problems/reorder-list)

<!--more-->

示例 1:

```
给定链表 1->2->3->4, 重新排列为 1->4->2->3.
```



示例 2:

```
给定链表 1->2->3->4->5, 重新排列为 1->5->2->4->3.
```



### 思路

目标链表是原链表左半端和反转后的右半端合并的结果，所以：

1. 先找到中间节点
2. 反转右半部分节点
3. 将两链表合并



### 代码实现

```java
class Solution {
    public void reorderList(ListNode head) {
        if(head==null){
            return;
        }
        ListNode mid = getMiddleListNode(head);
        ListNode l1 = head;
        ListNode l2 = mid.next;
        mid.next = null;
        l2 = reverseListNode(l2);
        mergeListNode(l1,l2);
    }

    private ListNode getMiddleListNode(ListNode head){
        ListNode slow = head;
        ListNode fast = head;
        while(fast.next!=null&&fast.next.next!=null){
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }

    private ListNode reverseListNode(ListNode head){
        ListNode pre = null;
        ListNode cur = head;
        while(cur!=null){
            ListNode temp = cur.next;
            cur.next = pre;
            pre = cur;
            cur = temp;
        }
        return pre;
    }

    private void mergeListNode(ListNode l1,ListNode l2){
        ListNode l1Next;
        ListNode l2Next;
        while(l1!=null&&l2!=null){
            l1Next = l1.next;
            l2Next = l2.next;

            l1.next = l2;
            l1 = l1Next;

            l2.next = l1;
            l2 = l2Next;
        }
    }
}
```

