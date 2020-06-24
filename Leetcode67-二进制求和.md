---
title: Leetcode67.二进制求和
date: 2020-06-23 09:56:16
categories: Leetcode
tags:
  - 栈
  - String
---

## Leetcode67.二进制求和

给你两个二进制字符串，返回它们的和（用二进制表示）。

输入为 非空 字符串且只包含数字 1 和 0。

 [题目链接](https://leetcode-cn.com/problems/add-binary)

<!--more-->

示例 1:

```
输入: a = "11", b = "1"
输出: "100"
```



示例 2:

```
输入: a = "1010", b = "1011"
输出: "10101"
```




提示：

```
每个字符串仅由字符 '0' 或 '1' 组成。
1 <= a.length, b.length <= 10^4
字符串如果不是 "0" ，就都不含前导零。
```

### 思路

创建两个栈`stack1`和`stack2`，分别将字符串`a`和`b`的字符入栈，设置进位标志`r`。当两个栈出栈元素加上`r`大于等于2时，说明有进位，`r`置为1；否则`r`置为0. 最后将当前结果添加到`StringBuilder`中。

当两个栈有一个为空时，每次将进位`r`与出栈元素进行判断，重复上述过程。

最后将得到的`StringBuilder`逆序即为结果。



### 代码实现

```java
class Solution {
    public String addBinary(String a, String b) {
        LinkedList<Character> stack1 = new LinkedList<>();
        LinkedList<Character> stack2 = new LinkedList<>();
        char[] charA = a.toCharArray();
        char[] charB = b.toCharArray();
        //入栈
        for (char c : charA) {
            stack1.push(c);
        }
        for (char c : charB) {
            stack2.push(c);
        }
        StringBuilder sb = new StringBuilder();
        //进位
        int r = 0;
        //出栈
        while (!stack1.isEmpty() && !stack2.isEmpty()) {
            int x = stack1.pop() - '0';
            int y = stack2.pop() - '0';
            int temp = x + y + r;
            if (temp >= 2) {
                r = 1;
            } else {
                r = 0;
            }
            sb.append((char) (temp % 2 + '0'));
        }
        while (!stack1.isEmpty()) {
            int t = stack1.pop() - '0';
            int temp = t + r;
            if (temp >= 2) {
                r = 1;
            } else {
                r = 0;
            }
            sb.append((char) (temp % 2 + '0'));
        }
        while (!stack2.isEmpty()) {
            int t = stack2.pop() - '0';
            int temp = t + r;
            if (temp >= 2) {
                r = 1;
            } else {
                r = 0;
            }
            sb.append((char) (temp % 2 + '0'));
        }
        //最后如果还有一个进位则添加到结果中
        if (r == 1) {
            sb.append('1');
        }
        return sb.reverse().toString();
    }
}
```



