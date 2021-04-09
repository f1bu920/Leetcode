---
title: Leetcode470.用Rand7()实现Rand10()
date: 2021-03-28 15:13:44
categories: Leetcode
tags:
  - 随机
---

## Leetcode470.用Rand7()实现Rand10()

已有方法 rand7 可生成 1 到 7 范围内的均匀随机整数，试写一个方法 rand10 生成 1 到 10 范围内的均匀随机整数。

不要使用系统的 Math.random() 方法。

 [题目链接](https://leetcode-cn.com/problems/implement-rand10-using-rand7)

<!--more-->

示例 1:

输入: 1
输出: [7]
示例 2:

输入: 2
输出: [8,4]
示例 3:

输入: 3
输出: [8,1,10]


提示:

rand7 已定义。
传入参数: n 表示 rand10 的调用次数。


进阶:

rand7()调用次数的 期望值 是多少 ?
你能否尽量少调用 rand7() ?



### 思路

**`(randX() - 1)*Y + randY()`可以等概率生成`[1, x*y]`的数据。**

所以`(rand7() - 1) * 7 + rand7()`会得到`[1, 49]`的数据，要获得rand10()数据，可以获得[1, 40]内的数据再和10取余。



### 代码实现

```java
class Solution extends SolBase {
    public int rand10() {
        int x = 11;
        int num = 49;
        while(num > 40){
            num = (rand7() - 1) * 7 + rand7();
            x = 1 + num % 10;
        }
        return x;
    }
}
```

