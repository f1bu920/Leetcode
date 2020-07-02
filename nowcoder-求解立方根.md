---
title: nowcoder.求解立方根
date: 2020-06-11 10:22:25
categories: nowcoder
tags:
  - 二分查找
---

## nowcoder.求解立方根

### 题目描述

•计算一个数字的立方根，不使用库函数

详细描述：

•接口说明

原型：

public static double getCubeRoot(double input)

输入:double 待求解参数

返回值:double 输入参数的立方根，保留一位小数

[链接](https://www.nowcoder.com/practice/caf35ae421194a1090c22fe223357dca?tpId=37&&tqId=21330&rp=1&ru=/activity/oj&qru=/ta/huawei/question-ranking)

<!--more-->

## 输入描述:

```
待求解参数 double类型
```

### 输出描述:

```
输入参数的立方根 也是double类型
```

示例1

### 输入

```
216
```

### 输出

```
6.0
```



### 思路

利用二分查找，每次检查中间数的立方，如果刚好等于目标值，直接返回；如果小于目标值，将左边界移到`mid`处；如果大于目标值，将右边界移到`mid`处。

注意**循环退出条件需要将精度设置小一点。**



### 代码实现

```java
import java.util.*;
public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        while(sc.hasNext()){
            double input = sc.nextDouble();
            System.out.printf("%.1f\n",getCubeRoot(input));
        }
    }
    
    public static double getCubeRoot(double input){
        double left = 0;
        double right = input;
        while (right - left > 0.0001) {
            double mid = left + (right - left) / 2;
            double t = mid * mid * mid;
            if (t == input) {
                return mid;
            } else if (t < input) {
                left = mid;
            } else {
                right = mid;
            }
        }
        return left;
    }
}
```

