---
title: Leetcode18.四数之和
date: 2020-10-05 12:47:12
categories: Leetcode
tags:
  - 双指针
  - 排序
---

## Leetcode18.四数之和

给定一个包含 n 个整数的数组 nums 和一个目标值 target，判断 nums 中是否存在四个元素 a，b，c 和 d ，使得 a + b + c + d 的值与 target 相等？找出所有满足条件且不重复的四元组。

注意：

答案中不可以包含重复的四元组。

[题目链接](https://leetcode-cn.com/problems/4sum)

<!--more-->

示例：

```
给定数组 nums = [1, 0, -1, 0, -2, 2]，和 target = 0。

满足要求的四元组集合为：
[
  [-1,  0, 0, 1],
  [-2, -1, 1, 2],
  [-2,  0, 0, 2]
]
```



### 思路

先将数组排序，因为四元组不能重复，所以**在同一重循环中，如果当前元素与上一个元素相同，则跳过当前元素。**此外，外层使用两层循环枚举前两个数，内层使用双指针`left`、`right`分别指向剩下区间的开头`j+1`和结尾`n-1`。

- 如果当前和等于`target`，将当前四个数添加到结果中，然后分别将左右指针右移、左移直到遇到不同的数；
- 如果当前和大于`target`，将右指针左移；
- 如果当前和小于`target`, 将左指针右移。

记得利用剪枝进行优化。



### 代码实现

```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        List<List<Integer>> result = new ArrayList();
        if(nums==null||nums.length<4){
            return result;
        }
        Arrays.sort(nums);
        int n = nums.length;
        for(int i = 0;i<n-3;i++){
            //进行剪枝、去重
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            if (nums[i] + nums[i + 1] + nums[i + 2] + nums[i + 3] > target) {
                break;
            }
            for(int j = i+1;j<n-2;j++){
                //进行剪枝、去重
                if (j > i + 1 && nums[j] == nums[j - 1]) {
                    continue;
                }
                if (nums[i] + nums[j] + nums[j + 1] + nums[j + 2] > target) {
                    break;
                }
                if (nums[i] + nums[j] + nums[n - 2] + nums[n - 1] < target) {
                    continue;
                }
                //双指针
                int left = j+1;
                int right = n-1;
                while(left<right){
                    int currentSum = nums[i]+nums[j]+nums[left]+nums[right];
                    if(currentSum==target){
                        result.add(Arrays.asList(nums[i],nums[j],nums[left],nums[right]));
                        //移动左右指针
                        while(left<right&&nums[left]==nums[left+1]){
                            left++;
                        }
                        left++;
                        while(left<right&&nums[right]==nums[right-1]){
                            right--;
                        }
                        right--;
                    }else if(currentSum>target){
                        right--;
                    }else{
                        left++;
                    }
                }
            }
        }
        return result;
    }
}
```



