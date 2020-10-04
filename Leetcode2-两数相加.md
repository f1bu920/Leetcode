---
title: Leetcode2.两数相加
date: 2020-10-04 10:42:21
categories: Leetcode
tags:
  - 链表
---

## Leetcode2.两数相加

给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

[题目链接](https://leetcode-cn.com/problems/add-two-numbers)

<!--more-->

示例：

```
输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807
```



### 思路

使用`l1`、`l2`每次计算他们相加的和，使用`count`记录进位信息，当遍历完成较短链表后，如果另一条链表还有元素就加到后面。



### 代码实现

```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        if(l1==null){
            return l2;
        }
        if(l2==null){
            return l1;
        }
        ListNode head = l1;
        ListNode cur = l1;
        //进位信息
        int count = 0;
        while(l1!=null&&l2!=null){
            cur = l1;
            //相加
            int val = l1.val+l2.val+count;
            cur.val = val%10;
            count = val>=10? 1:0;
            l1 = l1.next;
            l2 = l2.next;
        }
        //当l1较长，l2较短时
        while(l1!=null){
            cur.next = l1;
            cur = l1;
            int val = l1.val+count;
            count = val>=10? 1:0;
            cur.val = val%10;
            //因为val<10时，必不可能进位，所以可以直接跳出循环
            if(val<10){
                break;
            }
            l1 = l1.next;
        }
        //同理
        while(l2!=null){
            cur.next = l2;
            cur = l2;
            int val = l2.val+count;
            cur.val = val%10;
            count = val>=10?1:0;
            if(val<10){
                break;
            }
            l2 = l2.next;
        }
        //如果最后还有进位，则新建一个节点插入到尾部
        if(count==1){
            cur.next = new ListNode(1);
        }
        return head;
    }
}
```

