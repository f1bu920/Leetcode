---
title: Leetcode338.比特位计数
date: 2020-07-19 17:03:16
categories: Leetcode
tags:
  - 位运算
  - 动态规划
---

## Leetcode338.比特位计数

给定一个非负整数 num。对于 0 ≤ i ≤ num 范围中的每个数字 i ，计算其二进制数中的 1 的数目并将它们作为数组返回。

[题目链接](https://leetcode-cn.com/problems/counting-bits)

<!--more-->

示例 1:

```
输入: 2
输出: [0,1,1]
```



示例 2:

```
输入: 5
输出: [0,1,1,2,1,2]
```



进阶:

- 给出时间复杂度为O(n*sizeof(integer))的解答非常容易。但你可以在线性时间O(n)内用一趟扫描做到吗？
  要求算法的空间复杂度为O(n)。
- 你能进一步完善解法吗？要求在C++或任何其他语言中不使用任何内置函数（如 C++ 中的 __builtin_popcount）来执行此操作。



### 思路及代码实现

直接通过右移运算判断每个数字的二进制中1的个数。

```java
class Solution {
    public int[] countBits(int num) {
        int[] result = new int[num + 1];
        for (int i = 0; i <= num; i++) {
            int x = i;
            //计数
            int count = 0;
            while (x != 0) {
                //判断尾数是否是1
                if ((x & 1) == 1) {
                    count++;
                }
                x = x >> 1;
            }
            result[i] = count;
        }
        return result;
    }
}
```



[动态规划](https://leetcode-cn.com/problems/counting-bits/solution/bi-te-wei-ji-shu-by-leetcode/)

