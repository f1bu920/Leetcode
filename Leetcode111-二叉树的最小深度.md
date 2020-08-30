---
title: Leetcode111.二叉树的最小深度
date: 2020-08-30 09:46:37
categories: Leetcode
tags:
  - 深度优先搜素
  - 递归
---

## Leetcode111.二叉树的最小深度

给定一个二叉树，找出其最小深度。

最小深度是从根节点到最近叶子节点的最短路径上的节点数量。

说明: 叶子节点是指没有子节点的节点。

[题目链接](https://leetcode-cn.com/problems/minimum-depth-of-binary-tree)

<!--more-->

示例:

```
给定二叉树 [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回它的最小深度  2.
```



### 思路

最小深度的意思是最近叶子节点到根节点的距离，所以

```
  1
 / 
2
```

这棵二叉树的最小深度是2而不是1.使用`left`和`right`分别记录左子节点和右子节点的最小深度，所以总最小深度就是`left`和`right`的较小值。



### 代码实现

```java
class Solution {
    public int minDepth(TreeNode root) {
        if(root==null){
            return 0;
        }
        if(root.left==null&&root.right==null){
            return 1;
        }
        int left = Integer.MAX_VALUE;
        int right = Integer.MAX_VALUE;
        //注意要进行子节点判断不为空
        if(root.left!=null){
            left = 1+minDepth(root.left);
        }
        if(root.right!=null)
            right = 1+minDepth(root.right);
        return Math.min(left,right);
    }
}
```

