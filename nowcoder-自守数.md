---
title: nowcoder.自守数
date: 2020-06-13 08:42:54
categories: nowcoder
tags:
  - Math
---

## nowcoder.自守数

### 题目描述

自守数是指一个数的平方的尾数等于该数自身的自然数。例如：25^2 = 625，76^2 = 5776，9376^2 = 87909376。请求出n以内的自守数的个数



接口说明


/*
功能: 求出n以内的自守数的个数


输入参数：
int n

返回值：
n以内自守数的数量。
*/



public static int CalcAutomorphicNumbers( int n)
{
/*在这里实现功能*/

return 0;

}

本题有多组输入数据，请使用while(cin>>)等方式处理

[题目链接](https://www.nowcoder.com/practice/88ddd31618f04514ae3a689e83f3ab8e?tpId=37&&tqId=21322&rp=1&ru=/activity/oj&qru=/ta/huawei/question-ranking)

<!--more-->



### 输入描述:

```
int型整数
```

### 输出描述:

```
n以内自守数的数量。
```

示例1

### 输入

```
2000
```

### 输出

```
8
```



### 思路

由数学知识可知，一个数是自守数的前提是其个位数为1、5、6，这样其平方数的个位才能与这个数的个位对应上。

此外，确定一个数是否是自守数，首先需要确定这个数的位数`t`，然后通过取余操作找到其平方数的后`t`个数，对比相同则计数器加一。



### 代码实现

```java
import java.util.*;
public class Main{
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        while (sc.hasNextInt()) {
            int n = sc.nextInt();
            //count初始化为1是因为0也是自守数
            int count = 1;
            for (int i = 1; i <= n; i++) {
                if (i % 10 == 5 || i % 10 == 6 || i % 10 == 1) {
                    //平方数
                    int square = i * i;
                    //这个数的位数
                    int t = 0;
                    int x = i;
                    while (x != 0) {
                        x /= 10;
                        t++;
                    }
                    //取余判断是否相等
                    if (square % (Math.pow(10, t)) == i) {
                        count++;
                    }
                }
            }
            System.out.println(count);
        }
    }
}
```

