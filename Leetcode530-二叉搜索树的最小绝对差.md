---
title: Leetcode530.二叉搜索树的最小绝对差
date: 2020-10-12 09:27:32
categories: Leetcode
tags:
  - 树
---

## Leetcode530.二叉搜索树的最小绝对差

给你一棵所有节点为非负值的二叉搜索树，请你计算树中任意两节点的差的绝对值的最小值。

 [题目连接](https://leetcode-cn.com/problems/minimum-absolute-difference-in-bst)

<!--more-->

示例：

```
输入：

   1
    \
     3
    /
   2

输出：
1
```



解释：
最小绝对差为 1，其中 2 和 1 的差的绝对值为 1（或者 2 和 3）。


提示：

- 树中至少有 2 个节点。
- 本题与 783 https://leetcode-cn.com/problems/minimum-distance-between-bst-nodes/ 相同



### 思路

因为是二叉搜索树，所以中序遍历序列是一个递增的序列，利用两个变量分别记录上次和这次遍历的节点值，并用一份全局变量`minDiff`记录差绝对值的最小值。



### 代码实现

```java
class Solution {
    int minDiff = Integer.MAX_VALUE;
    int pre = Integer.MAX_VALUE;
    int cur = 0;
    public int getMinimumDifference(TreeNode root) {
        inOrder(root);
        return minDiff;
    }
    private void inOrder(TreeNode root){
        if(root==null){
            return;
        }
        inOrder(root.left);
        cur = root.val;
        minDiff = Math.min(Math.abs(cur-pre),minDiff);
        pre = cur;
        inOrder(root.right);
    }
}
```

