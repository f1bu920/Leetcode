---
title: Leetcode1071.字符串的最大公因子
date: 2020-03-12 16:16:25
categories: Leetcode
tags: 
  - String
  - Java
---

## Leetcode1071.字符串的最大公因子

对于字符串 S 和 T，只有在 S = T + ... + T（T 与自身连接 1 次或多次）时，我们才认定 “T 能除尽 S”。

返回最长字符串 X，要求满足 X 能除尽 str1 且 X 能除尽 str2。

[题目链接](https://leetcode-cn.com/problems/greatest-common-divisor-of-strings)

<!--more-->

示例 1：

> 输入：str1 = "ABCABC", str2 = "ABC"
>
> 输出："ABC"

示例 2：

> 输入：str1 = "ABABAB", str2 = "ABAB"
>
> 输出："AB"

示例 3：

> 输入：str1 = "LEET", str2 = "CODE"
>
> 输出：""


提示：

> 1 <= str1.length <= 1000
>
> 1 <= str2.length <= 1000
> str1[i] 和 str2[i] 为大写英文字母

---

- 方法一：枚举

从后往前遍历最大字串`[0,i]`，遇到符合条件的即为最大公因子串；

优化：如果存在公因子串，则`str1`是`m`个子串重复，`str2`是`n`个子串重复，因此`m+n`个子串和`n+m`个子串是一样的，即`(str1+str2).equals(str2+str1)`则代表有解。

```java
class Solution {
    public String gcdOfStrings(String str1, String str2) {
         if (!(str1+str2).equals(str2+str1)) return "";
        int len1 = str1.length();
        int len2 = str2.length();
        //最大公约数
        for (int i = Math.min(len1,len2);i>=1;i--){
            if (len1%i==0 && len2%i==0){
                //最大公约数对应子串
                String x = str1.substring(0,i);
                int lenx = x.length();
                //判断相加len/lenx次后是否与str1和str2相等
                int x1 = len1 / lenx;
                int x2 = len2 / lenx;
                String temp1 = "";
                String temp2 = "";
                while (x1>0){
                    temp1 = temp1+ x;
                    x1--;
                }
                while (x2>0){
                    temp2 +=x;
                    x2--;
                }
                //最大公因子只可能是最大公约数时取得，若相等则返回，否则为空
                if (temp1.equals(str1) &&temp2.equals(str2)){
                    return x;
                }
                else{
                    return "";
                }
            }
        }
        return "";
    }
}
```

---

- 方法二：辗转相除法

确定有解后，最大解即为`len1`和`len2`的最大公约数

```java
class Solution {
    public String gcdOfStrings(String str1, String str2) {
        if (!(str1+str2).equals(str2+str1)){
            return "";
        }
        return str1.substring(0,gcd(str1.length(),str2.length()));
    }
    // 求最大公约数
    public int gcd(int a, int b) {
        if (b == 0) {
            return a;
        }
        return gcd(b, a % b);
    }
}
```

