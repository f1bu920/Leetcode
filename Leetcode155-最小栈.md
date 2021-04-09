---
title: Leetcode155.最小栈
date: 2020-07-18 10:57:26
categories: Leetcode
tags:
  - 栈
---

## Leetcode155.最小栈

设计一个支持 `push` ，`pop` ，`top` 操作，并能在常数时间内检索到最小元素的栈。

`push(x)` —— 将元素 x 推入栈中。
`pop()` —— 删除栈顶的元素。
`top()` —— 获取栈顶元素。
`getMin()` —— 检索栈中的最小元素。

[题目链接](https://leetcode-cn.com/problems/min-stack)

<!--more-->


示例:

```
输入：
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]

输出：
[null,null,null,null,-3,null,0,-2]

解释：
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.getMin();   --> 返回 -2.
```




提示：

- `pop`、`top` 和 `getMin` 操作总是在 非空栈 上调用。



### 思路

用一个数组模拟栈，设置一个指针`index`指向栈顶元素，`min`记录当前栈中最小元素，在进行`push`、`pop`操作时更新最小值。

法二：

使用两个栈，一个栈正常存值，另一个栈push时取栈顶元素和push元素的最小值压栈。

### 代码实现

```java
class MinStack {
    private int min;
    private int[] elements;
    private int size;
    private int index;

    /** initialize your data structure here. */
    public MinStack() {
        elements = new int[10000];
        min = Integer.MAX_VALUE;
        size = 0;
        index = -1;
    }
    
    public void push(int x) {
        elements[++index] = x;
        //在压栈时更新min值
        min = Math.min(min,x);
        size++;
    }
    
    public void pop() {
        if(min == elements[index]){
            min = elements[0];
            for(int i = 1;i<index;i++){
                min = Math.min(min,elements[i]);
            }
        }
        index--;
        //如果当前栈中只有一个元素，抛出后需要将min更新为最大值
        if(index==-1){
            min = Integer.MAX_VALUE;
        }
    }
    
    public int top() {
        return elements[index];
    }
    
    public int getMin() {
        return min;
    }
}

```



