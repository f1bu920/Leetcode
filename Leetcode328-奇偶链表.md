---
title: Leetcode328.奇偶链表
date: 2020-11-13 10:16:12
category: Leetcode
tags:
  - 链表
---

## Leetcode328.奇偶链表

给定一个单链表，把所有的奇数节点和偶数节点分别排在一起。请注意，这里的奇数节点和偶数节点指的是节点编号的奇偶性，而不是节点的值的奇偶性。

请尝试使用原地算法完成。你的算法的空间复杂度应为 O(1)，时间复杂度应为 O(nodes)，nodes 为节点总数。

[题目链接](https://leetcode-cn.com/problems/odd-even-linked-list)

<!--more-->

示例 1:

```
输入: 1->2->3->4->5->NULL
输出: 1->3->5->2->4->NULL
```



示例 2:

```
输入: 2->1->3->5->6->4->7->NULL 
输出: 2->3->6->7->1->5->4->NULL
```



说明:

- 应当保持奇数节点和偶数节点的相对顺序。
- 链表的第一个节点视为奇数节点，第二个节点视为偶数节点，以此类推。



### 思路

分离链表，根据节点下标的奇偶性将链表分为奇链表和偶链表，然后将偶链表链接在奇链表之后。

使用`evenHead`记录偶链表的表头，`even`和`odd`分别代表遍历到的偶节点和奇节点。



### 代码实现

```java
class Solution {
    public ListNode oddEvenList(ListNode head) {
        if(head == null){
            return head;
        }
        //奇数
        ListNode odd = head;
        //偶数
        ListNode even = head.next;
        //偶链表表头
        ListNode evenHead = even;
        while(even != null && even.next != null){
            odd.next = even.next;
            odd = odd.next;

            even.next = odd.next;
            even = even.next;
        }
        //将偶链表接在奇链表后面
        odd.next = evenHead;
        return head;
    }
}
```



