---
title: 剑指offerII 115.重建序列
date: 2022-7-23 16:40:38
categories: nowcoder
tags:
  - 剑指offer
  - 二叉树
---

## 剑指offerII 55.平衡二叉树

### 题目描述

输入一棵二叉树的根节点，判断该树是不是平衡二叉树。如果某二叉树中任意节点的左右子树的深度相差不超过1，那么它就是一棵平衡二叉树。

示例 1:

给定二叉树 [3,9,20,null,null,15,7]

    	3
       / \
      9  20
        /  \
       15   7
    返回 true 。
示例 2:

给定二叉树 [1,2,2,3,3,null,null,4,4]

           1
          / \
         2   2
        / \
       3   3
      / \
     4   4
    返回 false 。
 

限制：

```0 <= 树的结点个数 <= 10000```

 <!--more-->

[题目链接](https://leetcode.cn/problems/ping-heng-er-cha-shu-lcof)





### 思路

平衡二叉树的左右两颗子树的高度差不超过1，且两颗子树都是平衡二叉树。因此可用自底向上的递归法进行判断：对于遍历到的当前节点，先判断其左右子树是否平衡，再判断当前节点为根阶段的树是否平衡。



### 代码实现

```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        return height(root) >= 0;
    }
    // 获取树的高度,非平衡二叉树直接返回-1
    public int height(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int leftHeight = height(root.left);
        int rightHeight = height(root.right);
        if (leftHeight == -1 || rightHeight == -1 || Math.abs(leftHeight - rightHeight) > 1) {
            return -1;
        } else {
            return Math.max(leftHeight, rightHeight) + 1;
        }
    }
}
```

