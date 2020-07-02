---
title: nowcoder.记负均正
date: 2020-06-16 11:07:12
categories: nowcoder
tags:
  - Array
---

## nowcoder.记负均正

### 题目描述

首先输入要输入的整数个数n，然后输入n个整数。输出为n个整数中负数的个数，和所有正整数的平均值，结果保留一位小数。

[连接](https://www.nowcoder.com/practice/6abde6ffcc354ea1a8333836bd6876b8?tpId=37&&tqId=21320&rp=1&ru=/ta/huawei&qru=/ta/huawei/question-ranking)

<!--more-->

### 输入描述:

```
首先输入一个正整数n，
然后输入n个整数。
```

### 输出描述:

```
输出负数的个数，和所有正整数的平均值。
```

示例1

### 输入

```
5
1
2
3
4
5
```

### 输出

```
0 3
```



### 思路

设置负数个数计数器`nNegative`、正整数个数计数器`nPositive`以及正整数和`sum`，每次输入时判断是否是负数即可。



### 代码实现

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        while (sc.hasNext()) {
            int n = sc.nextInt();
            int nNegative = 0;//负数个数
            int nPositive = 0;//正整数个数
            int sum = 0;//正整数的和
            for (int i = 0; i < n; i++) {
                int temp = sc.nextInt();
                if (temp < 0) {
                    nNegative++;
                }
                if (temp > 0) {
                    nPositive++;
                    sum += temp;
                }
            }
            System.out.printf("%d %.1f\n", nNegative, 1.0 * sum / nPositive);
        }
    }
}
```

