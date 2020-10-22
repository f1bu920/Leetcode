---
title: 剑指offer.二维数组中的查找
date: 2020-10-22 19:40:38
categories: 剑指offer
tags:
  - 剑指offer
  - 二分查找
---

## 剑指offer.二维数组中的查找

### 题目描述

在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。



### 思路

因为二维数组从左到右递增，从上到下递增，所以每次选取右上方或者左下方的元素与`target`进行比较就可以每次排除一行或者一列：

1. 如果选取元素等于`target`，直接返回`true`；
2. 如果大于`target`，排除这一列；
3. 如果小于`target`，排除这一行。



### 代码实现

```java
public class Solution {
    public boolean Find(int target, int [][] array) {
        int rows = array.length - 1;
        int col = array[0].length - 1;
        int row = 0;
        while(row <= rows && col >= 0){
            if(array[row][col]==target){
                return true;
            }else if(array[row][col] > target){
                col--;
            }else{
                row++;
            }
        }
        return false;
    }
}
```

