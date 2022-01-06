---
title: Leetcode457.环形数组是否存在循环
date: 2021-08-07 11:43:22
categories: Leetcode
tags:
  - 双指针
---

## Leetcode457.环形数组是否存在循环

存在一个不含 0 的 环形 数组 nums ，每个 nums[i] 都表示位于下标 i 的角色应该向前或向后移动的下标个数：

如果 nums[i] 是正数，向前 移动 nums[i] 步
如果 nums[i] 是负数，向后 移动 nums[i] 步
因为数组是 环形 的，所以可以假设从最后一个元素向前移动一步会到达第一个元素，而第一个元素向后移动一步会到达最后一个元素。

数组中的 循环 由长度为 k 的下标序列 seq ：

遵循上述移动规则将导致重复下标序列 seq[0] -> seq[1] -> ... -> seq[k - 1] -> seq[0] -> ...
所有 nums[seq[j]] 应当不是 全正 就是 全负
k > 1
如果 nums 中存在循环，返回 true ；否则，返回 false 。

 [题目链接](https://leetcode-cn.com/problems/circular-array-loop)
<!--more-->

示例 1：

输入：nums = [2,-1,1,2,2]
输出：true
解释：存在循环，按下标 0 -> 2 -> 3 -> 0 。循环长度为 3 。
示例 2：

输入：nums = [-1,2]
输出：false
解释：按下标 1 -> 1 -> 1 ... 的运动无法构成循环，因为循环的长度为 1 。根据定义，循环的长度必须大于 1 。
示例 3:

输入：nums = [-2,1,-1,-2,-2]
输出：false
解释：按下标 1 -> 2 -> 1 -> ... 的运动无法构成循环，因为 nums[1] 是正数，而 nums[2] 是负数。
所有 nums[seq[j]] 应当不是全正就是全负。


提示：

- 1 <= nums.length <= 5000
- -1000 <= nums[i] <= 1000
- nums[i] != 0



### 思路

和环形链表的思路一样，利用快慢指针，慢指针一次跳一次，快指针一次跳两次，如果有循环则slow和fast一定可以相等。期间，检查当前单向边的方向是否与初始方向一致，如果不一致，直接停止遍历；为了降低时间复杂度可以标记每个节点是否访问过，如果下一个节点为已经访问过的节点则停止遍历。因为原数组中保证元素不为0，所以无需新建一个数组记录每个下标的访问情况，只需要将原数组对应的元素置0即可。

当nums[i]是n的整数倍时，i的后继节点是i本身，此时k=1，不符合要求。



### 代码实现

```java
class Solution {
    public boolean circularArrayLoop(int[] nums) {
        int n = nums.length;
        for (int i = 0; i < n; i++) {
            if (nums[i] == 0) {
                continue;
            }
            int slow = i;
            int fast = getNextIndex(nums, i);
            while (nums[slow] * nums[fast] > 0 && nums[slow] * nums[getNextIndex(nums, fast)] > 0) {
                if (slow == fast) {
                    if (slow != getNextIndex(nums, slow)) {
                        return true;
                    } else {
                        break;
                    }
                }
                slow = getNextIndex(nums, slow);
                fast = getNextIndex(nums, getNextIndex(nums, fast));
            }
            int index = i;
            while (nums[index] * nums[getNextIndex(nums, index)] > 0) {
                int temp = index;
                index = getNextIndex(nums, index);
                nums[temp] = 0;
            }
        }
        return false;
    }

    private int getNextIndex(int[] nums, int index) {
        int n = nums.length;
        return ((index + nums[index]) % n + n) % n;
    }
}
```



