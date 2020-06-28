---
title: Leetcode461.汉明距离
date: 2020-06-28 10:11:35
categories: Leetcode
tags:
  - 位运算
---

## Leetcode461.汉明距离

两个整数之间的汉明距离指的是这两个数字对应二进制位不同的位置的数目。

给出两个整数 `x` 和` y`，计算它们之间的汉明距离。

注意：
`0 ≤ x, y < 2^31`.

[题目链接](https://leetcode-cn.com/problems/hamming-distance)

<!--more-->

示例:

```
输入: x = 1, y = 4

输出: 2

解释:
1   (0 0 0 1)
4   (0 1 0 0)
       ↑   ↑

上面的箭头指出了对应二进制位不同的位置。
```



### 思路

从示例可以看出，汉明距离就是要统计两个数异或结果对应二进制数中`1`的数量。可以使用JDK中`Integer`自带的`bitCount`方法；也可以将异或结果右移统计1的数量。



### 代码实现

```java
class Solution {
    public int hammingDistance(int x, int y) {
        //异或结果
        int xor = x ^ y;
        //计数器
        int count = 0;
        while (xor != 0) {
            //和1相与，判断最后一位是否是1
            //也可以使用xor%2
            if ((xor & 1) == 1) {
                count++;
            }
            //右移一位
            xor = xor >> 1;
        }
        return count;
    }
}
```

```java
class Solution {
    public int hammingDistance(int x, int y) {
        return Integer.bitCount(x ^ y);
    }
}
```

