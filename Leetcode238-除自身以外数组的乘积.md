---
title: Leetcode238.除自身以外数组的乘积
date: 2020-06-04 09:15:52
categories: Leetcode
tags:
  - 动态规划
  - Array
---

## Leetcode238.除自身以外数组的乘积

给你一个长度为 `n` 的整数数组 `nums`，其中 `n > 1`，返回输出数组 `output` ，其中 `output[i]` 等于 `nums` 中除 `nums[i]` 之外其余各元素的乘积。

 [题目链接](https://leetcode-cn.com/problems/product-of-array-except-self)

<!--more-->

示例:

```
输入: [1,2,3,4]
输出: [24,12,8,6]
```




提示：题目数据保证数组之中任意元素的全部前缀元素和后缀（甚至是整个数组）的乘积都在 32 位整数范围内。

说明: 请不要使用除法，且在 O(n) 时间复杂度内完成此题。

进阶：
你可以在常数空间复杂度内完成这个题目吗？（ 出于对空间复杂度分析的目的，输出数组不被视为额外空间。）



#### 思路

与[Leetcode152.乘积的最大数组]([https://f1bu920.github.io/2020/05/18/Leetcode152-%E4%B9%98%E7%A7%AF%E6%9C%80%E5%A4%A7%E5%AD%90%E6%95%B0%E7%BB%84/](https://f1bu920.github.io/2020/05/18/Leetcode152-乘积最大子数组/))类似，都采用动态规划来存储已经计算过的值。

令·`dp[i][0]`代表`nums[i]`左边的乘积，`dp[i][1]`代表`nums[i]`右边的乘积。所以可以很轻易的得到状态转移方程$dp[i][0] = dp[i-1][0]*nums[i-1]$、$dp[i][1] = dp[i+1][1]*nums[i+1]$。

考虑初始化：第一位的左侧乘积和最后一位的右侧乘积都为1：`dp[0][0]=1;dp[len-1][1]=1`。

最后将`dp[i][0]`与`dp[i][1]`相乘就是结果。



**此题的进阶解法中要求空间复杂度为常数级别，所以只需对上述解法做些许调整即可。****

1. **构造结果数组`output`，对于`output[i]`代表`i`左侧的数组乘积。构造方式与`dp[i][0]`相同。**
2. **因为不能使用额外的数组，所以使用一个变量`R`来记录右侧的乘积，从后往前遍历，与`dp[i][1]`相同。**

#### 代码实现

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        if (nums == null || nums.length == 0) {
            return new int[0];
        }
        int len = nums.length;
        int[] output = new int[len];
        int[][] dp = new int[len][2];
        dp[0][0] = 1;
        dp[len - 1][1] = 1;
        for (int i = 1; i < len; i++) {
            dp[i][0] = dp[i - 1][0] * nums[i - 1];
        }
        for (int i = len - 2; i >= 0; i--) {
            dp[i][1] = dp[i + 1][1] * nums[i + 1];
        }
        for (int i = 0; i < len; i++) {
            output[i] = dp[i][0] * dp[i][1];
        }
        return output;
    }
}
```

- 进阶解法

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        if (nums == null || nums.length == 0) {
            return new int[0];
        }
        int len = nums.length;
        int[] output = new int[len];
        output[0] = 1;
        //output[i]表示i左侧所有元素的乘积
        for (int i = 1; i < len; i++) {
            output[i] = output[i - 1] * nums[i - 1];
        }
        //R表示i右侧所有元素的乘积
        int R = 1;
        for (int i = len - 1; i >= 0; i--) {
            //对于i，左侧的乘积为output[i]，右侧乘积为R
            output[i] = output[i] * R;
            //R需要包括右侧所有元素的乘积，所以计算下一个结果时需要将当前值乘到R上
            R = R * nums[i];
        }
        return output;
    }
}
```

