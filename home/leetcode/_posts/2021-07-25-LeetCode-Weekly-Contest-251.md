---
layout: post
title: LeetCode Weekly Contest 251
categories: LeetCode
---
睡过头了，所以没有考试（还好没考，最后一题有点恶心）

# T1: Sum of Digits of String After Convert
字符串解析成数字进行K次求和（每位数求和），暴力即可。

# T2: Largest Number After Mutating Substring
给定一个字符串，找出一个连续子串，按要求改变数后，最终的字串最大。

搜索找子串，满足前面的数都大于等于改变后的数，然后子串的数要小于等于改变的数即可，然后改变拼接

# T3: Maximum Compatibility Score Sum
状态压缩动态规划，可以提前做好预处理计算分数

# T4: Delete Duplicate Floders in System
删除重复的文件夹，本质是个Tire图，构建Trie图，然后通过HashKey等之类的方法来Hash对应的子文件夹，进行判定和删除。
按规则模拟找到所有相同的文件夹，然后处理即可
