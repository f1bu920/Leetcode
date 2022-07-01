---
title: Leetcode241.为运算表达式设计优先级
date: 2022-07-01 16:15:39
categories: Leetcode
tags:
  - 递归
  - 记忆化搜索
---

## Leetcode241.为运算表达式设计优先级

给你一个由数字和运算符组成的字符串` expression` ，按不同优先级组合数字和运算符，计算并返回所有可能组合的结果。你可以 按任意顺序 返回答案。

生成的测试用例满足其对应输出值符合 32 位整数范围，不同结果的数量不超过 10的四次方 。

 <!--more-->

示例 1：

```java
输入：expression = "2-1-1"
输出：[0,2]
解释：
((2-1)-1) = 0 
(2-(1-1)) = 2
```



示例 2：

```java
输入：expression = "2*3-4*5"
输出：[-34,-14,-10,-10,10]
解释：
(2*(3-(4*5))) = -34 
((2*3)-(4*5)) = -14 
((2*(3-4))*5) = -10 
(2*((3-4)*5)) = -10 
(((2*3)-4)*5) = 10
```




提示：

- 1 <= expression.length <= 20
- expression 由数字和算符 '+'、'-' 和 '*' 组成。
- 输入表达式中的所有整数值在范围 [0, 99] 

### 思路

本质上是一个分治问题，即大问题划分成左右两个小问题，对于一个形如`x op y`的表达式(`op`为运算符，`x y`为数字)，它的组合结果取决于`x`和`y`的结果组合数，`x`和`y`则又是一个形如`x op y`的表达式问题。

思路分为三步：

1. 将表达式按运算符分为左右两个部分，分别求解
2. 递归求解
3. 合并，根据左右两边的解，算出最终解。



### 实现

```go
func diffWaysToCompute(input string) []int {
	// 判断是否全为数字，如果全为数字直接返回
	if isAllDigit(input) {
		num, _ :=strconv.Atoi(input)
		return []int{num}
	}

	var result []int
	for i, c := range input {
		curr := string(c)
		if curr == "+" || curr == "-" || curr == "*" {
            // 递归
            // 左边集合
			left := diffWaysToCompute(input[:i])
            // 右边集合
			right := diffWaysToCompute(input[i+1:])
            // 遍历
			for _, leftNum := range left {
				for _, rightNum := range right {
					var num int
					if curr == "+" {
						num = leftNum + rightNum
					} else if curr == "-" {
						num = leftNum - rightNum
					} else if curr == "*" {
						num = leftNum * rightNum
					}
					result = append(result, num)
				}
			}
		}
	}
	return result
}

func isAllDigit(input string) bool {
	_, err := strconv.Atoi(input)
	if err != nil {
		return false
	}
	return true
}

```

