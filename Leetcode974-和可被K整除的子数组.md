---
title: Leetcode974.和可被K整除的子数组
date: 2020-05-27 09:36:04
categories: Leetcode
tags:
  - 前缀和
  - 哈希表
---

## Leetcode974.和可被K整除的子数组

给定一个整数数组 A，返回其中元素之和可被 K 整除的（连续、非空）子数组的数目。

 [题目链接](https://leetcode-cn.com/problems/subarray-sums-divisible-by-k)

<!--more-->

示例：

```
输入：A = [4,5,0,-2,-3,1], K = 5
输出：7
解释：
有 7 个子数组满足其元素之和可被 K = 5 整除：
[4, 5, 0, -2, -3, 1], [5], [5, 0], [5, 0, -2, -3], [0], [0, -2, -3], [-2, -3]
```




提示：

```
1 <= A.length <= 30000
-10000 <= A[i] <= 10000
2 <= K <= 10000
```

#### 思路

- 前缀和

  看到子数组之和，就应该与前缀和有关，令`preSum[i]`代表从`A[0]`到`A[i-1]`之和，注意有一位下标偏移。

  枚举子数组的左右边界，若右边界值减去左边界值再取模等于0，则计数器++。

  时间复杂度为`O(n^2)`，超出时间限制。

- 哈希表

  因为判断和可被K整除的条件为`(preSum[j] - preSum[i])%K==0` ，等价于`preSum[j]%K == preSum[i]%K`。可以引入哈希表来存储：

  - key：**前缀和 mod K，数值作为key，因此键值为0到K-1**；
  - value：结果出现次数。

  遍历之前，预置边界情况，`map`中提前存入0:1.

  遍历数组每一项，下·求前缀和`sum`，求当前项的前缀和 mod K，存入`map`中：

  - 若之前没存过，则存入key: 1；
  - 若之前存过，对应值+1。

  边存边查看`map`，如果`map`中已存在`key`为当前前缀和 mod K，

  - 说明**存在之前的前缀和 mod K == 当前前缀和 mod K**；
  - 将之前出现过的前缀和 mod K次数累加给`result`。

  注意**要考虑前缀和为负数的情况，负数取模仍为负数，`(sum % K + K) % K`，如“-1, 2, 9”。**

#### 代码实现

- 前缀和

```java
class Solution {
    public int subarraysDivByK(int[] A, int K) {
        int result = 0;
        int[] preSum = new int[A.length + 1];
        preSum[0] = 0;
        for (int i = 0; i < A.length; i++) {
            preSum[i + 1] = A[i] + preSum[i];
        }
        for (int i = 0; i < A.length; i++) {
            for (int j = i; j < A.length; j++) {
                if ((preSum[j + 1] - preSum[i]) % K == 0) {
                    result++;
                }
            }
        }
        return result;
    }
}
```

超出时间限制。

- 哈希表

```java
class Solution {
    public int subarraysDivByK(int[] A, int K) {
        int result = 0;
        Map<Integer, Integer> map = new HashMap<>(A.length + 1);
        int sum = 0;
        //提前加入map[0] = 1，
        map.put(0, 1);
        for (int i = 0; i < A.length; i++) {
            sum += A[i];
            //预防前缀和为负数的情况
            int temp = (sum % K + K) % K;
            //已经出现过，将之前出现的次数累加给result，并加一
            if (map.containsKey(temp)) {
                result += map.get(temp);
                map.put(temp, map.get(temp) + 1);
                //未出现过，添加key：1
            } else {
                map.put(temp, 1);
            }
        }
        return result;
    }
}
```

