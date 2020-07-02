---
title: nowcoder.合法IP
date: 2020-06-14 10:11:50
categories: nowcoder
tags:
  - String
---

## nowcoder.合法IP

### 题目描述

现在IPV4下用一个32位无符号整数来表示，一般用点分方式来显示，点将IP地址分成4个部分，每个部分为8位，表示成一个无符号整数（因此不需要用正号出现），如10.137.17.1，是我们非常熟悉的IP地址，一个IP地址串中没有空格出现（因为要表示成一个32数字）。

现在需要你用程序来判断IP是否合法。



### 输入描述:

```
输入一个ip地址
```

### 输出描述:

```
返回判断的结果YES or NO
```

示例1

### 输入

```
10.138.15.1
```

### 输出

```
YES
```



### 思路

由题意知，字符串以`.`为分隔，各个部分不能含有空格和负数，且每个部分为8位，则每个部分范围为0到255.



### 代码实现

```java
import java.io.*;
public class Main{
    public static void main(String[] args) throws IOException{
        BufferedReader bf = new BufferedReader(new InputStreamReader(System.in));
        String str = null;
        while ((str = bf.readLine()) != null) {
            boolean flag = true;
            String[] s = str.split("\\.");
            for (String value : s) {
                if (value.contains(" ")) {
                    System.out.println("NO");
                    flag = false;
                    break;
                }
                if (Integer.parseInt(value) >= 0 && Integer.parseInt(value) <= 255) {
                } else {
                    System.out.println("NO");
                    flag = false;
                    break;
                }
            }
            if (flag)
                System.out.println("YES");
        }
    }
}
```

