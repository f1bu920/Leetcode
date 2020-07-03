---
title: Leetcode32.最长有效括号
date: 2020-07-03 10:33:38
categories: Leetcode
tags:
  - 动态规划
---

## Leetcode32.最长有效括号

给定一个只包含 '(' 和 ')' 的字符串，找出最长的包含有效括号的子串的长度。

[题目链接](https://leetcode-cn.com/problems/longest-valid-parentheses)

<!--more-->

示例 1:

```
输入: "(()"
输出: 2
解释: 最长有效括号子串为 "()"
```



示例 2:

```
输入: ")()())"
输出: 4
解释: 最长有效括号子串为 "()()"
```



### 思路

令`dp[i]`代表以`i`为索引的字符结尾的最长有效括号的长度。当`s[i]==)`时：

1. `s[i-1]==(`，`dp[i] = dp[i-2]+2`。
2. `s[i-1]==)`，即形如`...())`，如果`s[i-dp[i-1]-1]==(`，其中`dp[i-1]`是以下标为`i-1`字符结尾的字串长度，因此`i-dp[i-1]-1`即为与当前右括号对应的括号的下标，如果这个括号为左括号，则当前遍历到的右括号是有小括号中的一部分，举例：`()(())`。
3. 因为以`(`结尾的字串一定非法，所以默认`dp[i]=0`。



### 代码实现

```java
class Solution {
    public int longestValidParentheses(String s) {
        int maxLen = 0;
        char[] chars = s.toCharArray();
        int[] dp = new int[chars.length];
        for(int i = 1;i<chars.length;i++){
            if(chars[i]==')'){
                //...()形式
                if(chars[i-1]=='('){
                    dp[i] = i>=2?dp[i-2]+2:2;
                    //...))形式
                    //i-dp[i-1]-1代表与当前右括号相匹配的位置，如果这个位置为(
                }else if((i-dp[i-1]-1)>=0&&chars[i-dp[i-1]-1]=='('){
                    //举例：()(())，i-dp[i-1]-2就是第一个右括号
                    dp[i] = dp[i-1]+(i-dp[i-1]-2>=0?dp[i-dp[i-1]-2]:0)+2;
                }
            }
            maxLen = Math.max(maxLen, dp[i]);
        }
        return maxLen;
    }
}
```

