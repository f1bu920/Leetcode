---
title: Leetcode41.缺失的第一个正数
date: 2020-06-27 08:55:11
categories: Leetcode
tags:
  - 哈希表
  - Array
---

## Leetcode41.缺失的第一个正数

给你一个未排序的整数数组，请你找出其中没有出现的最小的正整数。

 [题目链接](https://leetcode-cn.com/problems/first-missing-positive)

<!--more-->

示例 1:

```
输入: [1,2,0]
输出: 3
```



示例 2:

```
输入: [3,4,-1,1]
输出: 2
```



示例 3:

```
输入: [7,8,9,11,12]
输出: 1
```




提示：

你的算法的时间复杂度应为O(n)，并且只能使用常数级别的额外空间。



### 思路

因为缺失的第一个正数一定在`[1, n+1]`之间，`n`为数组长度，所以可以利用哈希表存储。当哈希表中不存在`i`时，即找到了最小缺失正数。但此方法不满足空间复杂度为常数级的要求。

同理，可以先将数组排序再用二分查找，但同样不满足时间复杂度为`O(n)`的要求。

因为要找的数一定在`[1, n+1]`之间，可以将数组看成哈希表来原地哈希。哈希的规则就是将数值为`i`的数映射到下标为`i-1`的地方。



### 代码实现

```java
class Solution {
    public int firstMissingPositive(int[] nums) {
        int len = nums.length;
        for (int i = 0; i < len; i++) {
            //nums[nums[i] - 1] != nums[i]的意思就是下标为i-1的值不等于i，此时将num[i]交换到i-1处
            while (nums[i] >= 1 && nums[i] <= len && nums[nums[i] - 1] != nums[i]) {
                int index = nums[i] - 1;
                int temp = nums[i];
                nums[i] = nums[index];
                nums[index] = temp;
            }
        }
        //遍历数组，若i-1处的值不等于i，则返回i
        for (int i = 1; i <= len; i++) {
            if (nums[i - 1] != i) {
                return i;
            }
        }
        //否则返回n+1
        return len + 1;
    }
}
```

