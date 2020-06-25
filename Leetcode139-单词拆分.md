---
title: Leetcode139.单词拆分
date: 2020-06-25 15:54:29
categories: Leetcode
tags:
  - 动态规划
---

## Leetcode139.单词拆分

给定一个非空字符串 s 和一个包含非空单词列表的字典 wordDict，判定 s 是否可以被空格拆分为一个或多个在字典中出现的单词。

说明：

拆分时可以重复使用字典中的单词。
你可以假设字典中没有重复的单词。

[参考链接](https://leetcode-cn.com/problems/word-break/)

<!--more-->

示例 1：

```
输入: s = "leetcode", wordDict = ["leet", "code"]
输出: true
解释: 返回 true 因为 "leetcode" 可以被拆分成 "leet code"。
```



示例 2：

```
输入: s = "applepenapple", wordDict = ["apple", "pen"]
输出: true
解释: 返回 true 因为 "applepenapple" 可以被拆分成 "apple pen apple"。
     注意你可以重复使用字典中的单词。
```



示例 3：

```
输入: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
输出: false
```



### 思路

令`dp[i]`表示前`i`个字符组成的字符串`s[0, i-1]`能否被空格拆分成若干个字典中出现的单词。外层循环`i`从1开始枚举前`i`个字符，内层循环`j`从0到`i-1`枚举分割点，若`s[0,j-1]`合法且`s[j, i-1]`合法，那么`s[0, i-1]`也合法。最后，`dp[len]`即为结果。



### 代码实现

```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        int len = s.length();
        //判断剩下字符是否存在于集合中时，可以使用HashSet提高效率
        Set<String> set = new HashSet<>(wordDict);
        //dp[i]表示前i个字符是否合法
        boolean[] dp = new boolean[len + 1];
        //初始化
        dp[0] = true;
        for (int i = 1; i <= len; i++) {
            //j是分割点
            for (int j = 0; j < i; j++) {
                //如果dp[j]合法且s[j,i-1]出现在字典中时，合法
                if (dp[j] && set.contains(s.substring(j, i))) {
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[len];
    }
}
```



