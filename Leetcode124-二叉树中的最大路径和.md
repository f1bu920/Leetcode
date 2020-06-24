---
title: Leetcode124.二叉树中的最大路径和
date: 2020-06-21 12:53:16
categories: Leetcode
tags:
  - 树
  - 递归
---

## Leetcode124.二叉树中的最大路径和

给定一个非空二叉树，返回其最大路径和。

本题中，路径被定义为一条从树中任意节点出发，达到任意节点的序列。该路径至少包含一个节点，且不一定经过根节点。

[题目链接](https://leetcode-cn.com/problems/binary-tree-maximum-path-sum)

<!--more-->

示例 1:

    输入: [1,2,3]
       1
      / \
     2   3
    输出: 6


示例 2:

```
输入: [-10,9,20,null,null,15,7]

   -10
   / \
  9  20
    /  \
   15   7

输出: 42
```



### 思路

创建递归函数`private int getMaxPath(TreeNode root)`，其返回以`root`为根节点的树的最大贡献值。

树中一个节点的最大路径和取决于该节点的值与该节点的左右子节点的最大贡献值。如果子节点最大贡献值为正，则计入该节点的最大路径和，否则不计入。维护一个全局变量`maxRoute`存储最大路径和，在递归中更新这个最大值。



### 代码实现

```java
class Solution {
    int maxRoute = Integer.MIN_VALUE;

    public int maxPathSum(TreeNode root) {
        getMaxPath(root);
        return maxRoute;
    }

    private int getMaxPath(TreeNode root){
        if (root == null) {
            return 0;
        }
        int left = Math.max(getMaxPath(root.left), 0);
        int right = Math.max(getMaxPath(root.right), 0);
        maxRoute = Math.max(maxRoute, left + right + root.val);
        return root.val + Math.max(left, right);
    }
}
```

