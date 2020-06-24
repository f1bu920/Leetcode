---
title: Leetcode69.x的平方根
date: 2020-06-17 13:47:44
categories: Leetcode
tags:
  - 牛顿迭代法
  - 二分搜索
---

## Leetcode69.x的平方根

实现 `int sqrt(int x)` 函数。

计算并返回 `x` 的平方根，其中 `x `是非负整数。

由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。

[题目链接](https://leetcode-cn.com/problems/sqrtx)

<!--more-->

[牛顿迭代法wiki](https://oi-wiki.org/math/newton/)

示例 1:

输入: 4
输出: 2
示例 2:

输入: 8
输出: 2
说明: 8 的平方根是 2.82842..., 
     由于返回类型是整数，小数部分将被舍去。



### 思路

牛顿迭代法的公式为：$X_{i+1} = X_{i}-f(x_{i})/f'(x_{i})$。

对应此题求平方根就是$X_{i+1} = (X_{i}+n/X_{i})/2$。

### 代码实现

```java
class Solution {
    public int mySqrt(int x) {
        if(x==0){
            return 0;
        }
        //精确度
        double e = 1e-15;
        double n = x;
        while(true){
            //nx即为X（i+1）
            double nx = (n+x/n)/2;
            //如果小于这个精确度就退出循环
            if(Math.abs(nx-n)<=e){
                break;
            }
            n = nx;
        }
        return (int) n;
    }
}
```

