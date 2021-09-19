---
layout: post
title: LeetCode Biweekly Contest 61
categories: LeetCode
---
第一次30min解决战斗，奈何罚时太狠了，自己失误率过高

# T1: Count Number of Pairs With Absolute Difference K
模拟即可

# T2: Find Original Array From Doubled Array
罚时题*1，基数排序，然后模拟判断是否拆分两个数组，第一个是第二个的double即可。

# T3: Maximum Earnings From Taxi
DP题，按时间模拟即可，对Rides进行排序即可

# T4: Minimum Number of Operations to Make Array Continuous
注意重复，首选去重，去重的个数都是需要修改的。枚举开始的x，记录[x,x+n)这个区间
内有多少个去重后的数，答案就是n-这个值即可。
