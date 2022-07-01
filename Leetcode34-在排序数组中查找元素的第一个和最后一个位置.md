---
title: Leetcode34.在排序数组中查找元素的第一个和最后一个位置
date: 2020-07-03 09:35:20
categories: Leetcode
tags:
  - 二分搜索
---

## Leetcode34.在排序数组中查找元素的第一个和最后一个位置

给定一个按照升序排列的整数数组 `nums`，和一个目标值 `target`。找出给定目标值在数组中的开始位置和结束位置。

你的算法时间复杂度必须是 O(log n) 级别。

如果数组中不存在目标值，返回 [-1, -1]。

[题目链接](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array)

<!--more-->

示例 1:

```
输入: nums = [5,7,7,8,8,10], target = 8
输出: [3,4]
```



示例 2:

```
输入: nums = [5,7,7,8,8,10], target = 6
输出: [-1,-1]
```

### 思路

使用二分查找法找到第一个`target`后，向前向后遍历找到其边界。



### 代码实现

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int[] result = {-1,-1};
        int left = 0;
        int right = nums.length-1;
        while(left<=right){
            int mid = left+(right-left)/2;
            if(nums[mid]<target){
                left = mid + 1;
            }else if(nums[mid]>target){
                right = mid - 1;
            }else{
                int i = mid-1;
                int j = mid+1;
                while(i>=0&&nums[i]==target){
                    i--;
                }
                while(j<nums.length&&nums[j]==target){
                    j++;
                }
                result[0] = i+1;
                result[1] = j-1;
                return result;
            }
        }
        return result;
    }
}
```

```java
class Solution {
    int[] nums;
    int n;
    int target;
    public int[] searchRange(int[] nums, int target) {
        int[] ans=new int[]{-1,-1};
        if(nums==null||nums.length==0)
            return ans;

        this.nums=nums;
        this.target=target;
        n=nums.length;

        ans[0]=findFirst();
        if(ans[0]==-1)
            return ans;
        ans[1]=findLast();
        return ans;
    }
    //寻找左边界
    private int findFirst(){
        int left=0,right=n-1;
        while(left<right){
            int mid=(left+right)/2;
            if(target==nums[mid])
                right=mid;
            else if(target<nums[mid])
                right=mid-1;
            else
                left=mid+1;
        }
        return nums[left]==target?left:-1;
    }
    //寻找右边界
    private int findLast(){
        int left=0,right=n-1;
        while(left<right){
            int mid=(left+right+1)/2;
            if(target==nums[mid])
                left=mid;
            else if(target<nums[mid])
                right=mid-1;
            else
                left=mid+1;
        }
        return nums[left]==target?left:-1;
        
    }
}
```

