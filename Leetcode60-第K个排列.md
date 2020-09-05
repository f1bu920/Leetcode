---
title: Leetcode60.第K个排列
date: 2020-09-05 10:01:44
categories: Leetcode
tags:
  - 回溯
---

## Leetcode60.第K个排列

给出集合 [1,2,3,…,n]，其所有元素共有 n! 种排列。

按大小顺序列出所有排列情况，并一一标记，当 n = 3 时, 所有排列如下：

```
"123"
"132"
"213"
"231"
"312"
"321"
```



给定 n 和 k，返回第 k 个排列。

说明：

给定 n 的范围是 [1, 9]。
给定 k 的范围是[1,  n!]。

[题目链接](https://leetcode-cn.com/problems/permutation-sequence)

<!--more-->

示例 1:

```
输入: n = 3, k = 3
输出: "213"
```



示例 2:

```
输入: n = 4, k = 9
输出: "2314"
```



### 思路

每进入一个分支，可以根据已经选择的数的个数计算出未选择的数的个数，计算其阶乘可以得到这一分支的排列个数`count`：

- 如果`k`小于等于`count`，则所求排列一定在这个分支中，递归求解；
- 否则，直接跳过这一分支，剪枝。

创建一个全局数组来存储`n`个数的阶乘。

### 代码实现

```java
class Solution {
    int n;
    int k;
    int[] factorial;

    public String getPermutation(int n, int k) {
        this.n = n;
        this.k = k;
        factorial = new int[n + 1];
        calculateFactorial(n);
        boolean[] used = new boolean[n + 1];
        StringBuilder path = new StringBuilder();
        dfs(0, path, used);
        return path.toString();
    }

    private void dfs(int index, StringBuilder path, boolean[] used) {
        if (index == n) {
            return;
        }
        //这一分支下的排列个数
        int count = factorial[n - 1 - index];
        for (int i = 1; i <= n; i++) {
            if (!used[i]) {
                if (count < k) {
                    k -= count;
                    continue;
                }
                used[i] = true;
                path.append(i);
                dfs(index + 1, path, used);
                //没必要进行回溯
                return;
            }
        }
    }
    //计算阶乘
    private void calculateFactorial(int n) {
        factorial[0] = 1;
        for (int i = 1; i <= n; i++) {
            factorial[i] = i * factorial[i - 1];
        }
    }
}
```



