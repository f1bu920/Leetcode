---
title: Leetcode142.环形链表II
date: 2020-09-16 11:25:07
categories: Leetcode
tags:
  - 链表
  - 双指针
---

## Leetcode142.环形链表II

给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。

为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。

说明：不允许修改给定的链表。

 [题目链接](https://leetcode-cn.com/problems/linked-list-cycle-ii)

<!--more-->

示例 1：

输入：head = [3,2,0,-4], pos = 1
输出：tail connects to node index 1
解释：链表中有一个环，其尾部连接到第二个节点。

![](https://f1bu920.github.io/images/circularlinkedlist.png)



进阶：
你是否可以不用额外空间解决此题？



### 思路

- 法一

  创建一个`Set`来存储访问过的节点，当遇到已访问的节点时即环的第一个节点。

- 法二

  [数学证明](https://leetcode-cn.com/problems/linked-list-cycle-ii/solution/linked-list-cycle-ii-kuai-man-zhi-zhen-shuang-zhi-/)

  利用快慢指针`fast`和`slow`，快指针每次走两步，慢指针每次走一步。

  - 如果没有环，指针会走到`null`处，直接返回`null`；
  - **有环时，使用快慢指针一定会相遇。相遇后，将快指针`fast`指针指向`head`，慢指针不动，同时每轮走一步，直到相遇。第二次相遇点就是环的入口。**



### 代码实现

- 哈希表

```java
public class Solution {
    public ListNode detectCycle(ListNode head) {
        Set<ListNode> visited = new HashSet();
        ListNode cur = head;
        while(cur!=null){
            if(visited.contains(cur)){
                return cur;
            }
            visited.add(cur);
            cur = cur.next;
        }
        return null;
    }
}
```

- 快慢指针

```java
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode fast = head;
        ListNode slow = head;
        while(true){
            if(fast==null||fast.next==null){
                return null;
            }
            fast = fast.next.next;
            slow = slow.next;
            //第一次相遇
            if(fast==slow){
                break;
            }
        }
        //构造第二次相遇
        fast = head;
        while(fast!=slow){
            fast = fast.next;
            slow = slow.next;
        }
        return slow;
    }
}
```

