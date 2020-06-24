---
title: Leetcode9.回文数
date: 2020-06-10 08:31:24
categories: Leetcode
tags:
  - String
---

## Leetcode9.回文数

判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

[题目连接](https://leetcode-cn.com/problems/palindrome-number)

<!--more-->

示例 1:

```
输入: 121
输出: true
```



示例 2:

```
输入: -121
输出: false
解释: 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。
```



示例 3:

```
输入: 10
输出: false
解释: 从右向左读, 为 01 。因此它不是一个回文数。
```



进阶:

你能不将整数转为字符串来解决这个问题吗？



#### 思路

最简单的方法是将数字转化为字符串，然后利用双指针前后移动进行判断。



#### 代码实现

```java
class Solution {
    public boolean isPalindrome(int x) {
        char[] chars = String.valueOf(x).toCharArray();
        int len = chars.length;
        for (int i = 0; i < len / 2; i++) {
            if (chars[i] != chars[len - 1 - i]) {
                return false;
            }
        }
        return true;
    }
}
```



