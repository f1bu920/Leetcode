---
title: Leetcode605.种花问题
date: 2021-04-05 13:26:22
categories: Leetcode
tags:
  - 贪心
---

## Leetcode605.种花问题

假设有一个很长的花坛，一部分地块种植了花，另一部分却没有。可是，花不能种植在相邻的地块上，它们会争夺水源，两者都会死去。

给你一个整数数组  flowerbed 表示花坛，由若干 0 和 1 组成，其中 0 表示没种植花，1 表示种植了花。另有一个数 n ，能否在不打破种植规则的情况下种入 n 朵花？能则返回 true ，不能则返回 false。

 [题目链接](https://leetcode-cn.com/problems/can-place-flowers)

<!--more-->

示例 1：

输入：flowerbed = [1,0,0,0,1], n = 1
输出：true
示例 2：

输入：flowerbed = [1,0,0,0,1], n = 2
输出：false


提示：

- 1 <= flowerbed.length <= 2 * 104
- flowerbed[i] 为 0 或 1
- flowerbed 中不存在相邻的两朵花
- 0 <= n <= flowerbed.length

### 思路

假设花坛的下标为`i`和`j`处种了花，中间没有种花且`j - i >= 2`，则可以种植花的范围是`[i + 2, j - 2]`，共`p = j - i - 3`个位置。当`p`是奇数时，可以种`(p + 1) / 2`颗花，当`p`是偶数时，可以种`p / 2`颗花，但因为偶数时`p / 2`与`(p + 1) / 2`相等，所有可以认为能种`(j - i - 2) / 2`朵花。

遍历数组，使用`pre`指针指向上次遍历到1的位置，初始时指向-1，计算每两个区间内能种花的颗树并累加，最后如果大于等于n则返回true。



### 代码实现

```java
class Solution {
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        //i、j下标处种花时，可以种花的下标范围为[i+2，j-2]，共j-i-3处位置，最多可以种植 （j-i-2）/ 2颗花
        int count = 0;
        int pre = -1;
        int len = flowerbed.length;
        for (int i = 0; i < flowerbed.length; i++) {
            if (flowerbed[i] == 1) {
                if (pre < 0) {
                    if (i >= 2) {
                        count += i / 2;
                    }
                } else {
                    count += (i - pre - 2) / 2;
                }
                pre = i;
            }
        }
        //相当于种植区间为[0, len - 1], 种植区间为[x, y]时能种`(y - x + 2) / 2`颗花
        if (pre < 0) {
            count += (len + 1) / 2;
        } else {
            //相当于种植区间为[pre + 2, len - 1]
            count += (len - pre - 1) / 2;
        }
        return count >= n;
    }
}
```

