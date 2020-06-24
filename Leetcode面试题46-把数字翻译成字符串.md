---
title: Leetcode面试题46.把数字翻译成字符串
date: 2020-06-09 08:46:19
categories: Leetcode
tags:
  - 动态规划
---

## Leetcode面试题46.把数字翻译成字符串

给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

 [题目链接](https://leetcode-cn.com/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof)

<!--more-->

示例 1:

```
输入: 12258
输出: 5
解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"
```




提示：

- 0 <= num < 231



#### 思路

与[Leetcode198.打家劫舍](https://leetcode-cn.com/problems/house-robber/)类似，可以用`dp[i]`来表示以第`i`位结尾的前缀串翻译的个数，对于第`i`个位置，有如下的翻译规则：

- 可以当作单独一位来翻译
- 如果第`i-1`位和第`i`位可以一起翻译，即大于等于10且小于等于25，就连起来翻译。

可以得到状态转移方程：$dp[i] = dp[i-1] + dp[i-2],[10<=x<=25]$

其中，`x`代表第`i-1`位与第`i`位连在一起得到的数字。如果不满足后面条件，则$dp[i] = d[i-1]$.

**注意：当满足`10<=x<=25`时还要判断`i`是否大于等于2，否则会数组下标越界，可以将`i=1`单独考虑。**



#### 代码实现

```java
class Solution {
    public int translateNum(int num) {
        String str = String.valueOf(num);
        int len = str.length();
        int[] dp = new int[len];
        dp[0] = 1;
        for (int i = 1; i < len; i++) {
            //一定可以单独翻译
            dp[i] = dp[i - 1];
            String pre = str.substring(i - 1, i + 1);
            //可以连起来翻译的条件
            if (pre.compareTo("10") >= 0 && pre.compareTo("25") <= 0) {
                //i=1单独讨论
                if (i != 1) {
                    dp[i] += dp[i - 2];
                } else {
                    dp[i] = 2;
                }
            }
        }
        return dp[len - 1];
    }
}
```



