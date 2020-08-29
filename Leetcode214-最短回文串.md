---
title: Leetcode214.最短回文串
date: 2020-08-29 08:55:54
categories: Leetcode
tags:
  - String
---

## Leetcode214.最短回文串

给定一个字符串 s，你可以通过在字符串前面添加字符将其转换为回文串。找到并返回可以用这种方式转换的最短回文串。

[题目链接](https://leetcode-cn.com/problems/shortest-palindrome)

<!--more-->

示例 1:

```
输入: "aacecaaa"
输出: "aaacecaaa"
```



示例 2:

```
输入: "abcd"
输出: "dcbabcd"
```



### 思路

求最短回文串就是求从`s[0]`开始的最长回文子串，再将剩下的部分逆序拼接到`s`的开头。

求从头开始的最长回文子串，先将`s`逆序，再进行比较，如果字符串`s[0, n-i]`等于字符串`reverse[i,n]`，即代表找到了最长回文子串，退出循环。



### 代码实现

```java
class Solution {
    public String shortestPalindrome(String s) {
        int n = s.length();
        //逆序
        String reverse = new StringBuilder(s).reverse().toString();
        //记录i的值，i代表s减去从头开始的最长回文子串剩下的部分的开始下标
        int longestSubString = 0;
        for (int i = 0; i < n; i++) {
            if (s.substring(0, n - i).equals(reverse.substring(i, n))) {
                longestSubString = i;
                break;
            }
        }
        //将剩下部分逆序拼接到s的开头
        return new StringBuilder(s.substring(n - longestSubString, n)).reverse().toString() + s;
    }
}
```

