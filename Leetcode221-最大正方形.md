---
title: Leetcode221.最大正方形
date: 2020-05-12 08:36:59
categories: Leetcode
tags:
  - 动态规划
---

## Leetcode221.最大正方形

在一个由 0 和 1 组成的二维矩阵内，找到只包含 1 的最大正方形，并返回其面积。

[题目链接](https://leetcode-cn.com/problems/maximal-square)

<!--more-->

示例:

```
输入: 

1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0

输出: 4
```

#### 思路

- 暴力法

  遍历整个数组，以每个`1`为正方形的左上角，找到正方形的最大边长`maxSize`，最大面积即为最大边长的平方。

  - 确认左上角后，根据此元素所在的行和列确认可能的最大正方形的边长。因为不能超出矩形的最大行和最大列，所以当前可能的最大边长为`currentMaxSize=Math.min(row-i,col-j)`。
  - 每次在下方新增一行，在右方新增一列，判断新增的行和列是否都为`1`。

- 动态规划

  令`dp[i][j]`代表以`i`、`j`为右下角且只包含1的正方形的最大边长。对于每个位置`(i, j)`，我们有：

  - 如果为`0`，那么`dp[i][j]=0`，因为此位置不可能在正方形中。

  - 如果为`1`，则
    $$
    dp[i][j] = min(dp[i-1][j], dp[i][j-1],dp[i-1][j-1])+1
    $$
    由其左方、上方、左上方的`dp`决定。

  此外，当`i`和`j`至少有一个为0时，如果`matrix[i][j]='1'`，则`dp[i][j]=1`，且只能为1。

#### 代码实现

- 暴力法

```java
class Solution {
    public int maximalSquare(char[][] matrix) {
        int maxSize = 0;
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return 0;
        }
        int row = matrix.length;
        int col = matrix[0].length;
        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                if (matrix[i][j] == '1') {
                    maxSize = Math.max(maxSize, 1);
                    //当前可能的最大边长
                    int currentMaxSize = Math.min(row - i, col - j);
                    for (int k = 1; k < currentMaxSize; k++) {
                        if (matrix[i + k][j + k] == '0') {
                            break;
                        }
                        boolean flag = true;
                        //在下方新增一行，在右方新增一列
                        for (int l = 0; l < k; l++) {
                            if (matrix[i + k][j + l] == '0' || matrix[i + l][j + k] == '0') {
                                flag = false;
                                break;
                            }
                        }
                        if (flag) {
                            maxSize = Math.max(maxSize, k + 1);
                        } else
                            break;
                    }
                }
            }
        }
        return maxSize * maxSize;
    }
}
```

- 动态规划

```java
class Solution {
    public int maximalSquare(char[][] matrix) {
        int maxSize = 0;
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return 0;
        }
        int row = matrix.length;
        int col = matrix[0].length;
        int[][] dp = new int[row][col];
        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                if (matrix[i][j] == '1') {
                    //至少有一个为0
                    if (i == 0 || j == 0) {
                        dp[i][j] = 1;
                    } else {
                        //左方、上方、左上方三者取小再+1
                        dp[i][j] = Math.min(Math.min(dp[i][j - 1], dp[i - 1][j]), dp[i - 1][j - 1]) + 1;
                    }
                    maxSize = Math.max(maxSize, dp[i][j]);
                }
            }
        }
        return maxSize * maxSize;
    }
}
```