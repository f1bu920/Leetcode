---
title: Nowcoder.DNA序列
date: 2020-08-04 12:27:52
categories: nowcoder
tags:
  - String
  - Slide Window
---

## Nowcoder.DNA序列

### 题目描述

一个DNA序列由A/C/G/T四个字母的排列组合组成。G和C的比例（定义为GC-Ratio）是序列中G和C两个字母的总的出现次数除以总的字母数目（也就是序列长度）。在基因工程中，这个比例非常重要。因为高的GC-Ratio可能是基因的起始点。

给定一个很长的DNA序列，以及要求的最小子序列长度，研究人员经常会需要在其中找出GC-Ratio最高的子序列。

 [题目连接](https://www.nowcoder.com/practice/e8480ed7501640709354db1cc4ffd42a?tpId=37&&tqId=21286&rp=1&ru=/ta/huawei&qru=/ta/huawei/question-ranking)

<!--more-->

### 输入描述:

```
输入一个string型基因序列，和int型子串的长度
```

### 输出描述:

```
找出GC比例最高的子串,如果有多个输出第一个的子串
```

示例1

### 输入

```
AACTGTGCACGACCTGA
5
```

### 输出

```
GCACG
```



### 思路

先统计从0开始的第一个子串中G、C的个数，然后利用滑动窗口统计以`left`为左边界的子串中G、C的个数，并维护最大个数和`left`左边界，最后的以`left`为左边界的窗口就是答案。



### 代码实现

```java
import java.util.*;
public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        while(sc.hasNext()){
            String str = sc.nextLine();
            int n = sc.nextInt();
            //统计第一个子串中GC个数
            int count = 0;
            for(int i = 0;i<n;i++){
                if(str.charAt(i)=='G'||str.charAt(i)=='C'){
                    count++;
                }
            }
            int max = count;
            int left = 0;
            for(int i = 1;i<str.length()-n;i++){
                if(str.charAt(i-1)=='G'||str.charAt(i-1)=='C'){
                    count--;
                }
                if(str.charAt(i+n-1)=='G'||str.charAt(i+n-1)=='C'){
                    count++;
                }
                if(count>max){
                    max = count;
                    left = i;
                }
            }
            System.out.println(str.substring(left,left+n));
        }
    }
}
```



