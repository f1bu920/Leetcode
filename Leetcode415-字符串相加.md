---
title: Leetcode415.字符串相加
date: 2020-08-03 08:20:33
categories: Leetcode
tags:
  - String
---

## Leetcode415.字符串相加

给定两个字符串形式的非负整数 `num1` 和`num2` ，计算它们的和。

注意：

1. num1 和num2 的长度都小于 5100.
2. num1 和num2 都只包含数字 0-9.
3. num1 和num2 都不包含任何前导零。
4. 你不能使用任何內建 BigInteger 库， 也不能直接将输入的字符串转换为整数形式。

[题目连接](https://leetcode-cn.com/problems/add-strings)

<!--more-->



### 思路

模拟相加的过程，取两个字符串较长的那个，每次遍历相加，短的字符串不够时补0.



### 代码实现

```java
class Solution {
    public String addStrings(String num1, String num2) {
        StringBuilder sb = new StringBuilder();
        int i = num1.length() - 1;
        int j = num2.length() - 1;
        //进位
        int cnt = 0;
        while (i >= 0 || j >= 0) {
            int n1 = i >= 0 ? num1.charAt(i) - '0' : 0;
            int n2 = j >= 0 ? num2.charAt(j) - '0' : 0;
            int current = n1 + n2 + cnt;
            cnt = current >= 10 ? 1 : 0;
            sb.append(current % 10);
            i--;
            j--;
        }
        if (cnt == 1) {
            sb.append(1);
        }
        return sb.reverse().toString();
    }
}
```

