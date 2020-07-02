---
title: nowcoder.24点运算
date: 2020-06-19 09:36:50
categories: nowcoder
tags:
  - 枚举
---

## nowcoder.24点运算

### 题目描述

计算24点是一种扑克牌益智游戏，随机抽出4张扑克牌，通过加(+)，减(-)，乘(*), 除(/)四种运算法则计算得到整数24，本问题中，扑克牌通过如下字符或者字符串表示，其中，小写joker表示小王，大写JOKER表示大王： 

​          3 4 5 6 7 8 9 10 J Q K A 2 joker JOKER

本程序要求实现：输入4张牌，输出一个算式，算式的结果为24点。 

详细说明： 

1.运算只考虑加减乘除运算，没有阶乘等特殊运算符号，友情提醒，整数除法要当心； 

2.牌面2~10对应的权值为2~10, J、Q、K、A权值分别为为11、12、13、1； 

3.输入4张牌为字符串形式，以一个空格隔开，首尾无空格；如果输入的4张牌中包含大小王，则输出字符串“ERROR”，表示无法运算； 

4.输出的算式格式为4张牌通过+-*/四个运算符相连，中间无空格，4张牌出现顺序任意，只要结果正确； 

5.输出算式的运算顺序从左至右，不包含括号，如1+2+3*4的结果为24

6.如果存在多种算式都能计算得出24，只需输出一种即可，如果无法得出24，则输出“NONE”表示无解。

[链接](https://www.nowcoder.com/practice/7e124483271e4c979a82eb2956544f9d?tpId=37&&tqId=21312&rp=1&ru=/ta/huawei&qru=/ta/huawei/question-ranking)

<!--more-->

### 输入描述:

```
输入4张牌为字符串形式，以一个空格隔开，首尾无空格；
```

### 输出描述:

```
如果输入的4张牌中包含大小王，则输出字符串“ERROR”，表示无法运算； 
```

示例1

### 输入

```
A A A A
```

### 输出

```
NONE
```



### 思路

对于输入的字符串`input`，先判断其中有没有`JOKER`。

创建辅助函数`changeStringToInt`将字符类型的牌转化为数字类型，例如将`A`转化为1，将`J`转化为11，如果牌是`JOKER`则返回-1。

创建方法`getAll`获得所有的运算符数组，因为一共有四张牌，所以一共有三种运算符，则一共有64种可能，每种可能有三个运算符，即`char[][] all = new char[64][3]`。

创建单个计算函数`getSum`，输入两个数字和一个运算符，返回他们的运算结果。

对于四个数字进行四层枚举，遍历运算符数组，如果得到的结果等于24，打印并返回；如果遍历结束还没有等于24的结果，则输出`NONE`。



### 代码实现

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
    //运算符列表
    static char[] operations = {'+', '-', '*', '/'};

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String input = null;
        while ((input = br.readLine()) != null) {
            String[] strs = input.split(" ");
            //获取四张牌对应的数字
            int a = changeStringToInt(strs[0]);
            int b = changeStringToInt(strs[1]);
            int c = changeStringToInt(strs[2]);
            int d = changeStringToInt(strs[3]);
            if (a == -1 || b == -1 || c == -1 || d == -1) {
                System.out.println("ERROR");
            } else {
                calculate(a, b, c, d);
            }
        }
    }
    //将牌转化为对应的数字
    private static int changeStringToInt(String s) {
        switch (s.toUpperCase()) {
            case "A":
                return 1;
            case "J":
                return 11;
            case "Q":
                return 12;
            case "K":
                return 13;
            case "JOKER":
                return -1;
            default:
                return Integer.parseInt(s);
        }
    }
    //将数字转化为对应的牌
    private static String changeIntToString(int i) {
        switch (i) {
            case 1:
                return "A";
            case 11:
                return "J";
            case 12:
                return "Q";
            case 13:
                return "K";
            default:
                return String.valueOf(i);
        }
    }
    //获取所有的运算符排列组合的数组
    private static char[][] getAll() {
        int index = 0;
        char[][] all = new char[64][3];
        for (int i = 0; i < 4; i++) {
            for (int j = 0; j < 4; j++) {
                for (int k = 0; k < 4; k++) {
                    all[index++] = new char[]{operations[i], operations[j], operations[k]};
                }
            }
        }
        return all;
    }

    private static void calculate(int a, int b, int c, int d) {
        int[] arr = {a, b, c, d};
        char[][] all = getAll();
        //四个数字排列组合
        for (int i = 0; i < 4; i++) {
            for (int j = 0; j < 4; j++) {
                for (int k = 0; k < 4; k++) {
                    for (int l = 0; l < 4; l++) {
                        //除去重复的情况
                        if (i != j && i != k && i != l && j != k && j != l && k != l) {
                            //对每一种枚举情况都遍历一次运算符数组
                            for (char[] chars : all) {
                                int sum = getSum(arr[i], arr[j], chars[0]);
                                sum = getSum(sum, arr[k], chars[1]);
                                sum = getSum(sum, arr[l], chars[2]);
                                if (sum == 24) {
                                    System.out.println(changeIntToString(arr[i]) + chars[0] + changeIntToString(arr[j]) + chars[1] + changeIntToString(arr[k]) + chars[2] + changeIntToString(arr[l]));
                                    return;
                                }
                            }
                        }
                    }
                }
            }
        }
        System.out.println("NONE");
    }

    private static int getSum(int a, int b, char c) {
        int sum = 0;
        switch (c) {
            case '+':
                sum = a + b;
                break;
            case '-':
                sum = a - b;
                break;
            case '*':
                sum = a * b;
                break;
            case '/':
                sum = a / b;
                break;
            default:
                return 0;
        }
        return sum;
    }
}
```



