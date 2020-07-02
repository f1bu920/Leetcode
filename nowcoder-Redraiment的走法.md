---
title: nowcoder.Redraiment的走法
date: 2020-06-12 09:39:49
categories: nowcoder
tags:
  - 动态规划
---

## nowcoder.Redraiment的走法

### 题目描述

题目描述 

  Redraiment是走梅花桩的高手。Redraiment总是起点不限，从前到后，往高的桩子走，但走的步数最多，不知道为什么？你能替Redraiment研究他最多走的步数吗？ 

 

样例输入

6

2 5 1 5 4 5

 

样例输出

3

 

提示

Example: 
6个点的高度各为 2 5 1 5 4 5 
如从第1格开始走,最多为3步, 2 4 5 
从第2格开始走,最多只有1步,5 
而从第3格开始走最多有3步,1 4 5 
从第5格开始走最多有2步,4 5

所以这个结果是3。

 

接口说明

方法原型：

  int GetResult(int num, int[] pInput, List pResult);

输入参数：
  int num：整数，表示数组元素的个数（保证有效）。
  int[] pInput: 数组，存放输入的数字。

输出参数：
  List pResult: 保证传入一个空的List，要求把结果放入第一个位置。
返回值：
 正确返回1，错误返回0

 [链接](https://www.nowcoder.com/practice/24e6243b9f0446b081b1d6d32f2aa3aa?tpId=37&&tqId=21326&rp=1&ru=/activity/oj&qru=/ta/huawei/question-ranking)

<!--more-->

### 输入描述:

```
输入多行，先输入数组的个数，再输入相应个数的整数
```

### 输出描述:

```
输出结果
```

示例1

### 输入

```
6
2
5
1
5
4
5
```

### 输出

```
3
```



### 思路

每次走桩都是从前往后，往高的地方走，因此可以转化为求最长递增子序列的问题。

令`dp[i]`代表从开始处到`i`处的递增子序列长度，最后 找到`dp`中的最大值即可。



### 代码实现

```java
import java.util.*;
public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        while(sc.hasNextInt()){
            int num = sc.nextInt();
            int[] pInput = new int[num];
            for(int i = 0;i<num;i++){
                pInput[i] = sc.nextInt();
            }
            GetResult(num,pInput);
        }
    }
    static int GetResult(int num, int[] pInput){
        int[] dp = new int[num];
        //求增长子序列
        for(int i = 0;i<num;i++){
            dp[i] = 1;
            for(int j = 0;j<i;j++){
                if(pInput[j]<pInput[i]){
                    dp[i] = Math.max(dp[i], dp[j]+1);
                }
            }
        }
        //找到增长子序列的最大值
        int max = dp[0];
        for(int i = 0;i<num;i++){
            max = Math.max(max,dp[i]);
        }
        System.out.println(max);
        return max;
    }
}
```

