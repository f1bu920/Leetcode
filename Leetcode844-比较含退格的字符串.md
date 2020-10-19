---
title: Leetcode844.比较含退格的字符串
date: 2020-10-19 10:02:25
categories: Leetcode
tags:
  - 双指针
  - String
---

## Leetcode844.比较含退格的字符串

给定 S 和 T 两个字符串，当它们分别被输入到空白的文本编辑器后，判断二者是否相等，并返回结果。 # 代表退格字符。

注意：如果对空文本输入退格字符，文本继续为空。

 [题目链接](https://leetcode-cn.com/problems/backspace-string-compare)

<!--more-->

示例 1：

```
输入：S = "ab#c", T = "ad#c"
输出：true
解释：S 和 T 都会变成 “ac”。
```



示例 2：

```
输入：S = "ab##", T = "c#d#"
输出：true
解释：S 和 T 都会变成 “”。
```



示例 3：

```
输入：S = "a##c", T = "#a#c"
输出：true
解释：S 和 T 都会变成 “c”。
```



示例 4：

```
输入：S = "a#c", T = "b"
输出：false
解释：S 会变成 “c”，但 T 仍然是 “b”。
```




提示：

- 1 <= S.length <= 200
- 1 <= T.length <= 200
- S 和 T 只含有小写字母以及字符 '#'。


进阶：

你可以用 O(N) 的时间复杂度和 O(1) 的空间复杂度解决该问题吗？



### 思路

- 构造字符串

  利用`StringBuilder`重新构造出字符串，最后判断两个`StringBuilder`是否相等。

- 双指针

  从后往前遍历字符串，[官方题解](https://leetcode-cn.com/problems/backspace-string-compare/solution/bi-jiao-han-tui-ge-de-zi-fu-chuan-by-leetcode-solu/#comment)



### 代码实现

- 构造字符串

  ```java
  class Solution {
      public boolean backspaceCompare(String S, String T) {
          StringBuilder s = new StringBuilder();
          for (char c : S.toCharArray()) {
              if (c == '#') {
                  if (s.length() >= 1) {
                      s.deleteCharAt(s.length() - 1);
                  }
              } else {
                  s.append(c);
              }
          }
          StringBuilder t = new StringBuilder();
          for (char c : T.toCharArray()) {
              if (c == '#') {
                  if (t.length() >= 1) {
                      t.deleteCharAt(t.length() - 1);
                  }
              } else {
                  t.append(c);
              }
          }
          return s.compareTo(t) == 0;
      }
  }
  ```

  

