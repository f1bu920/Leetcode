---
title: Leetcode404.左叶子之和
date: 2020-09-19 09:57:57
categories: Leetcode
tags:
  - 树
  - 递归
---

## Leetcode404.左叶子之和

计算给定二叉树的所有左叶子之和。

[题目链接](https://leetcode-cn.com/problems/sum-of-left-leaves)

<!--more-->

示例：

    	3
       / \
      9  20
        /  \
       15   7
    
    在这个二叉树中，有两个左叶子，分别是 9 和 15，所以返回 24


### 思路与代码实现

```java
class Solution {
    public int sumOfLeftLeaves(TreeNode root) {
        if(root==null){
            return 0;
        }
        return sumOfLeftLeaves(root.left)+sumOfLeftLeaves(root.right)+
            //判断是否是左叶子节点
        (root.left!=null&&root.left.left==null&&root.left.right==null?root.left.val:0);
    }
}
```



