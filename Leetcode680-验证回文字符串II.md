---
title: Leetcode680.验证回文字符串II
date: 2020-05-19 09:44:56
categories: Leetcode
tags:
  - String
  - 双指针
---

## Leetcode680.验证回文字符串II

给定一个非空字符串 s，最多删除一个字符。判断是否能成为回文字符串。

[题目链接](https://leetcode-cn.com/problems/valid-palindrome-ii)

<!--more-->

示例 1:

输入: "aba"
输出: True
示例 2:

输入: "abca"
输出: True
解释: 你可以删除c字符。
注意:

字符串只包含从 a-z 的小写字母。字符串的最大长度是50000。

## 思路

令`l`和`r`分别指向字符串的两端，如果`l`和`r`指向的字符相等，则左右指针向中间移动，直到左右指针相遇，代表是回文串。

当遇到不相等的情况时，分两种情况：`l`向右移动一位或者`r`向左移动一位，移动一位就代表删去一位字符。当两种情况至少有一个是回文串时，返回`true`。



#### 代码实现

```java
public boolean validPalindrome(String s) {
        int l = 0;
        int r = s.length() - 1;
        while (l < r) {
            if (s.charAt(l) == s.charAt(r)) {
                l++;
                r--;
            } else {
                boolean flagL = true;
                boolean flagR = true;
                //l向右移动一位
                for (int i = l + 1, j = r; i < j; i++, j--) {
                    if (s.charAt(i) != s.charAt(j)) {
                        flagL = false;
                        break;
                    }
                }
                //r向左移动一位
                for (int i = l, j = r - 1; i < j; i++, j--) {
                    if (s.charAt(i) != s.charAt(j)) {
                        flagR = false;
                        break;
                    }
                }
                return flagL || flagR;
            }
        }
        return true;
    }
}
```

