---
layout: post
title: LeetCode Weekly Contest 262
categories: LeetCode
---
整个人傻乎乎的，虽然全部做完了，但是时间整个人都是懵逼的，前三题耗时太长了。

# T1: Two out of Three
用二进制表示3个数组的位置，找出1出现2次以上的即可

# T2: Minimum Operations to Make a Uni-Value Grid
映射到线性空间上，然后O（n）计算求解，求解前先判断是否正常

# T3: Stock Price Fluctuation
使用TreeSet即可，可以直接使用Long（当时傻掉了）来组合Timestamp和Price

# T4: Partition Array Into Two Arrays to Minimize Sum Difference
假设数组总和为sum，那么找一个a,满足sum-2*a最小，且2*a小于等于sum（如果sum为负数，可以转换成正数）
假设数组长度是2*n，拆成两个n长度的数组，进行计算求和。转换成
2个数组集合，第一个集合找出k个数，第二个集合找出n-k个数，且满足这两个数相加
的和符合前面的条件，可以排序线性扫描计算
