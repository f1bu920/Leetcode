---
title: nowcoder.201301 JAVA题目2-3级
date: 2020-06-11 07:59:34
categories: nowcoder
tags:
  - 动态规划
---

## nowcoder.201301 JAVA题目2-3级

### 题目描述

请编写一个函数（允许增加子函数），计算n x m的棋盘格子（n为横向的格子数，m为竖向的格子数）沿着各自边缘线从左上角走到右下角，总共有多少种走法，要求不能走回头路，即：只能往右和往下走，不能往左和往上走。

[题目链接](https://www.nowcoder.com/practice/e2a22f0305eb4f2f9846e7d644dba09b?tpId=37&&tqId=21314&rp=1&ru=/activity/oj&qru=/ta/huawei/question-ranking)

<!--more-->

### 输入描述:

```
输入两个正整数
```

### 输出描述:

```
返回结果
```

示例1

### 输入

```
2
2
```

### 输出

```
6
```



### 思路

运用动态规划的思想，将右下角坐标看作`(0,0)`，左上角坐标看作`(n,m)`。从左上角移动到右下角等价于从右下角移动到左上角，且只能向左向上移动。令`dp[i][j]`代表从`(0,0)`移动到`(i,j)`的走法数目，则可以得到状态转移方程**$dp[i][j] = dp[i][j-1]+dp[i-1][j],i>=1 AND j>=1$.**

考虑初始化：当处于边界时，即`i=0`或`j=0`时，`dp[i][j]`都为1.



### 代码实现

```java
import java.util.*;

public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        while (sc.hasNext()) {
            int n = sc.nextInt();
            int m = sc.nextInt();
            int[][] dp = new int[n + 1][m + 1];
            dp[0][0] = 0;
            dp[0][1] = dp[1][0] = 1;
            //初始化
            for (int i = 0; i <= m; i++) {
                dp[0][i] = 1;
            }
            for (int i = 0; i <= n; i++) {
                dp[i][0] = 1;
            }
            for (int i = 1; i <= n; i++) {
                for (int j = 1; j <= m; j++) {
                    dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
                }
            }
            System.out.println(dp[n][m]);
        }
    }
}
```

