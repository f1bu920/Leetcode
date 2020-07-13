---
title: Leetcode350.两个数组的交集II
date: 2020-07-13 09:54:40
categories: Leetcode
tags:
  - 哈希表
  - 排序
---

## Leetcode350.两个数组的交集II

给定两个数组，编写一个函数来计算它们的交集。

[题目链接](https://leetcode-cn.com/problems/intersection-of-two-arrays-ii)

<!--more-->

示例 1:

```
输入: nums1 = [1,2,2,1], nums2 = [2,2]
输出: [2,2]
```



示例 2:

```
输入: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出: [4,9]
```



说明：

- 输出结果中每个元素出现的次数，应与元素在两个数组中出现的次数一致。

- 我们可以不考虑输出结果的顺序。

进阶:

如果给定的数组已经排好序呢？你将如何优化你的算法？
如果 nums1 的大小比 nums2 小很多，哪种方法更优？
如果 nums2 的元素存储在磁盘上，磁盘内存是有限的，并且你不能一次加载所有的元素到内存中，你该怎么办？



### 思路

利用哈希表存储数组中每个数字出现的次数，遍历另一个数组，如果当前元素出现在哈希表中且出现次数大于1，将当前元素添加到结果中，并将出现次数减一；若出现次数小于等于1，将当前元素添加到结果后从哈希表中删除这个元素。

第二个思路就是将两个数组排序，利用双指针移动直到一个数组遍历完成。



### 代码实现

```java
//哈希表代码
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        List<Integer> list = new ArrayList<>();
        Map<Integer, Integer> map1 = new HashMap<>();
        for (int value : nums1) {
            map1.put(value, map1.getOrDefault(value, 0) + 1);
        }
        for (int value : nums2) {
            if (map1.containsKey(value)) {
                list.add(value);
                int t = map1.get(value);
                if (t > 1) {
                    map1.put(value, t - 1);
                } else {
                    map1.remove(value);
                }
            }
        }
        int[] result = new int[list.size()];
        int index = 0;
        for (int value : list) {
            result[index++] = value;
        }
        return result;
    }
}
```



