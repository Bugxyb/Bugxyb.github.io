---
layout: post
title: LeetCode Weekly Contest 266
categories: LeetCode
---
由于搬家，所以上周比赛没有参加，今天比赛难度简单，找回状态中（状态偏不行）

# T1: Count Vowel SubStrings of a String
直接枚举统计即可，注意是子串有且只有5种字符

# T2: Vowels of All Substrings
找到对应的Vowel字符，然后计算出包含这个字符由多少个子串即可，数学统计计算

# T3: Minimized Maximum of Products Distributed to Any Store
二分答案，判断答案是否ok

# T4: Maximum Path Quality of a Graph
搜索即可，因为maxTime/Time最大是10，所以最多枚举10步即可，而且每个点最多只有4条边，
后面可以做个优化就是判断这个点回0的最小时间，因为终点要为0
