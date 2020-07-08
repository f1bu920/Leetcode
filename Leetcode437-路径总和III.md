---
title: Leetcode437.路径总和III
date: 2020-07-08 09:00:39
categories: Leetcode
tags:
  - 树
  - 递归
  - 先序遍历
---

## Leetcode437.路径总和III

给定一个二叉树，它的每个结点都存放着一个整数值。

找出路径和等于给定数值的路径总数。

路径不需要从根节点开始，也不需要在叶子节点结束，但是路径方向必须是向下的（只能从父节点到子节点）。

二叉树不超过1000个节点，且节点数值范围是 [-1000000,1000000] 的整数。

[题目链接](https://leetcode-cn.com/problems/path-sum-iii)

<!--more-->

示例：

    root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8
    	  10
    	 /  \
    	5   -3
       / \    \
      3   2   11
     / \   \
    3  -2   1
    
    返回 3。和等于 8 的路径有:
    
    1.  5 -> 3
    2.  5 -> 2 -> 1
    3.  -3 -> 11


### 思路

递归方式，因为只能从父节点到子节点，所以每次需要计算三次，即当前根节点计算一次，再递归调用根节点的左右子节点。计算当前节点时，若当前节点为空，则返回0；否则`sum`减去当前节点的值，若`sum==0`，则找到了一条路径；否则接着递归调用计算当前节点的左右子节点，最后将三者之和相加即可。



### 代码实现

```java
class Solution {
    public int pathSum(TreeNode root, int sum) {
        if (root == null) {
            return 0;
        }
        //计算以当前节点为起点的路径和
        int current = countSum(root, sum);
        //以左子节点为起点
        int left = pathSum(root.left, sum);
        //以右子节点为起点
        int right = pathSum(root.right, sum);
        //三者相加即为答案
        return current + left + right;
    }
    //计算以root为根节点的路径和
    private int countSum(TreeNode root, int sum) {
        if (root == null) {
            return 0;
        }
        //每次sum减去当前节点的值
        sum -= root.val;
        //sum==0代表找到了一条路径
        int result = sum == 0 ? 1 : 0;
        //接着递归调用
        return result + countSum(root.left, sum) + countSum(root.right, sum);
    }
}
```

