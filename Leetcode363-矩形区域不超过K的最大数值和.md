---
title: Leetcode363.矩形区域不超过K的最大数值和
date: 2021-04-22 13:56:38
categories: Leetcode
tags:
  - 动态规划
---

## Leetcode363.矩形区域不超过K的最大数值和

给你一个 m x n 的矩阵 matrix 和一个整数 k ，找出并返回矩阵内部矩形区域的不超过 k 的最大数值和。

题目数据保证总会存在一个数值和不超过 k 的矩形区域。

[题目链接](https://leetcode-cn.com/problems/max-sum-of-rectangle-no-larger-than-k)

<!--more-->

示例 1：

输入：matrix = [[1,0,1],[0,-2,3]], k = 2
输出：2
解释：蓝色边框圈出来的矩形区域 [[0, 1], [-2, 3]] 的数值和是 2，且 2 是不超过 k 的最大数字（k = 2）。
示例 2：

输入：matrix = [[2,2,-1]], k = 3
输出：3


提示：

- m == matrix.length
- n == matrix[i].length
- 1 <= m, n <= 100
- -100 <= matrix[i][j] <= 100
- -105 <= k <= 105



### 思路

先固定左边界，枚举右边界，使用`dp[i]`记录两个边界中间每一行的和，然后在`dp`数组中找到不超过k的连续子数组和的最大值。



### 代码实现

```java
class Solution {
    public int maxSumSubmatrix(int[][] matrix, int k) {
        int m = matrix.length;
        int n = matrix[0].length;
        int max = Integer.MIN_VALUE;
        //固定左边界
        for (int l = 0; l < n; l++) {
            //记录两个边界之间数字之和
            int[] dp = new int[m];
            //枚举右边界
            for (int r = l; r < n; r++) {
                for (int i = 0; i < m; i++) {
                    dp[i] += matrix[i][r];
                }
                max = Math.max(max, dpmax(dp, k));
                if (max == k) {
                    return k;
                }
            }
        }
        return max;
    }

    //找连续子数组之和不超过k的最大值
    private int dpmax(int[] arr, int k) {
        int max = Integer.MIN_VALUE;
        for (int l = 0; l < arr.length; l++) {
            int sum = 0;
            for (int r = l; r < arr.length; r++) {
                sum += arr[r];
                if (sum > max && sum <= k) {
                    max = sum;
                }
                if (max == k) {
                    return k;
                }
            }
        }
        return max;
    }
}
```



