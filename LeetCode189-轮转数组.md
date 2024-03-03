---
title: Leetcode189.轮转数组
date: 2024-03-03 16:39:42
categories: Leetcode
tags:
  - 数组
---

## Leetcode189.轮转数组

给定一个整数数组 `nums`，将数组中的元素向右轮转 `k` 个位置，其中 `k` 是非负数。

 

**示例 1:**

```
输入: nums = [1,2,3,4,5,6,7], k = 3
输出: [5,6,7,1,2,3,4]
解释:
向右轮转 1 步: [7,1,2,3,4,5,6]
向右轮转 2 步: [6,7,1,2,3,4,5]
向右轮转 3 步: [5,6,7,1,2,3,4]
```

**示例 2:**

```
输入：nums = [-1,-100,3,99], k = 2
输出：[3,99,-1,-100]
解释: 
向右轮转 1 步: [99,-1,-100,3]
向右轮转 2 步: [3,99,-1,-100]
```

 

**提示：**

- `1 <= nums.length <= 105`
- `-231 <= nums[i] <= 231 - 1`
- `0 <= k <= 105`

 

**进阶：**

- 尽可能想出更多的解决方案，至少有 **三种** 不同的方法可以解决这个问题。
- 你可以使用空间复杂度为 `O(1)` 的 **原地** 算法解决这个问题吗？



[题目链接](https://leetcode.cn/problems/rotate-array/solutions/551039/xuan-zhuan-shu-zu-by-leetcode-solution-nipk/)

### 思路

#### 额外数组

采用额外空间，遍历原数组，将原数组下标为 `i` 的元素放至新数组下标为` (i+k) mod n `的位置，最后将新数组拷贝至原数组即可。

时间复杂度O(n)，空间复杂度O(n)

#### 反转数组

先将原数组反转，再分别将区间`[0, k-1]`和`[k,n-1]`内的元素反转，即可得到结果

我们以 n=7，k=3 为例进行如下展示：

| 操作           | 结果          |
| -------------- | ------------- |
| 原始数组       | 1 2 3 4 5 6 7 |
| 全部反转       | 7 6 5 4 3 2 1 |
| 反转`[0, k-1]` | 5 6 7 4 3 2 1 |
| 反转`[k,n-1]`  | 5 6 7 1 2 3 4 |



### 代码实现

- 法一：额外数组

```
func rotate(nums []int, k int) {
    newNums := make([]int, len(nums))
    for i, v := range nums {
        newNums[(i+k)%len(nums)] = v
    }
    copy(nums, newNums)
}
```



- 法二：原地反转

```
func reverse(a []int) {
    for i, n := 0, len(a); i < n/2; i++ {
        a[i], a[n-1-i] = a[n-1-i], a[i]
    }
}

func rotate(nums []int, k int) {
    k %= len(nums)
    reverse(nums)
    reverse(nums[:k])
    reverse(nums[k:])
}
```

