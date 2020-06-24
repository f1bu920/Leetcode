---
title: Leetcode394.字符串解码
date: 2020-05-28 11:07:28
categories: Leetcode
tags:
  - 栈
  - 字符串
---

## Leetcode394.字符串解码

给定一个经过编码的字符串，返回它解码后的字符串。

编码规则为: `k[encoded_string]`，表示其中方括号内部的 `encoded_string` 正好重复 `k `次。注意 k 保证为正整数。

你可以认为输入字符串总是有效的；输入字符串中没有额外的空格，且输入的方括号总是符合格式要求的。

此外，你可以认为原始数据不包含数字，所有的数字只表示重复的次数 `k` ，例如不会出现像 `3a` 或 `2[4]` 的输入。

[题目链接](https://leetcode-cn.com/problems/decode-string)

<!--more-->

示例:

```
s = "3[a]2[bc]", 返回 "aaabcbc".
s = "3[a2[c]]", 返回 "accaccacc".
s = "2[abc]3[cd]ef", 返回 "abcabccdcdcdef".
```



#### 思路

因为可能出现括号嵌套的情况，如`3[a2[bc]]`，所以需要利用栈。先将`2[bc]`转化为`bcbc`再压入栈中，最后栈中元素就是最后的结果。

遍历字符串`s`，遇到数字、字母和`[`时入栈，遇到`]`时出栈。

出栈时利用`temp`储存被`pop()`出来的字符串直到栈顶元素是`[`，再抛出`[`。**注意，因为栈的缘故，`temp`中的元素是逆序的，如`2[bc]`，`temp`中存储的是`cb`，因此需要逆序。**

因为已知`[`前一定是数字，且数字个数可能不止一位，所以需要利用字符串来存储结果，如`100[Leetcode]`，最后同理，因为栈取元素是逆序的，结果也要`reverse`。

将`temp`重复`n`次，`n`为刚才得到的数字。再将结果压栈。

最终，栈中元素即为结果。

#### 代码实现

```java
class Solution {
    public String decodeString(String s) {
        //栈
        Stack<Character> stack = new Stack<Character>();
        StringBuilder sb = new StringBuilder();
        //遍历s
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            //如果是数字、字母或者[，入栈
            if (Character.isDigit(c) || c == '[' || Character.isLetter(c)) {
                stack.push(c);
                //如果是],出栈
            } else if (c == ']') {
                //记录[前的所有元素
                StringBuilder temp = new StringBuilder();
                while (stack.peek() != '[') {
                    char ch = stack.pop();
                    temp.append(ch);
                }
                //pop [
                stack.pop();
                //记录[前的数字,因为数字可能不止一位所以需要用字符串记录
                //因为栈取元素是逆序的，所以结果要逆序
                StringBuilder num = new StringBuilder();
                while (stack.size() > 0 && Character.isDigit(stack.peek())) {
                    num.append(stack.pop());
                }
                String reverse = temp.reverse().toString();
                temp = new StringBuilder();
                //字符串逆序repeat n次，n为[前数字
                temp.append(reverse.repeat(Math.max(0, Integer.parseInt(num.reverse().toString()))));
                //将得到的字符串压栈
                for (int j = 0; j < temp.length(); j++) {
                    stack.push(temp.charAt(j));
                }
            }
        }
        for (Character character : stack) {
            sb.append(character);
        }
        return sb.toString();
    }
}
```

