---
title: nowcoder.求最小公倍数
date: 2020-06-10 09:24:02
categories: nowcoder
tags:
  - 递归
  - Math
---

## nowcoder.求最小公倍数

### 题目描述

正整数A和正整数B 的最小公倍数是指 能被A和B整除的最小的正整数值，设计一个算法，求输入A和B的最小公倍数.

<!--more-->

### 输入描述:

```
输入两个正整数A和B。
```

### 输出描述:

```
输出A和B的最小公倍数。
```

示例1

### 输入

```
5 7
```

### 输出

```
35
```



### 思路

- 法一：

  令`i=A`，每次递增`A`，直到`i%B==0`。

- 递归：

  先求出最大公约数，则最小公倍数等于两个数乘积除以他们的最大公约数。



### 代码实现

- 法一：

```java
import java.io.*;
public class Main{
    public static void main(String[] args) throws IOException{
        BufferedReader bf = new BufferedReader(new InputStreamReader(System.in));
        String[] str = bf.readLine().trim().split(" ");
        int A = Integer.parseInt(str[0]);
        int B = Integer.parseInt(str[1]);
        for(int i = A;i<=A*B;i+=A){
            if(i%B==0){
                System.out.print(i);
                break;
            }
        }
    }
}
```



- 递归

```java
import java.io.*;
public class Main{
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        String[] str = bufferedReader.readLine().trim().split(" ");
        int A = Integer.parseInt(str[0]);
        int B = Integer.parseInt(str[1]);
        //最小公倍数=两数乘积除以最大公约数
        System.out.println(A * B / gcd(A, B));
    }
    //求最大公约数
    private static int gcd(int A, int B) {
        return B != 0 ? gcd(B, A % B) : A;
    }
}
```

