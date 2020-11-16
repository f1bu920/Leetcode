---
title: nowcoder-验证IP地址
date: 2020-11-16 13:36:09
category: Nowcoder
tags:
  - String
---

# nowcoder-验证IP地址

## 题目描述

编写一个函数来验证输入的字符串是否是有效的 IPv4 或 IPv6 地址

IPv4 地址由十进制数和点来表示，每个地址包含4个十进制数，其范围为 0 - 255， 用(".")分割。比如，172.16.254.1；
同时，IPv4 地址内的数不会以 0 开头。比如，地址 172.16.254.01 是不合法的。

IPv6 地址由8组16进制的数字来表示，每组表示 16 比特。这些组数字通过 (":")分割。比如, 2001:0db8:85a3:0000:0000:8a2e:0370:7334 是一个有效的地址。而且，我们可以加入一些以 0 开头的数字，字母可以使用大写，也可以是小写。所以， 2001:db8:85a3:0:0:8A2E:0370:7334 也是一个有效的 IPv6 address地址 (即，忽略 0 开头，忽略大小写)。

然而，我们不能因为某个组的值为 0，而使用一个空的组，以至于出现 (::) 的情况。 比如， 2001:0db8:85a3::8A2E:0370:7334 是无效的 IPv6 地址。
同时，在 IPv6 地址中，多余的 0 也是不被允许的。比如， 02001:0db8:85a3:0000:0000:8a2e:0370:7334 是无效的。

说明: 你可以认为给定的字符串里没有空格或者其他特殊字符。

[题目链接](https://www.nowcoder.com/practice/55fb3c68d08d46119f76ae2df7566880?tpId=190&&tqId=35411&rp=1&ru=/ta/job-code-high-rd&qru=/ta/job-code-high-rd/question-ranking)

<!--more-->

示例1

## 输入

[复制](javascript:void(0);)

```
"172.16.254.1"
```

## 返回值

[复制](javascript:void(0);)

```
"IPv4"
```

## 说明

```
这是一个有效的 IPv4 地址, 所以返回 "IPv4"
```

示例2

## 输入

[复制](javascript:void(0);)

```
"2001:0db8:85a3:0:0:8A2E:0370:7334"
```

## 返回值

[复制](javascript:void(0);)

```
"IPv6"
```

## 说明

```
这是一个有效的 IPv6 地址, 所以返回 "IPv6"
```

示例3

## 输入

[复制](javascript:void(0);)

```
"256.256.256.256"
```

## 返回值

[复制](javascript:void(0);)

```
"Neither"
```

## 说明

```
这个地址既不是 IPv4 也不是 IPv6 地址
```

## 备注:

```
ip地址的类型，可能为
IPv4,   IPv6,   Neither
```



## 代码实现

```java
import java.util.*;


public class Solution {
    /**
     * 验证IP地址
     * @param IP string字符串 一个IP地址字符串
     * @return string字符串
     */
    public String solve (String IP) {
        // write code here
        String neither = "Neither";
        String ipv4 = "IPv4";
        String ipv6 = "IPv6";
        if(IP == null){
            return neither;
        }
        if(isIpv4(IP)){
            return ipv4;
        }else if(isIpv6(IP)){
            return ipv6;
        }else{
            return neither;
        }
    }
    //判断是否是Ipv4地址
    private boolean isIpv4(String ip){
        String[] strs = ip.split("\\.");
        if(strs.length != 4){
            return false;
        }
        for(String str : strs){
            if(str.startsWith("0") && str.length() > 1){
                return false;
            }
            if(str.length() == 0){
                return false;
            }
            //进行转换时报异常直接返回false
            try{
                int num = Integer.parseInt(str);
                if(num < 0 || num > 255){
                    return false;
                }
            }catch(Exception e){
                return false;
            }
        }
        return true;
    }
    //判断是否是Ipv6地址
    private boolean isIpv6(String ip){
        String[] strs = ip.split(":");
        if(strs.length != 8){
            return false;
        }
        for(String str : strs){
            if(str.length() > 4){
                return false;
            }
        }
        return true;
    }
}
```

