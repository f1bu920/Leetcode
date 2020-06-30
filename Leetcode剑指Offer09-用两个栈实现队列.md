---
title: Leetcode剑指Offer09.用两个栈实现队列
date: 2020-06-30 08:40:03
categories: Leetcode
tags:
  - 栈
  - 设计
---

## Leetcode剑指Offer09.用两个栈实现队列

用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 `appendTail` 和 `deleteHead` ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，`deleteHead` 操作返回 -1 )

 [题目链接](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof)

<!--more-->

示例 1：

```
输入：
["CQueue","appendTail","deleteHead","deleteHead"]
[[],[3],[],[]]
输出：[null,null,3,-1]
```



示例 2：

```
输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]
```



提示：

- 1 <= values <= 10000
- 最多会对 appendTail、deleteHead 进行 10000 次调用



### 思路

用两个栈，栈1进行插入操作，栈2进行删除操作。使用两个指针`point1`与`point2`分别指向两个栈的栈顶元素。

当删除元素时，若栈2为空则不断弹出栈1元素并压入栈2直到栈1为空，同时维护两个栈顶指针，这样就能实现队列先进先出的特性。



### 代码实现

```java
class CQueue {
    private int[] stack1;
    private int[] stack2;
    //两个指针初始时都为-1
    int point1 = -1;
    int point2 = -1;

    public CQueue() {
        stack1 = new int[10000];
        stack2 = new int[10000];
    }
    //栈1用于添加元素
    public void appendTail(int value) {
        stack1[++point1] = value;
    }
    //栈2用于删除元素
    public int deleteHead() {
        //栈2为空时将栈1中元素全部出栈并压入栈2
        if(point2==-1){
            while(point1>=0){
                stack2[++point2] = stack1[point1--];
            }
        }
        //若栈2仍然为空，则代表没有元素
        if(point2==-1){
            return -1;
        }
        int ans = stack2[point2--];
        return ans;
    }
}
```



