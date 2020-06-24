---
title: Leetcode25.K个一组反转链表
date: 2020-05-16 09:11:16
categories: Leetcode
tags:
  - 链表
---

## Leetcode25.K个一组反转链表

给你一个链表，每 k 个节点一组进行翻转，请你返回翻转后的链表。

k 是一个正整数，它的值小于或等于链表的长度。

如果节点总数不是 k 的整数倍，那么请将最后剩余的节点保持原有顺序。

 [题目链接](https://leetcode-cn.com/problems/reverse-nodes-in-k-group)

<!--more-->

示例：

给你这个链表：1->2->3->4->5

当 k = 2 时，应当返回: 2->1->4->3->5

当 k = 3 时，应当返回: 3->2->1->4->5



说明：

你的算法只能使用常数的额外空间。
你不能只是单纯的改变节点内部的值，而是需要实际进行节点交换。



#### 思路

创建一个虚拟头节点`dummyHead`，两个指针`head`和`tail`分别代表子段链表的开头和结尾，移动`k`次`tail`，使`tail`指向子链表的结尾。令指针`pre`指向上个子链表的结尾，初始时`pre`指向虚拟头节点，`pre`的作用是翻转完后将子链表再接回`pre`。指针`nex`指向下一段子链表的开头。

[参考链接](https://leetcode-cn.com/problems/reverse-nodes-in-k-group/solution/k-ge-yi-zu-fan-zhuan-lian-biao-by-leetcode-solutio/)

#### 代码实现

```java
class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode dummyHead = new ListNode(-1);
        dummyHead.next = head;
        ListNode pre = dummyHead;
        ListNode tail = dummyHead;
        int t;
        while (tail.next != null) {
            t = k;
            //向后移动k位
            while (t > 0 && tail != null) {
                t--;
                tail = tail.next;
            }
            //链表结束
            if (tail == null) {
                break;
            }
            //子链表的开头
            head = pre.next;
            //下一段链表的开头
            ListNode nex = tail.next;
            //断开，否则后面反转链表会死循环
            tail.next = null;
            //接上子链表
            pre.next = reverseListNode(head);
            //准备进行下一次子链表反转
            head.next = nex;
            pre = head;
            tail = pre;
        }
        return dummyHead.next;
    }
    //反转边表
    private ListNode reverseListNode(ListNode head) {
        if (head == null) {
            return null;
        }
        ListNode cur = head;
        ListNode pre = null;
        while (cur != null) {
            ListNode next = cur.next;
            cur.next = pre;
            pre = cur;
            cur = next;
        }
        return pre;
    }
}
```



