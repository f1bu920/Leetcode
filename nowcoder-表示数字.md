---
title: nowcoder.表示数字
date: 2020-06-13 09:49:31
categories: nowcoder
tags:
  - String
---

## nowcoder.表示数字

### 题目描述

将一个字符中所有出现的数字前后加上符号“*”，其他字符保持不变
public static String MarkNum(String pInStr)
{

return null;

}

注意：输入数据可能有多行

[链接](https://www.nowcoder.com/practice/637062df51674de8ba464e792d1a0ac6?tpId=37&&tqId=21319&rp=1&ru=/activity/oj&qru=/ta/huawei/question-ranking)

<!--more-->

### 输入描述:

```
输入一个字符串
```

### 输出描述:

```
字符中所有出现的数字前后加上符号“*”，其他字符保持不变
```

示例1

### 输入

```
Jkdi234klowe90a3
```

### 输出

```
Jkdi*234*klowe*90*a*3*
```



### 思路

利用`StringBuilder`减少创建`String`的内存消耗，遍历字符串，遇到数字添加进`StringBuilder`中，注意要利用`for`循环找到下一个不是数字的字符，并将遍历下标减一。



### 代码实现

```java
import java.io.*;
public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader bf = new BufferedReader(new InputStreamReader(System.in));
        String str = null;
        while ((str = bf.readLine()) != null) {
            System.out.println(MarkNum(str));
        }
    }

    public static String MarkNum(String pInStr) {
        char[] chars = pInStr.toCharArray();
        int len = chars.length;
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < len; i++) {
            if (Character.isDigit(chars[i])) {
                sb.append('*');
                sb.append(chars[i]);
                //这里i++是为了找到下一个不是数字的字符
                i++;
                while (i < len && Character.isDigit(chars[i])) {
                    sb.append(chars[i]);
                    i++;
                }
                //注意这里要i--,因为最后循环体中还会进行i++
                //如果不减一，就会跳过下一个不是数字的字符
                i--;
                sb.append('*');
            } else {
                sb.append(chars[i]);
            }
        }
        return sb.toString();
    }
}
```

