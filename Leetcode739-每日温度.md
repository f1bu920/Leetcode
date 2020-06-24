---
title: Leetcode739.每日温度
date: 2020-06-11 08:30:01
categories: Leetcode
tags:
  - stack
---

##  Leetcode739.每日温度

根据每日 气温 列表，请重新生成一个列表，对应位置的输出是需要再等待多久温度才会升高超过该日的天数。如果之后都不会升高，请在该位置用 0 来代替。

例如，给定一个列表 temperatures = [73, 74, 75, 71, 69, 72, 76, 73]，你的输出应该是 [1, 1, 4, 2, 1, 1, 0, 0]。

提示：气温 列表长度的范围是 [1, 30000]。每个气温的值的均为华氏度，都是在 [30, 100] 范围内的整数。

[链接](https://leetcode-cn.com/problems/daily-temperatures)

<!--more-->

#### 思路

利用单调栈存储元素的下标，当栈为空时，将当前元素下标压栈；当前元素比栈顶元素大时，出栈，计算当前元素下标与栈顶元素下标的距离，重复此过程，直到栈为空或者当前元素小于等于栈顶元素，最后将当前元素压栈。



#### 代码实现

```java
class Solution {
    public int[] dailyTemperatures(int[] T) {
        int len = T.length;
        int[] result = new int[len];
        Deque<Integer> stack = new LinkedList<>();
        for (int i = 0; i < len; i++) {
            if (stack.isEmpty()) {
                stack.push(i);
            } else {
                //当前元素大于栈顶元素时出栈
                while (!stack.isEmpty() && T[i] > T[stack.peek()]) {
                    int head = stack.pop();
                    result[head] = i - head;
                }
                //最后将当前元素压栈
                stack.push(i);
            }
        }
        return result;
    }
}
```

