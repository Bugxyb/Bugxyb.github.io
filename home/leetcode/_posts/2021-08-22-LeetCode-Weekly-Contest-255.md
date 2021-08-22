---
layout: post
title: LeetCode Weekly Contest 255
categories: LeetCode
---
最后一题稍微卡住了，极限过题，但是整体还行，应该进前100了。

# T1: Find Greatest Common Divisor of Array
找出最大最小的数，求他们的最大公约数

# T2: Find Unique Binary String
把字符串（二进制）转成十进制数，找出不存在的数字，然后再转成二进制输出

# T3: Minimizee the Difference Between Target and Chosen Elements
统计,F\[i,k\]表示前i行，每行选一个数能不能达到k，然后最后和target进行统计即可

# T4: Find Array Given Subset Sums
模拟题，一个结论：按绝对值从小到大枚举每一个数，然后判断能不能根据这个数把数组
一分为二，如果可以，那么再对拆分的数据执行相同操作即可。
