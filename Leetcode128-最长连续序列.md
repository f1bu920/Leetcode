---
title: Leetcode128.最长连续序列
date: 2020-06-06 08:51:18
categories: Leetcode
tags:
  - Array
  - 哈希表
---

## Leetcode128.最长连续序列

给定一个未排序的整数数组，找出最长连续序列的长度。

要求算法的时间复杂度为 O(n)。

[题目链接](https://leetcode-cn.com/problems/longest-consecutive-sequence)

<!--more-->

示例:

```
输入: [100, 4, 200, 1, 3, 2]
输出: 4
解释: 最长连续序列是 [1, 2, 3, 4]。它的长度为 4。
```



#### 思路

暴力做法是枚举数组中每个元素`x`，考虑以其为起点，判断`x+1, x+2`等是否存在。不断枚举并更新答案。更高效的做法是利用哈希表，判断哈希表中是否存在这个数，但极端情况下的时间复杂度仍为`O(n^2)`。

对于一个序列`x, x+1, x+2, x+3...`，只需要枚举一次`x`即可，不需要再枚举`x+1`、`x+2`和之后的元素了，因此对于哈希表中当前元素`x`，需要判断是否存在`x-1`，若存在，则跳过，不存在则接着统计以其为起点的连续序列。



#### 代码实现

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        int longestSize = 0;
        Set<Integer> set = new HashSet<>();
        //将数组元素添加到集合中
        for (int num : nums) {
            set.add(num);
        }
        for (int num : set) {
            //遍历集合中元素x，若存在x-1，跳过；不存在则记录当前连续序列
            if (!set.contains(num - 1)) {
                //统计以x为起点的连续序列
                int currentSize = 1;
                int currentNum = num;
                while (set.contains(currentNum + 1)) {
                    currentNum += 1;
                    currentSize += 1;
                }
                longestSize = Math.max(longestSize, currentSize);
            }
        }
        return longestSize;
    }
}
```

