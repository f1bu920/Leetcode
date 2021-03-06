---
title: Leetcode64.最小路径和
date: 2020-07-25 08:33:56
categories: Leetcode
tags:
  - 动态规划
---

## Leetcode64.最小路径和

给定一个包含非负整数的 m x n 网格，请找出一条从左上角到右下角的路径，使得路径上的数字总和为最小。

说明：每次只能向下或者向右移动一步。

[题目链接](https://leetcode-cn.com/problems/minimum-path-sum)

<!--more-->

示例:

```
输入:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
输出: 7
解释: 因为路径 1→3→1→1→1 的总和最小。
```



### 思路

动态规划，令`dp[i][j]`表示走到`(i,j)`位置的最小路径和。

状态转移方程为`dp[i][j] = Math.min(dp[i-1][j],dp[i][j-1])+grid[i][j]`。

初始化：第一行和第一列需要特殊考虑。



### 代码实现

```java
class Solution {
    public int minPathSum(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        int[][] dp = new int[m][n];
        dp[0][0] = grid[0][0];
        //第一行
        for(int i = 1;i<n;i++){
            dp[0][i] = dp[0][i-1]+grid[0][i];
        }
        //第一列
        for(int i = 1;i<m;i++){
            dp[i][0] = dp[i-1][0] + grid[i][0];
        }
        for(int i = 1;i<m;i++){
            for(int j = 1;j<n;j++){
                dp[i][j] = Math.min(dp[i-1][j],dp[i][j-1])+grid[i][j];
            }
        }
        return dp[m-1][n-1];
    }
}
```

