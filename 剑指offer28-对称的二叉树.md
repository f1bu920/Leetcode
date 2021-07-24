---
title: 剑指offer28.对称的二叉树
date: 2021-07-24 15:06:29
categories: 剑指offer
tags:
  - 树
  - 递归
---

## 剑指offer28.对称的二叉树

请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。

例如，二叉树 [1,2,2,3,4,4,3] 是对称的。

    	1
       / \
      2   2
     / \ / \
    3  4 4  3

但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:

    	1
       / \
      2   2
       \   \
       3    3
 [题目链接](https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof/)

<!--more-->

示例 1：

输入：root = [1,2,2,3,4,4,3]
输出：true
示例 2：

输入：root = [1,2,2,null,3,null,3]
输出：false


限制：

0 <= 节点个数 <= 1000



### 思路

递归，当`root == null`时，直接返回true；否则检查左右两颗子树，当左右节点同时为空时，返回true，当不是同时为空或值不相等时直接返回false；递归判断。

### 代码

```java
class Solution {
    public boolean isSymmetric(TreeNode root) {
        if(root == null){
            return true;
        }
        return check(root.left, root.right);
    }

    private boolean check(TreeNode leftNode, TreeNode rightNode){
        if(leftNode == null && rightNode == null){
            return true;
        }
        if(leftNode == null || rightNode == null || leftNode.val != rightNode.val){
            return false;
        }
        return check(leftNode.left, rightNode.right) && check(leftNode.right, rightNode.left);
    }
}
```

