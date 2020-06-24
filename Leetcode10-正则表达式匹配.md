---
title: Leetcode10.正则表达式匹配
date: 2020-06-20 13:46:19
categories: Leetcode
tags:
  - 动态规划
---

## Leetcode10.正则表达式匹配

给你一个字符串 `s` 和一个字符规律 `p`，请你来实现一个支持 `'.'` 和 `'*'` 的正则表达式匹配。

'`.`' 匹配任意单个字符
'`*`' 匹配零个或多个前面的那一个元素
所谓匹配，是要涵盖 整个 字符串 s的，而不是部分字符串。

说明:

`s` 可能为空，且只包含从 a-z 的小写字母。
`p` 可能为空，且只包含从 a-z 的小写字母，以及字符 . 和 *。

[题目链接](https://leetcode-cn.com/problems/regular-expression-matching)

<!--more-->

示例 1:

```
输入:
s = "aa"
p = "a"
输出: false
解释: "a" 无法匹配 "aa" 整个字符串。
```



示例 2:

```
输入:
s = "aa"
p = "a*"
输出: true
解释: 因为 '*' 代表可以匹配零个或多个前面的那一个元素, 在这里前面的元素就是 'a'。因此，字符串 "aa" 可被视为 'a' 重复了一次。
```



示例 3:

```
输入:
s = "ab"
p = ".*"
输出: true
解释: ".*" 表示可匹配零个或多个（'*'）任意字符（'.'）。
```



示例 4:

```
输入:
s = "aab"
p = "c*a*b"
输出: true
解释: 因为 '*' 表示零个或多个，这里 'c' 为 0 个, 'a' 被重复一次。因此可以匹配字符串 "aab"。
```



示例 5:

```
输入:
s = "mississippi"
p = "mis*is*p*."
输出: false
```



### 思路

[参考链接](https://leetcode-cn.com/problems/regular-expression-matching/solution/dong-tai-gui-hua-zen-yao-cong-0kai-shi-si-kao-da-b/)

令`dp[i][j]`代表`s`的前`i`个字符能否被`p`的前`j`个字符匹配。

对于当前遍历的字符`s[i]`和`p[j]`，

1. 如果两者相等，则`dp[i][j] `=`dp[i-1][j-1]` ;
2. 如果`p[j]=='.'`，有`dp[i][j] = dp[i-1][j-1]`。
3. 如果`p[j]=='*'`，有：
   1. 如果`s[i] != p[j-1]`，则`dp[i][j] = d[i][j-2]`。
   2. 如果`s[i] == p[j-1]`或者`p[j-1]  == '.'`：有
      - 多个字符匹配的情况，`dp[i][j] = dp[i-1][j]`。
      - 单个字符匹配的情况，`dp[i][j] = dp[i][j-1]`。
      - 没有匹配的情况，`dp[i][j] = dp[i][j-2]`。

### 代码实现

```java
class Solution {
    public boolean isMatch(String s, String p) {
        if (s == null || p == null) {
            return false;
        }
        int m = s.length();
        int n = p.length();
        //dp[i][j]表示s的前i个能否被p的前j个匹配
        boolean[][] dp = new boolean[m + 1][n + 1];
        dp[0][0] = true;
        //这里初始化是防止s=""，p="a*b*c*d*"这种情况
        for (int i = 0; i < n; i++) {
            if (p.charAt(i) == '*' && dp[0][i - 1])
                dp[0][i + 1] = true;
        }
        //这里采用的加法形式
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (p.charAt(j) == '.' || p.charAt(j) == s.charAt(i)) {
                    dp[i + 1][j + 1] = dp[i][j];
                } else if (p.charAt(j) == '*') {
                    /*
                     dp[i][j] = dp[i-1][j] // 多个字符匹配的情况
                     or dp[i][j] = dp[i][j-1] // 单个字符匹配的情况
                     or dp[i][j] = dp[i][j-2] // 没有匹配的情况
                     */
                    //没有匹配
                    if (p.charAt(j - 1) != s.charAt(i) && p.charAt(j - 1) != '.') {
                        dp[i + 1][j + 1] = dp[i + 1][j - 1];
                    } else {
                        //dp[i+1][j+1] = dp[i+1][j]:单个字符匹配的情况
                        //dp[i+1][j+1] = dp[i+1][j]:没有字符的匹配情况
                        //dp[i+1][j+1] = dp[i][j+1]:多个字符匹配的情况
                        dp[i + 1][j + 1] = (dp[i + 1][j] || dp[i + 1][j - 1] || dp[i][j + 1]);
                    }
                }
            }
        }
        return dp[m][n];
    }
}
```



