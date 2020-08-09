---
title: Leetcode93.复原IP地址
date: 2020-08-09 10:33:11
categories: Leetcode
tags:
  - 回溯
---

##  Leetcode93.复原IP地址

给定一个只包含数字的字符串，复原它并返回所有可能的 IP 地址格式。

有效的 IP 地址正好由四个整数（每个整数位于 0 到 255 之间组成），整数之间用 '.' 分隔。

 [题目链接](https://leetcode-cn.com/problems/restore-ip-addresses)

<!--more-->

示例:

```
输入: "25525511135"
输出: ["255.255.11.135", "255.255.111.35"]
```



### 思路

用递归地方式对所有可能的字符串进行搜索，令`dfs(segId,segStart)`表示从`s[segStart]`开始搜索第`segId`段，`segId = 0,1,2,3`。因为IP地址的每一段都是0到255的整数，所以每次枚举当前这一段的结束位置，如果满足要求就进行下一轮的搜索。

注意：因为IP地址不能用前导零，所以如果`s[segStart]=0`，那么第`segId`段就只能为0。当全部遍历完4段时，添加到结果中。



另一种简单的解法就是用`i,j,k`枚举三个小数点的位置。

### 代码实现

```java
class Solution {
    List<String> list = new ArrayList();
    int[] segments = new int[4];

    public List<String> restoreIpAddresses(String s) {
        dfs(s, 0, 0);
        return list;
    }

    private void dfs(String s, int segId, int segStart) {
        //找到了4段IP，并且遍历完字符串，得到一种答案
        if (segId == 4) {
            if (segStart == s.length()) {
                StringBuilder sb = new StringBuilder();
                for (int i = 0; i < 4; i++) {
                    sb.append(segments[i]);
                    if (i != 3) {
                        sb.append('.');
                    }
                }
                list.add(sb.toString());
            }
            return;
        }
        //未遍历完4段IP就已经遍历完字符串，剪枝
        if (segStart == s.length()) {
            return;
        }
        //如果有前导零，则这一段只能为0
        if (s.charAt(segStart) == '0') {
            segments[segId] = 0;
            dfs(s, segId + 1, segStart + 1);
        }
        //一般情况，枚举每一种可能性
        int address = 0;
        for (int i = segStart; i < s.length(); i++) {
            address = address * 10 + s.charAt(i) - '0';
            //注意这里不能等于0
            if (address > 0 && address <= 255) {
                segments[segId] = address;
                dfs(s, segId + 1, i + 1);
            } else {
                break;
            }
        }
    }
}
```

