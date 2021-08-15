---
layout: post
title: LeetCode Weekly Contest 253
categories: LeetCode
---
一蹦毁所有,太简单了

# T1: Check If String is a Prefix of Array
判断一个字符串是不是由给定数组的前K个子串拼接而成，
暴力判断即可，但是真的坑太多了

# T2: Remove Stones to Minimize the Total
贪心，每次移除最多的石头堆就行了，通过优先队列处理

# T3: Minimum Number of Swaps to Make the String Balanced
括号匹配，需要满足针对一个右括号，需要前面的左括号大于右括号数量即可，
所以统计就行，如果不满足就把右括号变成左括号

# T4: Find the Longest Valid Obstacle Course at Each Position
每个位置到最长非连续递增子序列，通过树状数组维护即可，
即找前面值小于等于num\[i\]的最大值即可
