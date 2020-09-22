---
title: Leetcode968.监控二叉树
date: 2020-09-22 09:55:33
categories: Leetcode
tags:
  - 动态规划
  - 深度优先遍历
  - 树
---

##  Leetcode968.监控二叉树

给定一个二叉树，我们在树的节点上安装摄像头。

节点上的每个摄影头都可以监视其父对象、自身及其直接子对象。

计算监控树的所有节点所需的最小摄像头数量。

 [题目链接](https://leetcode-cn.com/problems/binary-tree-cameras)

<!--more-->

示例 1：

![](https://f1bu920.github.io/images/Leetcode968监控二叉树.png)

```
输入：[0,0,null,0,0]
输出：1
解释：如图所示，一台摄像头足以监控所有节点。
```



提示：

- 给定树的节点数的范围是 [1, 1000]。
- 每个节点的值都是 0。



### 思路

假设当前节点是`root`，左右节点分别为`left`、`right`。覆盖以`root`节点为根的树有两种情况：

- 在根节点处安装摄像头，所以左右孩子节点也会被覆盖。只需保证`left`、`right`的子树被覆盖即可。
- 根结点处不安装摄像头，所以左右孩子节点必须有一个安装摄像头。

所以，可以维护三个状态：

- `dp[0]`：`root`必须安装摄像头，覆盖整棵树的摄像头数目；
- `dp[1]`：覆盖整棵树需要的摄像头数目，无论 root是否放置摄像头；
- `dp[2]`：覆盖两棵子树需要的摄像头数目，无论节点 root本身是否被监控到。



### 代码实现

```jav
class Solution {
    public int minCameraCover(TreeNode root) {
        if(root==null){
            return 0;
        }
        int[] dp = dfs(root);
        return dp[1];
    }
    private int[] dfs(TreeNode root){
        if(root==null){
            return new int[]{Integer.MAX_VALUE/2,0,0};
        }
        int[] left = dfs(root.left);
        int[] right = dfs(root.right);
        int[] dp = new int[3];
        dp[0] = left[2] + right[2] + 1;
        dp[1] = Math.min(dp[0],Math.min(left[0]+right[1],right[0]+left[1]));
        dp[2] = Math.min(dp[0],left[1]+right[1]);
        return dp;
    }
}
```



