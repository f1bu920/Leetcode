---
title: nowcoder.人民币转换
date: 2020-06-16 14:09:07
categories: nowcoder
tags:
  - String
  - 递归
---

## nowcoder.人民币转换

### 题目描述

考试题目和要点：

1、中文大写金额数字前应标明“人民币”字样。中文大写金额数字应用壹、贰、叁、肆、伍、陆、柒、捌、玖、拾、佰、仟、万、亿、元、角、分、零、整等字样填写。（30分） 

2、中文大写金额数字到“元”为止的，在“元”之后，应写“整字，如￥ 532.00应写成“人民币伍佰叁拾贰元整”。在”角“和”分“后面不写”整字。（30分） 

3、阿拉伯数字中间有“0”时，中文大写要写“零”字，阿拉伯数字中间连续有几个“0”时，中文大写金额中间只写一个“零”字，如￥6007.14，应写成“人民币陆仟零柒元壹角肆分“。（

 [题目链接](https://www.nowcoder.com/practice/00ffd656b9604d1998e966d555005a4b?tpId=37&&tqId=21318&rp=1&ru=/ta/huawei&qru=/ta/huawei/question-ranking)

<!--more-->

### 输入描述:

```
输入一个double数
```

### 输出描述:

```
输出人民币格式
```

示例1

### 输入

```
151121.15
```

### 输出

```
人民币拾伍万壹仟壹佰贰拾壹元壹角伍分
```



### 思路

对输入的数字`money`，分别获得其整数部分和小数部分。



### 代码实现

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
    private final static char[] NUM = {'零', '壹', '贰', '叁', '肆', '伍', '陆', '柒', '捌', '玖', '拾', '佰', '仟', '万', '亿'};

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str = null;
        while ((str = br.readLine()) != null) {
            double money = Double.parseDouble(str);
            System.out.println(convert(money));
        }
    }

    private static String convert(double money) {
        StringBuilder result = new StringBuilder("人民币");
        long n = (long) money;//整数部分
        if (n > 0) {
            convert(n, result);
            result.append("元");
        }
        //处理小数部分
        //这里加上0.001是为了防止失真，测试用例中0.29如果这里不加0.001就会被认为是0.28
        int v = (int) (money * 100 - n * 100 + 0.001);
        int i = v / 10;
        int j = v % 10;
        //小数部分为0
        if (i == 0 && j == 0) {
            result.append("整");
            return result.toString();
        }
        if (i != 0) {
            result.append(NUM[i]).append("角");
        }
        if (j != 0) {
            result.append(NUM[j]).append("分");
        }
        return result.toString();
    }
    //整数部分
    private static void convert(long n, StringBuilder result) {
        //大于1亿
        if (n >= 100000000) {
            long q = n / 100000000;
            long r = n % 100000000;
            //得到1亿前面的数字转换成的字符
            convert(q, result);
            result.append("亿");
            //不是1亿的整数倍
            if (r != 0) {
                convert(r, result);
            }
            //大于1万
        } else if (n >= 10000) {

            long q = n / 10000;
            long r = n % 10000;
            ////得到1万前面的数字转换成的字符
            convert(q, result);
            result.append("万");
            if (r != 0) {
                //如n=10990/10090,需要加上零
                if (r < 1000) {
                    result.append("零");
                }
                convert(r, result);
            }
            //大于1k
        } else if (n >= 1000) {
            long q = n / 1000;
            long r = n % 1000;
            convert(q, result);
            result.append("仟");
            if (r != 0) {
                if (r < 100) {
                    result.append("零");
                }
                convert(r, result);
            }
            //大于100
        } else if (n >= 100) {
            long q = n / 100;
            long r = n % 100;
            convert(q, result);
            result.append("佰");
            if (r != 0) {
                //n=101
                if (r < 10) {
                    result.append("零");
                }
                convert(r, result);
            }
            //大于10
        } else if (n >= 10) {
            long q = n / 10;
            long r = n % 10;
            //这里需要判断是否大于1，因为没有一十几的叫法，只有二十几的叫法。
            if (q > 1) {
                convert(q, result);
            }
            result.append("拾");
            if (r != 0) {
                convert(r, result);
            }
        } else {
            result.append(NUM[(int) n]);
        }
    }
}
```

