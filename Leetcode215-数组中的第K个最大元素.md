---
title: Leetcode215.数组中的第K个最大元素
date: 2020-06-29 09:48:54
categories: Leetcode
tags:
  - 堆
  - 分治
---

## Leetcode215.数组中的第K个最大元素

在未排序的数组中找到第 k 个最大的元素。请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。

[题目链接](https://leetcode-cn.com/problems/kth-largest-element-in-an-array)

<!--more-->

示例 1:

```
输入: [3,2,1,5,6,4] 和 k = 2
输出: 5
```



示例 2:

```
输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
输出: 4
```



说明:

你可以假设 k 总是有效的，且 1 ≤ k ≤ 数组的长度。



### 思路及其代码实现

1. 排序

   将数组升序排序，返回下标为`len-k`的元素。

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        Arrays.sort(nums);
        return nums[nums.length-k];
    }
}
```

2. 分治

   利用快速排序算法中的`partition`操作，定位到索引为`len-k`的元素。因为`partition`操作总是能排定一个元素，这样利用二分法就能缩小搜索范围。但要注意切分时要随机选取元素，我选择的是`left`元素，因为测试用例中包含特例所以耗时较高。

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        int left = 0;
        int right = nums.length - 1;
        int target = nums.length - k;
        while (true) {
            //找到切分后的下标
            int index = partition(nums, left, right);
            //进行二分法搜索
            if (index == target) {
                return nums[index];
            } else if (index < target) {
                left = index + 1;
            } else {
                right = index - 1;
            }
        }
    }
    //切分操作
    private int partition(int[] nums, int left, int right) {
        //防止出现一个元素的情况报数组下标越界异常
        if (left >= right) {
            return left;
        }
        //两个指针
        int i = left;
        int j = right + 1;
        //选择的基准元素
        int key = nums[left];
        while (true) {
            //从左往右找到第一个大于等于的元素
            while (nums[++i] < key) {
                if (i == right) {
                    break;
                }
            }
            //从右往左找到第一个小于等于的元素
            while (nums[--j] > key) {
                if (j == left) {
                    break;
                }
            }
            //两指针相遇
            if (i >= j) {
                break;
            }
            //交换
            int temp = nums[i];
            nums[i] = nums[j];
            nums[j] = temp;
        }
        //将相遇处元素与基准元素交换
        int temp = nums[left];
        nums[left] = nums[j];
        nums[j] = temp;
        return j;
    }
}
```

3. 堆(优先级队列)

   利用`PriorityQueue`来将元素进行排序，`poll`掉前`len-k-1`个元素，返回第`len-k`个元素。

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        int len = nums.length;
        //默认按照升序排列
        PriorityQueue<Integer> queue = new PriorityQueue<>(len, (a, b) -> a - b);
        for (int num : nums) {
            queue.add(num);
        }
        for (int i = 0; i < len - k; i++) {
            queue.poll();
        }
        return queue.peek();
    }
}
```

