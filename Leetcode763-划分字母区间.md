---
title: Leetcode763.划分字母区间
date: 2020-10-22 09:23:58
categories: Leetcode
tags:
  - 双指针
  - 贪心
---

## Leetcode763.划分字母区间

字符串 S 由小写字母组成。我们要把这个字符串划分为尽可能多的片段，同一个字母只会出现在其中的一个片段。返回一个表示每个字符串片段的长度的列表。

 [题目链接](https://leetcode-cn.com/problems/partition-labels)

<!--more-->

示例 1：

```
输入：S = "ababcbacadefegdehijhklij"
输出：[9,7,8]
解释：
划分结果为 "ababcbaca", "defegde", "hijhklij"。
每个字母最多出现在一个片段中。
像 "ababcbacadefegde", "hijhklij" 的划分是错误的，因为划分的片段数较少。
```




提示：

- S的长度在[1, 500]之间。
- S只包含小写字母 'a' 到 'z' 。



### 思路

第一次遍历字符串，使用`lastIndex`数组记录每个字符出现的最后一个下标。

使用双指针`start`和`end`记录当前片段的起始下标和终止下标，初始时两个指针都初始化为0。从头遍历字符串，令`end = max(end,lastIndex[ch[i]-'a'])`。当`i`等于`end`时，当前访问段结束。



### 代码实现

```java
class Solution {
    public List<Integer> partitionLabels(String S) {
        List<Integer> result = new ArrayList();
        char[] ch = S.toCharArray();
        int[] lastIndex = new int[26];
        //记录每个字符出现的最后一个下标
        for(int i = 0;i<ch.length;i++){
            lastIndex[ch[i]-'a'] = i;
        }
        int start = 0;
        int end = 0;
        for(int i = 0;i<ch.length;i++){
            //更新end
            end = Math.max(end,lastIndex[ch[i]-'a']);
            //找到了一个区间
            if(i==end){
                result.add(end-start+1);
                start = end+1;
            }
        }
        return result;
    }
}
```

