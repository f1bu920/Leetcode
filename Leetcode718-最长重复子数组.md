---
title: Leetcode718.最长重复子数组
date: 2020-07-01 14:16:57
categories: Leetcode
tags:
  - 动态规划
  - Slide Windows
---

## Leetcode718.最长重复子数组

给两个整数数组 `A` 和 `B` ，返回两个数组中公共的、长度最长的子数组的长度。

**示例 1:**

```
输入:
A: [1,2,3,2,1]
B: [3,2,1,4,7]
输出: 3
解释: 
长度最长的公共子数组是 [3, 2, 1]。
```

**说明:**

1. 1 <= len(A), len(B) <= 1000
2. 0 <= A[i], B[i] < 100

[题目链接](https://leetcode-cn.com/problems/maximum-length-of-repeated-subarray/)

<!--more-->

### 思路

如果`A[i]==B[j]`，则`A[i:]`与`B[j:]`的最长公共前缀为`A[i+1:]`与`B[j+1:]`的最长公共前缀。

因此令 `dp[i][j]` 表示 `A[i:]` 和 `B[j:]` 的最长公共前缀，当`A[i]==B[j]`时，`dp[i][j] = dp[i+1][j+1]+1`；否则`dp[i][j] = 0`。

最后的结果就是`dp[i][j]`的最大值。



### 代码实现

```java
class Solution {
    public int findLength(int[] A, int[] B) {
        int a = A.length;
        int b = A.length;
        int[][] dp = new int[a+1][b+1];
        int maxLen = 0;
        //初始化
        dp[a][b] = 0;
        //从后往前遍历
        for(int i = a-1;i>=0;i--){
            for(int j = b-1;j>=0;j--){
                if(A[i]==B[j]){
                    dp[i][j] = dp[i+1][j+1]+1;
                }else{
                    dp[i][j] = 0;
                }
                maxLen = Math.max(maxLen,dp[i][j]);
            }
        }
        return maxLen;
    }
}
```

[官方题解](https://leetcode-cn.com/problems/maximum-length-of-repeated-subarray/solution/zui-chang-zhong-fu-zi-shu-zu-by-leetcode-solution/)

