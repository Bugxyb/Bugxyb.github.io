---
layout: post
title: LeetCode Biweekly Contest 60
categories: LeetCode
---
头晕了，罚时太傻逼了

# T1: Find the Middle Index in Array
计算综合，然后通过总和来枚举每一个index找出合适值输出

# T2: Find All Groups of Farmland
BFS，然后统计长宽里面是不是都是1

# T3: Operations on Tree
树上模拟直接操作即可

# T4: The Number of Good Subsets
最傻逼的一道题目，状态压缩，只需要记录小于30的质数（10个），计算即可。
优化一点就是每个数最多出现一次，所以可以进行数据统计，时间复杂度降低。
而不是傻逼的10^5个数全部遍历
