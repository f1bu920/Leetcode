---
title: Leetcode136.只出现一次的数字
date: 2020-05-14 09:17:10
categories: Leetcode
tags:
  - 哈希表
  - 位运算
---

## Leetcode136.只出现一次的数字

给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。

说明：

你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？

[题目链接](https://leetcode-cn.com/problems/single-number)

<!--more-->

示例 1:

输入: [2,2,1]
输出: 1
示例 2:

输入: [4,1,2,1,2]
输出: 4

#### 思路

- 哈希表

  使用集合存储数字，遍历数组中的每个数字，如果集合中没有该数字，则将该数字添加进集合；如果集合中有该数字，则将该数字从集合中删除。

- 位运算

  异或运算有3个性质：

  1. 任何数和0做异或结果都为其本身。
  2. 任何数和其本身做异或结果都为0。
  3. 异或运算满足交换律和结合律。

  因为数组中只有一个元素出现一次，其他元素都出现两次，所以将每个元素都做异或，结果就是只出现一次的数字。



#### 代码实现

- 哈希表

```java
class Solution {
    public int singleNumber(int[] nums) {
        Set<Integer> set = new HashSet<>(nums.length);
        for (int num : nums) {
            if (set.contains(num)) {
                set.remove(num);
            } else {
                set.add(num);
            }
        }
        return (int) set.toArray()[0];
    }
}
```

- 位运算

```java
class Solution {
    public int singleNumber(int[] nums) {
        int result = 0;
        for (int num : nums) {
            result ^= num;
        }
        return result;
    }
}
```



