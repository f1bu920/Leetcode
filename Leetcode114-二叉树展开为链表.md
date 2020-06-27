---
title: Leetcode114.二叉树展开为链表
date: 2020-06-27 10:20:23
categories: Leetcode
tags:
  - 树
  - 深度优先搜素
  - 栈
---

## Leetcode114.二叉树展开为链表

给定一个二叉树，原地将它展开为一个单链表。

 [题目链接](https://leetcode-cn.com/problems/flatten-binary-tree-to-linked-list)

<!--more-->

例如，给定二叉树

        1
       / \
      2   5
     / \   \
    3   4   6

将其展开为：

```
1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```



### 思路

从例子中可以看出展开成链表是用的二叉树的先序遍历，因此建立一个栈来进行先序遍历。

设置两个指针`pre`和`cur`，分别指向上一个元素和当前出栈元素。将`pre`的左指针设为`null`，右指针指向`cur`，更新`pre`。再将`cur`的左右非空子节点入栈。



### 代码实现

```java
class Solution {
    public void flatten(TreeNode root) {
        if (root == null) {
            return;
        }
        //栈
        LinkedList<TreeNode> stack = new LinkedList<>();
        TreeNode cur;
        //虚拟头节点
        TreeNode pre = new TreeNode(-1);
        stack.push(root);
        while (!stack.isEmpty()) {
            //出栈元素
            cur = stack.pop();
            //将上一个出栈元素的左指针指向null，右指针指向当前出栈元素
            pre.right = cur;
            pre.left = null;
            pre = cur;
            //左右非空子节点入栈
            if (cur.right != null) {
                stack.push(cur.right);
            }
            if (cur.left != null) {
                stack.push(cur.left);
            }
        }
    }
}
```

