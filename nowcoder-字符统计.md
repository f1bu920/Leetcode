---
title: nowcoder.字符统计
date: 2020-06-12 09:05:15
categories: nowcoder
tags:
  - String
  - Array
---

## nowcoder.字符统计

### 题目描述

如果统计的个数相同，则按照ASCII码由小到大排序输出 。如果有其他字符，则对这些字符不用进行统计。

实现以下接口：
输入一个字符串，对字符中的各个英文字符，数字，空格进行统计（可反复调用）
按照统计个数由多到少输出统计结果，如果统计的个数相同，则按照ASII码由小到大排序输出
清空目前的统计结果，重新统计
调用者会保证：
输入的字符串以‘\0’结尾。

[链接](https://www.nowcoder.com/practice/c1f9561de1e240099bdb904765da9ad0?tpId=37&&tqId=21325&rp=1&ru=/activity/oj&qru=/ta/huawei/question-ranking)

<!--more-->



### 输入描述:

```
输入一串字符。
```

### 输出描述:

```
对字符中的
各个英文字符（大小写分开统计），数字，空格进行统计，并按照统计个数由多到少输出,如果统计的个数相同，则按照ASII码由小到大排序输出 。如果有其他字符，则对这些字符不用进行统计。
```

示例1

### 输入

```
aadddccddc
```

### 输出

```
dca
```



### 思路

创建一个数组`nums`存储字符出现的次数，`nums[i]`代表ASCII码为`i`的字符出现的次数。

遍历整个字符串，找到每个字符出现次数，记录某个字符出现最多的次数`max`。

再次遍历`nums`，将出现次数等于`max`的字符添加到结果中，将`max--`，循环此过程，直到`max=0`。



### 代码实现

```java
import java.util.*;
public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        while(sc.hasNext()){
            String str = sc.nextLine();
            System.out.println(CharacterCount(str));
        }
    }
    private static String CharacterCount(String str){
        char[] chars = str.toCharArray();
        int[] nums = new int[129];
        int max = 0;
        for(int i = 0;i<chars.length;i++){
            int index = (int) chars[i];
            nums[index]++;
            max = Math.max(max,nums[index]);
        }
        StringBuilder sb = new StringBuilder();
        while(max!=0){
            for(int i = 0;i<nums.length;i++){
                if(max==nums[i]){
                    sb.append((char)i);
                }
            }
            max--;
        }
        return sb.toString();
    }
}
```

