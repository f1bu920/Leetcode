---
title: Leetcode面试题64.1+2+...+n
date: 2020-06-02 08:19:11
categories: Leetcode
tags:
  - 递归
  - 位运算
---

## Leetcode面试题64.1+2+...+n

求 1+2+...+n ，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。

 [题目链接](https://leetcode-cn.com/problems/qiu-12n-lcof)

<!--more-->

示例 1：

输入: n = 3
输出: 6
示例 2：

输入: n = 9
输出: 45


限制：

1 <= n <= 10000



#### 思路

不允许用循环和乘除,第一反应是用递归. 但递归也要用到`if`判断终止条件.

但可以应用逻辑运算符的短路效应:

- `A&&B`: 若`A=false`, 则`B`不会被执行.
- `A||B`: 若`A=true`, 则`B`不会被执行.

因为当`n=1`时需要终止递归, 所以可以利用短路效应`n>1&&sumNums(n-1)`.



#### 代码实现

```java
class Solution {
    int sum = 0;

    public int sumNums(int n) {
        boolean b = (n > 1) && sumNums(n - 1) > 0;
        sum += n;
        return sum;
    }
}
```



