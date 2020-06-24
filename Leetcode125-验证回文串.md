---
title: Leetcode125.验证回文串
date: 2020-05-19 10:12:01
categories: Leetcode
tags:
  - String 
  - 双指针
---

## Leetcode125.验证回文串

给定一个字符串，验证它是否是回文串，只考虑字母和数字字符，可以忽略字母的大小写。

说明：本题中，我们将空字符串定义为有效的回文串。

[题目链接](https://leetcode-cn.com/problems/valid-palindrome)

<!--more-->

示例 1:

输入: "A man, a plan, a canal: Panama"
输出: true
示例 2:

输入: "race a car"
输出: false

#### 思路

令左右指针分别指向字符串的两端，越过非数字和非字母的字符，若左右指针指向的字符相等，则左右指针向中间移动，直到左右指针相遇。

#### 代码实现

```java
class Solution {
    public boolean isPalindrome(String s) {
        int l = 0;
        int r = s.length() - 1;
        while (l<r){
            char cl = s.charAt(l);
            char cr = s.charAt(r);
            if (!Character.isLetterOrDigit(cl)){
                l++;
                continue;
            }
            if (!Character.isLetterOrDigit(cr)){
                r--;
                continue;
            }
            if (Character.toLowerCase(s.charAt(l)) == Character.toLowerCase(s.charAt(r))){
                l++;
                r--;
            }else {
                return false;
            }
        }
        return true;
    }
}
```

