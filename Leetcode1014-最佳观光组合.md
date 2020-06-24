---
title: Leetcode1014.最佳观光组合
date: 2020-06-17 08:25:38
categories: Leetcode
tags:
  - Array
---

## Leetcode1014.最佳观光组合

给定正整数数组 `A`，`A[i]` 表示第 `i `个观光景点的评分，并且两个景点 `i `和 `j` 之间的距离为 `j - i`。

一对景点（`i < j`）组成的观光组合的得分为（`A[i] + A[j] + i - j`）：**景点的评分之和减去它们两者之间的距离。**

返回一对观光景点能取得的最高分。

 [题目链接](https://leetcode-cn.com/problems/best-sightseeing-pair/)

<!--more-->

示例：

```
输入：[8,1,5,2,6]
输出：11
解释：i = 0, j = 2, A[i] + A[j] + i - j = 8 + 5 + 0 - 2 = 11
```




提示：

- 2 <= A.length <= 50000
- 1 <= A[i] <= 1000



### 思路

因为数据量最大为50000，所以用暴力法n的二次方的时间按复杂度会超时。

优化：**因为得分公式可以分成两部分`A[i]+i`和`A[j]-j`，**统计答案时，因为对于当前遍历的`A[j]-j`是不变的，所以就等价于求`[0,j-1]`区间中`A[i]+i`的最大值`m`，而`m`可以边遍历边维护。



### 代码实现

- 暴力法

```java
class Solution {
    public int maxScoreSightseeingPair(int[] A) {
        int len = A.length;
        int maxScore = A[0] + A[1] - 1;
        for (int i = 0; i < len - 1; i++) {
            for (int j = i + 1; j < len; j++) {
                maxScore = Math.max(maxScore, A[j] + A[i] + i - j);
            }
        }
        return maxScore;        
    }
}
```

超出时间限制

- 优化后

```java
class Solution {
    public int maxScoreSightseeingPair(int[] A) {
        int len = A.length;
        int maxScore = A[0] + A[1] - 1;
        int m = A[0];
        for (int j = 1; j < len; j++) {
            //A[i]+i在[0,j-1]区间上的最大值
            m = Math.max(m, A[j - 1] + j - 1);
            maxScore = Math.max(maxScore, m + A[j] - j);
        }
        return maxScore;     
    }
}
```

