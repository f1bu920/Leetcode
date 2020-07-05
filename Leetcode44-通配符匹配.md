---
title: Leetcode44.通配符匹配
date: 2020-07-05 09:29:12
categories: Leetcode
tags:
  - 动态规划
---

## Leetcode44.通配符匹配

给定一个字符串 (s) 和一个字符模式 (p) ，实现一个支持 '?' 和 '*' 的通配符匹配。

'?' 可以匹配任何单个字符。
'*' 可以匹配任意字符串（包括空字符串）。
两个字符串完全匹配才算匹配成功。

说明:

`s` 可能为空，且只包含从 a-z 的小写字母。
`p` 可能为空，且只包含从 a-z 的小写字母，以及字符 ? 和 *。

[题目链接](https://leetcode-cn.com/problems/wildcard-matching)

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
p = "*"
输出: true
解释: '*' 可以匹配任意字符串。
```



示例 3:

```
输入:
s = "cb"
p = "?a"
输出: false
解释: '?' 可以匹配 'c', 但第二个 'a' 无法匹配 'b'。
```



示例 4:

```
输入:
s = "adceb"
p = "*a*b"
输出: true
解释: 第一个 '*' 可以匹配空字符串, 第二个 '*' 可以匹配字符串 "dce".
```



示例 5:

```
输入:
s = "acdcb"
p = "a*c?b"
输出: false
```



### 思路

与[Leetcode10.正则表达式匹配]([https://github.com/f1bu920/Leetcode/blob/master/Leetcode10-%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F%E5%8C%B9%E9%85%8D.md](https://github.com/f1bu920/Leetcode/blob/master/Leetcode10-正则表达式匹配.md))类似，令`dp[i][j]`表示字符串`s`的前`i`个字符与字符串`p`的前`j`个字符是否匹配。`s`的前`i`个字符的下标为`i-1`，`p`的前`j`字符的下标为`j-1`。

- 当`p[j-1]=='?'`或者`p[j-1]==s[j-1]`时，因为`?`能够匹配任意一个字符，所以`dp[i][j] = dp[i-1][j-1]`。
- 当`p[j-1] == '*'`时，`*`可以匹配零个或者多个任意小写字母，所以可以分为使用星号和不使用信号：
  1. 使用信号，则`dp[i][j] = dp[i-1][j]`。
  2. 不使用星号，则`dp[i][j] = dp[i][j-1]`。

最终结果就是`dp[m][n]`。

初始化：

- `dp[0][0] = true`，即两个字符串都为空时匹配成功。
- `dp[i][0] = false`，空模式无法匹配非空字符串。
- `dp[0][j]`：当模式字符串的前`j`个字符都为`*`，`dp[0][j]`才为`true`。

### 代码实现

```java
class Solution {
    public boolean isMatch(String s, String p) {
        int m = s.length();
        int n = p.length();
        boolean[][] dp = new boolean[m + 1][n + 1];
        dp[0][0] = true;
        //初始化
        for (int i = 1; i <= n; i++) {
            if (p.charAt(i - 1) == '*') {
                dp[0][i] = true;
            } else {
                break;
            }
        }
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (p.charAt(j - 1) == '?' || p.charAt(j - 1) == s.charAt(i - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else if (p.charAt(j - 1) == '*') {
                    dp[i][j] = dp[i][j - 1] || dp[i - 1][j];
                }
            }
        }
        return dp[m][n];
    }
}
```

