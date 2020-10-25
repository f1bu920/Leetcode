---
title: Leetcode845.数组中的最长山脉
date: 2020-10-25 11:17:33
categories: Leetcode
tags:
  - 双指针
---

## Leetcode845.数组中的最长山脉

我们把数组 A 中符合下列属性的任意连续子数组 B 称为 “山脉”：

- B.length >= 3
- 存在 0 < i < B.length - 1 使得 B[0] < B[1] < ... B[i-1] < B[i] > B[i+1] > ... > B[B.length - 1]
  （注意：B 可以是 A 的任意子数组，包括整个数组 A。）

给出一个整数数组 `A`，返回最长 “山脉” 的长度。

如果不含有 “山脉” 则返回 0。

 [题目链接](https://leetcode-cn.com/problems/longest-mountain-in-array)

<!--more-->

示例 1：

```
输入：[2,1,4,7,3,2,5]
输出：5
解释：最长的 “山脉” 是 [1,4,7,3,2]，长度为 5。
```



示例 2：

```
输入：[2,2,2]
输出：0
解释：不含 “山脉”。
```




提示：

- 0 <= A.length <= 10000
- 0 <= A[i] <= 10000



### 思路

从左到右枚举山脚，使用双指针`left`枚举左山脚，`right`枚举右山脚，每次固定`left`；

- 因为山脉子数组最小长度为3，所以`left+2<n`;
- 因为山脉数组先增后减，所以开始时`A[left] < A[left+1]`；
- 将`right`初始化为`left + 1`，不断向右移动`right`，直到不满足`A[right] < A[right + 1]`为止
  - 此时，如果`right`等于`n-1`，表示到达数组尾部了，不可能形成山脉
  - 否则，`right`此时可能指向的是山顶，需要额外判断是否满足`A[right] > A[right+1]`
- 如果是山顶，就继续向右移动`right`，直到不满足`A[right] > A[right + 1]`为止，更新最长山脉长度。
- 当前山脉的右侧山脚可能是下一个山脉的左侧山脚，所以将`right`赋给`left`。



### 代码实现

```java
class Solution {
    public int longestMountain(int[] A) {
        if(A==null||A.length<3){
            return 0;
        }
        int n = A.length;
        int left = 0;
        int right = 0;
        int longest = 0;
        //左侧山脚需要满足left + 2 < n
        while(left + 2 < n){
            right = left + 1;
            //需要满足A[left] < A[left + 1]
            if(A[left] < A[left + 1]){
                //向右移动right找到山顶
                while(right < n - 1 && A[right] < A[right + 1]){
                    right++;
                }
                //判断是否是山顶，可能出现A[right] == A[right+1]，此时就不是山顶
                if(right < n - 1 && A[right] > A[right + 1]){
                    //是山顶的话，向右移动right找到右侧山脚
                    while(right < n - 1 && A[right] > A[right + 1]){
                        right++;
                    }
                    //更新最长山脉数组长度
                    longest = Math.max(longest, right - left + 1);
                }else{
                    //如果不是山顶，当前right指向的值不可能作为下一个山脉数组的左侧山脚
                    right++;
                }
            }
            //当前的右侧山脚可能是下一个山脉的左侧山脚，将right赋给left
            left = right;
        }
        return longest;
    }
}
```

