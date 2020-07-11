---
title: Leetcode面试题17.13.恢复空格
date: 2020-07-11 09:35:33
categories: Leetcode
tags:
  - 动态规划
---

## Leetcode面试题17.13.恢复空格

哦，不！你不小心把一个长篇文章中的空格、标点都删掉了，并且大写也弄成了小写。像句子`"I reset the computer. It still didn’t boot!"`已经变成了`"iresetthecomputeritstilldidntboot"`。在处理标点符号和大小写之前，你得先把它断成词语。当然了，你有一本厚厚的词典`dictionary`，不过，有些词没在词典里。假设文章用`sentence`表示，设计一个算法，把文章断开，要求未识别的字符最少，返回未识别的字符数。

**注意：**本题相对原题稍作改动，只需返回未识别的字符数

 []()

<!--more-->

**示例：**

```
输入：
dictionary = ["looked","just","like","her","brother"]
sentence = "jesslookedjustliketimherbrother"
输出： 7
解释： 断句后为"jess looked just like tim her brother"，共7个未识别字符。
```

**提示：**

- `0 <= len(sentence) <= 1000`
- `dictionary`中总字符数不超过 150000。
- 你可以认为`dictionary`和`sentence`中只包含小写字母。



### 思路

令`dp[i]`表示前`i`个字符的未识别字符数。对于第`i`个字符，如果第`i`个字符未匹配，则`dp[i] = dp[i-1] +1 `；

遍历前`i`个字符，如果以某个下标`begin`开始，以第`i`个字符结尾的字符串正好在字典中，则`dp[i] = Math.min(dp[i],dp[begin])`。

最后的结果就是`dp[n]`，`n`为`sentence`长度。



### 代码实现

```java
public class Solution {
    public int respace(String[] dictionary, String sentence) {
        Set<String> set = new HashSet<>(Arrays.asList(dictionary));
        int n = sentence.length();
        int[] dp = new int[n + 1];
        dp[0] = 0;
        for (int i = 1; i <= n; i++) {
            dp[i] = dp[i - 1] + 1;
            for (int begin = 0; begin < i; begin++) {
                if (set.contains(sentence.substring(begin, i))) {
                    dp[i] = Math.min(dp[i], dp[begin]);
                }
            }
        }
        return dp[n];
    }
}
```

