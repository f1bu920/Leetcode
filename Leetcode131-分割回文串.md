---
title: Leetcode131.分割回文串
date: 2021-03-20 17:43:00
categories: Leetcode
tags:
  - 回溯
---

### Leetcode131.分割回文串

给你一个字符串 s，请你将 s 分割成一些子串，使每个子串都是 回文串 。返回 s 所有可能的分割方案。

回文串 是正着读和反着读都一样的字符串。

 [题目链接](https://leetcode-cn.com/problems/palindrome-partitioning/)

<!--more-->

示例 1：

输入：s = "aab"
输出：[["a","a","b"],["aa","b"]]
示例 2：

输入：s = "a"
输出：[["a"]]


提示：

- 1 <= s.length <= 16

- s 仅由小写英文字母组成



### 思路

采取回溯的思路，判断前缀字符串是否回文，如果是回文则继续dfs，如果不是回文则剪枝。

当遍历完成后就得到了一个结果集。

因为会用到很多子串，避免截取子串的消耗采用字符数组。



### 代码实现

```java
class Solution {
    List<List<String>> result = new ArrayList<>();

    public List<List<String>> partition(String s) {
        if (s == null || s.length() == 0) {
            return result;
        }
        int n = s.length();
        char[] ch = s.toCharArray();
        Deque<String> stack = new ArrayDeque<>();
        backTrace(ch, 0, n, stack);
        return result;
    }

    private void backTrace(char[] ch, int index, int n, Deque<String> path) {
        if (index == n) {
            result.add(new ArrayList<>(path));
            return;
        }
        for (int i = index; i < n; i++) {
            //不构成直接剪枝
            if (!isPalindrome(ch, index, i)) {
                continue;
            }
            path.addLast(new String(ch, index, i + 1 - index));
            backTrace(ch, i + 1, n, path);
            //回滚
            path.removeLast();
        }
    }
    //判断字符数组区间是否构成回文串
    private boolean isPalindrome(char[] ch, int left, int right) {
        while (left < right) {
            if (ch[left] != ch[right]) {
                return false;
            }
            left++;
            right--;
        }
        return true;
    }
}
```

