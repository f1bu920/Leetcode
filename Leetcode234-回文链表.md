---
title: Leetcode234.回文链表
date: 2020-10-23 10:08:42
categories: Leetcode
tags:
  - 链表
---

## Leetcode234.回文链表

请判断一个链表是否为回文链表。

[题目链接](https://leetcode-cn.com/problems/palindrome-linked-list)

<!--more-->

示例 1:

```
输入: 1->2
输出: false
```



示例 2:

```
输入: 1->2->2->1
输出: true
```



进阶：

- 你能否用 O(n) 时间复杂度和 O(1) 空间复杂度解决此题？



### 思路

因为要`O(1)`时间复杂度，所以考虑递归。思想就是创建外指针`frontNode`，递归指向最后一个节点，在进行判断。

第二种思路就是先找到中点，再将后半部分反转，接着判断是否回文。



### 代码实现

```java
class Solution {
    ListNode frontNode;
    public boolean isPalindrome(ListNode head) {
        if(head==null){
            return true;
        }
        frontNode = head;
        return check(head);
    }
    private boolean check(ListNode head){
        if(head==null){
            return true;
        }
        //一直找到最后一个节点
        if(!check(head.next)){
            return false;
        }
        //接着判断是否回文，如果不回文会一直返回false
        if(head.val!=frontNode.val){
            return false;
        }
        frontNode = frontNode.next;
        return true;
    }
}
```



