---
title: Leetcode17.电话号码的字母组合
date: 2020-06-22 11:09:00
categories: Leetcode
tags:
  - 递归
  - String
---

## Leetcode17.电话号码的字母组合

给定一个仅包含数字 2-9 的字符串，返回所有它能表示的字母组合。

给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。

![](https://f1bu920.github.io/images/Leetcode17电话号码的字母组合.png)

[题目链接](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number)

<!--more-->

示例:

```
输入："23"
输出：["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

说明:
尽管上面的答案是按字典序排列的，但是你可以任意选择答案输出的顺序。



### 思路

![](https://f1bu920.github.io/images/Leetcode17思路.png)

使用`HashMap`存储数字对应的字符串组合，创建递归函数`private void combination(int index, String str, String digits)`，其中`index`是当前遍历到的`digits`中的字符下标，当`index==digits.length()`时，结束递归，并将`str`添加到结果中。



### 代码实现

```java
class Solution {
    List<String> list = new ArrayList<String>();
    Map<Character, String> map = new HashMap<>();


    public List<String> letterCombinations(String digits) {
        map.put('2', "abc");
        map.put('3', "def");
        map.put('4', "ghi");
        map.put('5', "jkl");
        map.put('6', "mno");
        map.put('7', "pqrs");
        map.put('8', "tuv");
        map.put('9', "wxyz");
        if (digits == null || digits.equals("")) {
            return list;
        }
        combination(0, "", digits);
        return list;
    }

    private void combination(int index, String str, String digits) {
        if (index == digits.length()) {
            list.add(str);
            return;
        }
        String letters = map.get(digits.charAt(index));
        for (int i = 0; i < letters.length(); i++) {
            combination(index + 1, str + letters.charAt(i), digits);
        }
    }
}
```

因为用了很多字符串拼接，也可以将`String str`换成`StringBuilder`。