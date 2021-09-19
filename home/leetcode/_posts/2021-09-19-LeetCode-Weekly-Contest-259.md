---
layout: post
title: LeetCode Weekly Contest 259
categories: LeetCode
---
最后一题有点大失所望，好像直接莽过去就行了

# T1: Find Value of Variable After Performing Operations
枚举4个操作判断即可

# T2: Sum of Beauty in the Array
O(n)复杂度，记录左边最大值，右边最小值判断即可

# T3: Detect Squares
枚举正方形长度，判断3个角有没有point

# T4: Longest Subsequence Repeated k Times
暴力莽就行，如果某个子串至少出现k次，那么这个子串前面的也至少出现k次。
做好判重查询即可，注意不是出现K次，是至少k次
