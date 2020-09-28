---
title: Leetcode117.填充每个节点的下一个右侧节点指针II
date: 2020-09-28 19:16:17
categories: Leetcode
tags:
  - 树
  - 层序遍历
---

## Leetcode117.填充每个节点的下一个右侧节点指针II

给定一个二叉树

```java
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```



填充它的每个 `next` 指针，让这个指针指向其下一个右侧节点。如果找不到下一个右侧节点，则将 `next` 指针设置为 `NULL`。

初始状态下，所有 `next` 指针都被设置为 `NULL`。

 [题目链接](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node-ii)

<!--more-->

进阶：

你只能使用常量级额外空间。
使用递归解题也符合要求，本题中递归程序占用的栈空间不算做额外的空间复杂度。


示例：

![](https://f1bu920.github.io/images/Leetcode117填充每个结点的下一个右侧指针II.png)

```
输入：root = [1,2,3,4,5,null,7]
输出：[1,#,2,3,#,4,5,7,#]
解释：给定二叉树如图 A 所示，你的函数应该填充它的每个 next 指针，以指向其下一个右侧节点，如图 B 所示。
```




提示：

- 树中的节点数小于 6000
- -100 <= node.val <= 100



### 思路

利用队列存储每层中的所有节点，然后使用两个指针`pre`和`cur`不断遍历并修改他们的`next`指针。



### 代码实现

```java
class Solution {
    public Node connect(Node root) {
        if(root==null){
            return null;
        }
        LinkedList<Node> queue = new LinkedList(); 
        queue.add(root);
        while(!queue.isEmpty()){
            int size = queue.size();
            Node pre = null;
            //先设置pre为每层的第一个节点
            if(size>0){
                pre = queue.poll();
                pre.next = null;
                if(pre.left!=null){
                    queue.add(pre.left);
                }
                if(pre.right!=null){
                    queue.add(pre.right);
                }
            }
            //遍历每层的节点，并修改他们的next指针
            for(int i = 0;i<size-1;i++){
                Node cur = queue.poll();
                if(cur.left!=null){
                    queue.add(cur.left);
                }
                if(cur.right!=null){
                    queue.add(cur.right);
                }
                pre.next = cur;
                pre = cur;
            }
        }
        return root;
    }
}
```



