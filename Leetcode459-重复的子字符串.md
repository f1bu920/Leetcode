---
title: Leetcode459.重复的子字符串
date: 2020-08-24 14:41:39
categories: Leetcode
tags:
  - String
---

## Leetcode459.重复的子字符串

给定一个非空的字符串，判断它是否可以由它的一个子串重复多次构成。给定的字符串只含有小写英文字母，并且长度不超过10000。

[题目链接](https://leetcode-cn.com/problems/repeated-substring-pattern)

<!--more-->

示例 1:

```java
输入: "abab"

输出: True
```

解释: 可由子字符串 "ab" 重复两次构成。
示例 2:

```
输入: "aba"

输出: False
```



示例 3:

```
输入: "abcabcabcabc"

输出: True
```



解释: 可由子字符串 "abc" 重复四次构成。 (或者子字符串 "abcabc" 重复两次构成。)



### 思路

枚举子字符串。因为子字符串的长度一定能被`s`的长度整除且一定是`s`的前缀，所以子字符串的长度，最多只能到`s`长度的一半。接着枚举`s`的第`j`的字符是否与第`j-i`个字符相等，其中`i`是子字符串的长度，`j`为当前遍历的位置。若出现不相等，退出循环；如果匹配成功，直接返回。



### 代码实现

```java
class Solution {
    public boolean repeatedSubstringPattern(String s) {
        int len = s.length();
        //i代表字串长度
        for (int i = 1; i * 2 <= len; i++) {
            if (len % i == 0) {
                //匹配成功的标志
                boolean flag = true;
                //枚举s能否由这i个子串组成
                for (int j = i; j < len; j++) {
                    if (s.charAt(j) != s.charAt(j - i)) {
                        flag = false;
                        break;
                    }
                }
                if (flag) {
                    return true;
                }
            }
        }
        return false;
    }
}
```

