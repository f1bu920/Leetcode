---
title: nowcoder.记负均正II
date: 2020-06-14 10:34:30
categories: nowcoder
tags:
  - Array
---

## nowcoder.记负均正II

### 题目描述

从输入任意个整型数，统计其中的负数个数并求所有非负数的平均值，结果保留一位小数。

[链接](https://www.nowcoder.com/practice/64f6f222499c4c94b338e588592b6a62?tpId=37&&tqId=21328&rp=1&ru=/activity/oj&qru=/ta/huawei/question-ranking)

<!--more-->

### 输入描述:

```
输入任意个整数
```

### 输出描述:

```
输出负数个数以及所有非负数的平均值
```

示例1

### 输入


```
-13
-4
-7
```

### 输出


```
3
0.0
```



### 思路

设置负数个数计数器`n`、非负数个数计数器`nPositive`以及非负数和`sum`，每次输入时判断是否是负数即可。



### 代码实现

```java
import java.util.*;
public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        double ans = 0;
        int n = 0;//负数个数
        int nPositive = 0;//非负数个数
        int sum = 0;
        while(sc.hasNextInt()){
            int num = sc.nextInt();
            if(num<0){
                n++;
            }else{
                nPositive++;
                sum+=num;
            }
        }
        System.out.println(n);
        System.out.printf("%.1f",(double) sum/nPositive);
    }
}
```

