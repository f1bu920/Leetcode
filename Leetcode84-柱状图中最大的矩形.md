---
title: Leetcode84.柱状图中最大的矩形
date: 2020-05-30 09:59:55
categories: Leetcode
tags:
  - 双指针
  - 栈
---

## Leetcode84.柱状图中最大的矩形

给定 n 个非负整数，用来表示柱状图中各个柱子的高度。每个柱子彼此相邻，且宽度为 1 。

求在该柱状图中，能够勾勒出来的矩形的最大面积。

 ![](https://f1bu920.github.io/images/Leetcode84.柱状图中的最大矩形1.png)

以上是柱状图的示例，其中每个柱子的宽度为 1，给定的高度为 [2,1,5,6,2,3]。

 

![](https://f1bu920.github.io/images/Leetcode84.柱状图中的最大矩形2.png)

图中阴影部分为所能勾勒出的最大矩形面积，其面积为 10 个单位。

 <!--more-->

[题目链接](https://leetcode-cn.com/problems/largest-rectangle-in-histogram)

相似题目：[接雨水]([https://f1bu920.github.io/2020/04/12/Leetcode42-%E6%8E%A5%E9%9B%A8%E6%B0%B4/](https://f1bu920.github.io/2020/04/12/Leetcode42-接雨水/))

示例:

```
输入: [2,1,5,6,2,3]
输出: 10
```



#### 思路

- 暴力法

  遍历数组，找到当前数组位置`i`的左右两侧比`heights[i]`小的位置`left`和·`right`。则当前矩形面积为`heights[i]*(right-left-1)`。

- 栈

[官方题解](https://leetcode-cn.com/problems/largest-rectangle-in-histogram/solution/zhu-zhuang-tu-zhong-zui-da-de-ju-xing-by-leetcode-/)

#### 代码实现

- 暴力法

```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        int result = 0;
        if (heights == null || heights.length == 0) {
            return 0;
        }
        int len = heights.length;
        for (int i = 0; i < len; i++) {
            int left = i;
            int right = i;
            //找到左侧比它小的位置
            while (left >= 0 && heights[left] >= heights[i]) {
                left--;
            }
            //找到右侧比它小的位置
            while (right < len && heights[right] >= heights[i]) {
                right++;
            }
            result = Math.max(result, heights[i] * (right - left - 1));
        }
        return result;
    }
}
```

- 单调栈

[官方题解](https://leetcode-cn.com/problems/largest-rectangle-in-histogram/solution/zhu-zhuang-tu-zhong-zui-da-de-ju-xing-by-leetcode-/)

```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        int n = heights.length;
        int[] left = new int[n];
        int[] right = new int[n];
        
        Stack<Integer> mono_stack = new Stack<Integer>();
        for (int i = 0; i < n; ++i) {
            while (!mono_stack.isEmpty() && heights[mono_stack.peek()] >= heights[i]) {
                mono_stack.pop();
            }
            left[i] = (mono_stack.isEmpty() ? -1 : mono_stack.peek());
            mono_stack.push(i);
        }

        mono_stack.clear();
        for (int i = n - 1; i >= 0; --i) {
            while (!mono_stack.isEmpty() && heights[mono_stack.peek()] >= heights[i]) {
                mono_stack.pop();
            }
            right[i] = (mono_stack.isEmpty() ? n : mono_stack.peek());
            mono_stack.push(i);
        }
        
        int ans = 0;
        for (int i = 0; i < n; ++i) {
            ans = Math.max(ans, (right[i] - left[i] - 1) * heights[i]);
        }
        return ans;
    }
}
```

