---
layout: post
title: LeetCode Biweekly Contest 65
categories: LeetCode
---
心态崩了，第二题太坑，然后键盘出问题，连删三次代码，哭泣

# T1: Check Whether Two Strings are Almost Equivalent
模拟统计即可

# T2: Walking Robot Simulation II
模拟操作，然后可以优化多次循环操作，但是至少要留一次循环（因为方向问题）

# T3: Most Beautiful item for Each Query
排序后进行统计询问即可

# T4: Maximum Number of Tasks You Can Assign
无论怎么样，完成的Tasks一定是前面力量最小的。所以二分答案，然后判断是否能完成：
如果直接完成就完成，不能就找个能吃药的完成进行判断即可，通过TreeMap来统计。
