---
title: Leetcode925.长按键入
date: 2020-10-21 09:58:26
categories: Leetcode
tags:
  - 双指针
  - 字符串
---

## Leetcode925.长按键入

你的朋友正在使用键盘输入他的名字 `name`。偶尔，在键入字符 c 时，按键可能会被长按，而字符可能被输入 1 次或多次。

你将会检查键盘输入的字符 `typed`。如果它对应的可能是你的朋友的名字（其中一些字符可能被长按），那么就返回 `True`。

 [题目链接](https://leetcode-cn.com/problems/long-pressed-name)

<!--more-->

示例 1：

```
输入：name = "alex", typed = "aaleex"
输出：true
解释：'alex' 中的 'a' 和 'e' 被长按。
```



示例 2：

```
输入：name = "saeed", typed = "ssaaedd"
输出：false
解释：'e' 一定需要被键入两次，但在 typed 的输出中不是这样。
```



示例 3：

```
输入：name = "leelee", typed = "lleeelee"
输出：true
```



示例 4：

```
输入：name = "laiden", typed = "laiden"
输出：true
解释：长按名字中的字符并不是必要的。
```




提示：

- name.length <= 1000
- typed.length <= 1000
- name 和 typed 的字符都是小写字母。



### 思路

利用双指针`index1`指向`name`，`index2`指向`typed`，每次将`index1`和`index2`移动到下一个不同的元素，判断移动的距离，若`index1`移动的距离大则直接返回`false`。

当有一个指针跑完后，最后结果判断是否都跑完。



### 代码实现

```java
class Solution {
    public boolean isLongPressedName(String name, String typed) {
        int index1 = 0;
        int index2 = 0;
        int n = name.length();
        int len = typed.length();
        if(n>len){
            return false;
        }
        if(n==len){
            return name.equals(typed);
        }
        while(index1<n&&index2<len){
            //值不相等直接返回false
            if(name.charAt(index1)!=typed.charAt(index2)){
                return false;
            }
            int i = index1+1;
            char c = name.charAt(index1);
            //移动到下一个不同的元素
            while(i<n&&name.charAt(i)==c){
                i++;
            }
            int j = index2+1;
            char t = typed.charAt(index2);
            //移动到下一个不同的元素
            while(j<typed.length()&&typed.charAt(j)==t){
                j++;
            }
            //如果index1移动的距离大于index2移动的距离，直接返回false
            if(i-index1>j-index2){
                return false;
            }
            index1 = i;
            index2 = j;
        }
        //最后判断是否还有剩余，如果有说明还有字符没被遍历到，返回false
        return (index1<n||index2<len) ? false : true;
    }
}
```

