---
title: Leetcode337.打家劫舍III
date: 2020-08-05 08:37:45
categories: Leetcode
tags:
  - 递归
  - 深度优先搜素
---

## Leetcode337.打家劫舍III

在上次打劫完一条街道之后和一圈房屋后，小偷又发现了一个新的可行窃的地区。这个地区只有一个入口，我们称之为“根”。 除了“根”之外，每栋房子有且只有一个“父“房子与之相连。一番侦察之后，聪明的小偷意识到“这个地方的所有房屋的排列类似于一棵二叉树”。 如果两个直接相连的房子在同一天晚上被打劫，房屋将自动报警。

计算在不触动警报的情况下，小偷一晚能够盗取的最高金额。

[题目链接](https://leetcode-cn.com/problems/house-robber-iii)

<!--more-->

示例 1:

    输入: [3,2,3,null,3,null,1]
    	 3
        / \
       2   3
        \   \ 
         3   1
    
    输出: 7 
    解释: 小偷一晚能够盗取的最高金额 = 3 + 3 + 1 = 7.

示例 2:

    输入: [3,4,5,1,3,null,1]
    	 3
    	/ \
       4   5
      / \   \ 
     1   3   1
    
    输出: 9
    解释: 小偷一晚能够盗取的最高金额 = 4 + 5 = 9.


### 思路

因为相邻节点不能偷，所有一共有两种情况：

1. 爷爷节点+四个孙子节点
2. 两个儿子节点

- 递归

  4个孙子的钱加上爷爷的钱，和两个儿子的钱取较大值。

- 动态规划

  令`int[] result = new int[2]`中`result[0]`表示当前节点不偷，`result[1]`表示当前节点偷。

  所以，`result[0] = max(left[0],left[1])+max(right[0],right[1])`;

  `result[1] = root.val+left[0]+right[0]`.



### 代码实现

- 递归

```java
class Solution {
    public int rob(TreeNode root) {
        return robDP(root);
    }
    private int robDP(TreeNode root){
        if(root==null){
            return 0;
        }
        int left = 0;
        int right = 0;
        //左孙子偷的钱
        if(root.left!=null){
            left = robDP(root.left.left)+robDP(root.left.right);
        }
        //右孙子偷的钱
        if(root.right!=null){
            right = robDP(root.right.left)+robDP(root.right.right);
        }
        //取大值
        return Math.max(root.val+left+right,robDP(root.left)+robDP(root.right));
    }
}
```

- 动态规划

```java
class Solution {
    public int rob(TreeNode root) {
        int[] result = robDP(root);
        return Math.max(result[0],result[1]);
    }
    private int[] robDP(TreeNode root){
        //dp[0]表示当前节点不偷，dp[1]表示当前节点偷
        int[] dp = new int[2];
        if(root==null){
            return dp;
        }
        int[] left = robDP(root.left);
        int[] right = robDP(root.right);
        dp[0] = Math.max(left[0],left[1])+Math.max(right[0],right[1]);
        dp[1] = root.val+left[0]+right[0];
        return dp;
    }
}
```



