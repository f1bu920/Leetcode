---
title: Leetcode116.填充每个节点的下一个右侧节点指针
date: 2020-10-15 13:00:28
categories: Leetcode
tags:
  - 树
---

## Leetcode116.填充每个节点的下一个右侧节点指针

给定一个完美二叉树，其所有叶子节点都在同一层，每个父节点都有两个子节点。二叉树定义如下：

```
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```



填充它的每个 `next` 指针，让这个指针指向其下一个右侧节点。如果找不到下一个右侧节点，则将 `next` 指针设置为`NULL`。

初始状态下，所有 next 指针都被设置为`NULL`。

 [题目链接](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node)

<!--more-->

示例：

```
输入：{"$id":"1","left":{"$id":"2","left":{"$id":"3","left":null,"next":null,"right":null,"val":4},"next":null,"right":{"$id":"4","left":null,"next":null,"right":null,"val":5},"val":2},"next":null,"right":{"$id":"5","left":{"$id":"6","left":null,"next":null,"right":null,"val":6},"next":null,"right":{"$id":"7","left":null,"next":null,"right":null,"val":7},"val":3},"val":1}

输出：{"$id":"1","left":{"$id":"2","left":{"$id":"3","left":null,"next":{"$id":"4","left":null,"next":{"$id":"5","left":null,"next":{"$id":"6","left":null,"next":null,"right":null,"val":7},"right":null,"val":6},"right":null,"val":5},"right":null,"val":4},"next":{"$id":"7","left":{"$ref":"5"},"next":null,"right":{"$ref":"6"},"val":3},"right":{"$ref":"4"},"val":2},"next":null,"right":{"$ref":"7"},"val":1}

解释：给定二叉树如图 A 所示，你的函数应该填充它的每个 next 指针，以指向其下一个右侧节点
```




提示：

- 你只能使用常量级额外空间。
- 使用递归解题也符合要求，本题中递归程序占用的栈空间不算做额外的空间复杂度。



### 思路

一种很容易想到的思路就是层序遍历，将每层节点添加到队列中，但不满足常量级额外空间的约束。

另一种思路就是利用已经建立的上一层`next`指针：

一棵树中存在两种`next`指针，一种是连接同一个父节点的两个子节点间的指针，可通过`head.left.next = head.right`直接建立联系。

另一种是不同父节点间的指针，这种情况不能直接建立，需要借助上一层已经建立好的`next`指针，`head.right.next = head.next.left`.



### 代码实现

```java
class Solution {
    public Node connect(Node root) {
        if(root==null){
            return root;
        }
        //最左侧节点
        Node leftmost = root;
        //leftmost.left!=null代表还有下一层
        while(leftmost.left!=null){
            Node head = leftmost;
            while(head!=null){
                //第一种情况
                head.left.next = head.right;
                //第二种情况
                if(head.next!=null){
                    head.right.next = head.next.left;
                }
                head = head.next;
            }
            //进入下一层
            leftmost = leftmost.left;
        }
        return root;
    }
}
```



