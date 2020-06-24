---
title: Leetcode76.最小覆盖子串
date: 2020-05-23 10:30:26
categories: Leetcode
tags:
  - Sliding Windows
  - 双指针
---

## Leetcode76.最小覆盖子串

给你一个字符串 S、一个字符串 T，请在字符串 S 里面找出：包含 T 所有字符的最小子串。

[题目链接](https://leetcode-cn.com/problems/minimum-window-substring)

<!--more-->

示例：

输入: S = "ADOBECODEBANC", T = "ABC"
输出: "BANC"
说明：

如果 S 中不存这样的子串，则返回空字符串 ""。
如果 S 中存在这样的子串，我们保证它是唯一的答案。

#### 思路

定义一个窗口的左右指针`left`和`right`。定义两个`HashMap`存储每个字母的出现次数，`mapT`存储字符串t中每个字母的出现次数，`map`存储遍历字符串`s`时的结果。、

在`s`上滑动窗口，将右指针向右移扩大窗口，遇到`mapT`中出现的字符时存入`map`中。当窗口包含t中全部字符时，尝试收缩左窗口，直到得到最小窗口。

#### 代码实现

```java
public class Solution {
    Map<Character, Integer> mapT;
    Map<Character, Integer> map;

    public String minWindow(String s, String t) {
        int sLen = s.length();
        int tLen = t.length();
        mapT = new HashMap<>(tLen);
        map = new HashMap<>(tLen);
        for (int i = 0; i < tLen; i++) {
            char c = t.charAt(i);
            mapT.put(c, mapT.getOrDefault(c, 0) + 1);
        }
        int left = 0;
        int right = 0;
        int start = -1;
        int end = -1;
        int minSize = Integer.MAX_VALUE;
        while (right < sLen) {
            char c = s.charAt(right);
            if (mapT.containsKey(c)) {
                map.put(c, map.getOrDefault(c, 0) + 1);
            }
            if (right - left + 1 < tLen) {
                right++;
                continue;
            }
            while (check() && left <= right) {
                if (right - left + 1 < minSize) {
                    start = left;
                    end = right;
                    minSize = right - left + 1;
                }
                char ch = s.charAt(left);
                if (map.containsKey(ch)) {
                    map.put(ch, map.get(ch) - 1);
                }
                left++;
            }
            right++;
        }
        return start == -1 ? "" : s.substring(start, end + 1);
    }

    private boolean check() {
        for (Map.Entry<Character, Integer> entry : mapT.entrySet()) {
            if (entry.getValue() > map.getOrDefault(entry.getKey(), 0)) {
                return false;
            }
        }
        return true;
    }
}
```

上述我自己的代码超出时间限制，(改了好久还是超时，贴以下官方的代码，个人感觉大同小异

```java
class Solution {
    Map<Character, Integer> ori = new HashMap<Character, Integer>();
    Map<Character, Integer> cnt = new HashMap<Character, Integer>();

    public String minWindow(String s, String t) {
        int tLen = t.length();
        for (int i = 0; i < tLen; i++) {
            char c = t.charAt(i);
            ori.put(c, ori.getOrDefault(c, 0) + 1);
        }
        int l = 0, r = -1;
        int len = Integer.MAX_VALUE, ansL = -1, ansR = -1;
        int sLen = s.length();
        while (r < sLen) {
            ++r;
            if (r < sLen && ori.containsKey(s.charAt(r))) {
                cnt.put(s.charAt(r), cnt.getOrDefault(s.charAt(r), 0) + 1);
            }
            while (check() && l <= r) {
                if (r - l + 1 < len) {
                    len = r - l + 1;
                    ansL = l;
                    ansR = l + len;
                }
                if (ori.containsKey(s.charAt(l))) {
                    cnt.put(s.charAt(l), cnt.getOrDefault(s.charAt(l), 0) - 1);
                }
                ++l;
            }
        }
        return ansL == -1 ? "" : s.substring(ansL, ansR);
    }

    public boolean check() {
        Iterator iter = ori.entrySet().iterator(); 
        while (iter.hasNext()) { 
            Map.Entry entry = (Map.Entry) iter.next(); 
            Character key = (Character) entry.getKey(); 
            Integer val = (Integer) entry.getValue(); 
            if (cnt.getOrDefault(key, 0) < val) {
                return false;
            }
        } 
        return true;
    }
}
```

更新：不会哈希表而采用数组存储每个字符出现次数：

```java
class Solution {
    public String minWindow(String s, String t) {
        int sLen = s.length();
        int tLen = t.length();
        //存储t中每个字符出现次数
        int[] needs = new int[128];
        //存储滑动窗口中每个字符出现次数
        int[] windows = new int[128];
        //存储窗口中字符出现次数
        int count = 0;
        int left = 0;
        int right = 0;
        int start = -1;
        int end = -1;
        int minSize = Integer.MAX_VALUE;
        //存储t中每个字符出现次数
        for (int i = 0; i < tLen; i++) {
            needs[t.charAt(i)]++;
        }
        while (right < sLen) {
            char c = s.charAt(right);
            windows[c]++;
            //needs[c] > 0：代表是t中出现的字符
            //needs[c] >= windows[c]：表示此时窗口中右边界字符出现次数小于等于t中该字符出现次数
            //所以需要count++
            if (needs[c] > 0 && needs[c] >= windows[c]) {
                count++;
            }
            //满足条件，尝试缩减左窗口
            while (count == tLen) {
                char ch = s.charAt(left);
                //记录当前最小字符串
                if (right - left + 1 < minSize) {
                    start = left;
                    end = right;
                    minSize = right - left + 1;
                }
                //needs[c] > 0：代表是t中出现的字符
                //needs[ch] == windows[ch]：代表此时左窗口字符恰好满足条件，左窗口右移后不满足
                if (needs[ch] > 0 && needs[ch] == windows[ch]) {
                    count--;
                }
                //左窗口右移，窗口中该字符个数减一
                windows[ch]--;
                left++;
            }
            right++;
        }
        return start == -1 ? "" : s.substring(start, end + 1);
    }

```

