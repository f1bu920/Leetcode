---
title: Leetcode191.位1的个数
date: 2021-03-24 18:53:48
categories: Leetcode
tags:
  - 位运算
---

## Leetcode191.位1的个数

编写一个函数，输入是一个无符号整数（以二进制串的形式），返回其二进制表达式中数字位数为 '1' 的个数（也被称为汉明重量）。

 [原题链接](https://leetcode-cn.com/problems/number-of-1-bits/)

<!--more-->

提示：

请注意，在某些语言（如 Java）中，没有无符号整数类型。在这种情况下，输入和输出都将被指定为有符号整数类型，并且不应影响您的实现，因为无论整数是有符号的还是无符号的，其内部的二进制表示形式都是相同的。
在 Java 中，编译器使用二进制补码记法来表示有符号整数。因此，在上面的 示例 3 中，输入表示有符号整数 -3。


示例 1：

```
输入：00000000000000000000000000001011
输出：3
解释：输入的二进制串 00000000000000000000000000001011 中，共有三位为 '1'。
```



示例 2：

```
输入：00000000000000000000000010000000
输出：1
解释：输入的二进制串 00000000000000000000000010000000 中，共有一位为 '1'。
```



示例 3：

```
输入：11111111111111111111111111111101
输出：31
解释：输入的二进制串 11111111111111111111111111111101 中，共有 31 位为 '1'。
```




提示：

输入必须是长度为 32 的 二进制串 。


进阶：

如果多次调用这个函数，你将如何优化你的算法？



### 思路

`n & (n - 1)`的值为将n最右侧的1值为0后的值



### 代码实现

```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        //n & (n - 1)将最后一位1转变为0
        int t = n;
        int result = 0;
        while(t != 0){
            t &= (t - 1);
            result++;
        }
        return result;
    }
}
```

