---
title: Leetcode1300.转变数组后最接近目标值的数组和
date: 2020-06-14 09:04:20
categories: Leetcode
tags:
  - 枚举
  - 二分查找
---

## Leetcode1300.转变数组后最接近目标值的数组和

给你一个整数数组 `arr` 和一个目标值 `target` ，请你返回一个整数 `value` ，使得将数组中所有大于 `value` 的值变成 `value` 后，数组的和最接近  `target` （最接近表示两者之差的绝对值最小）。

如果有多种使得和最接近 `target` 的方案，请你返回这些整数中的最小值。

请注意，答案不一定是 `arr` 中的数字。

 [题目链接](https://leetcode-cn.com/problems/sum-of-mutated-array-closest-to-target)

<!--more-->

[官方题解](https://leetcode-cn.com/problems/sum-of-mutated-array-closest-to-target/solution/bian-shu-zu-hou-zui-jie-jin-mu-biao-zhi-de-shu-zu-/)

示例 1：

```
输入：arr = [4,9,3], target = 10
输出：3
解释：当选择 value 为 3 时，数组会变成 [3, 3, 3]，和为 9 ，这是最接近 target 的方案。
```



示例 2：

```
输入：arr = [2,3,5], target = 10
输出：5
```



示例 3：

```
输入：arr = [60864,25176,27249,21296,20204], target = 56803
输出：11361
```




提示：

- 1 <= arr.length <= 10^4
- 1 <= arr[i], target <= 10^5

#### 思路

将数组排序，分别确定枚举的上下界为0和`arr[len-1]`。进行二分搜索，找到大于等于枚举值的第一个下标，计算转换后的当前数组和`cur = arr[0] + arr[1] +...+ arr[i-1] +(len-i)*i `。进行比较并更新结果和最接近的数组和`distance`。

上面可以利用前缀和来计算数组和。



#### 代码实现

```java
class Solution {
    public int findBestValue(int[] arr, int target) {
        Arrays.sort(arr);
        int len = arr.length;
        int right = arr[len - 1];
        int[] preSum = new int[len + 1];
        int result = 0, distance = target;
        //前缀和
        for (int i = 1; i <= len; i++) {
            preSum[i] = arr[i - 1] + preSum[i - 1];
        }
        for (int i = 1; i <= right; i++) {
            int index = Arrays.binarySearch(arr, i);
            //如果没找到，binarySearch方法返回-(low+1)
            if (index < 0) {
                index = -index - 1;
            }
            //当前转换后的数组和
            int cur = preSum[index] + (len - index) * i;
            //更新
            if (Math.abs(cur - target) < distance) {
                result = i;
                distance = Math.abs(cur - target);
            }
        }
        return result;
    }
}
```





