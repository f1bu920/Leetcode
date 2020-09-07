---
title: Leetcode347.前K个高频元素
date: 2020-09-07 08:59:55
categories: Leetcode
tags:
  - 堆
  - 哈希表
---

## Leetcode347.前K个高频元素

给定一个非空的整数数组，返回其中出现频率前 k 高的元素。

 [题目链接](https://leetcode-cn.com/problems/top-k-frequent-elements
)

<!--more-->

示例 1:

```
输入: nums = [1,1,1,2,2,3], k = 2
输出: [1,2]
```



示例 2:

```
输入: nums = [1], k = 1
输出: [1]
```




提示：

你可以假设给定的 k 总是合理的，且 1 ≤ k ≤ 数组中不相同的元素的个数。
你的算法的时间复杂度必须优于 O(n log n) , n 是数组的大小。
题目数据保证答案唯一，换句话说，数组中前 k 个高频元素的集合是唯一的。
你可以按任意顺序返回答案。



### 思路

利用哈希表存储数组元素的出现次数，再利用堆根据数组元素在哈希表中的出现次数进行降序排序。最后返回前K个元素即可。



### 代码实现

```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        int n = nums.length;
        Map<Integer, Integer> map = new HashMap(n);
        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
        PriorityQueue<Integer> heap = new PriorityQueue<>(n, (Integer i1, Integer i2) -> {
            return map.getOrDefault(i2, 0) - map.getOrDefault(i1, 0);
        });
        heap.addAll(map.keySet());
        int[] result = new int[k];
        for (int i = 0; i < k; i++) {
            result[i] = heap.remove();
        }
        return result;
    }
}
```

