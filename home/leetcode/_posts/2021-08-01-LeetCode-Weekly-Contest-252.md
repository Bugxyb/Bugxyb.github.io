---
layout: post
title: LeetCode Weekly Contest 252
categories: LeetCode
---
最弱考试题目，自己竟然傻逼了。大概可以25min内写完。

# T1: Three Divisors
判断这个数是不是质数的平方（1除外），暴力模拟即可

# T2: Maximum Number of Weeks for Which You Can Work
结论题，如果最大的里程大于剩余里程+2，那么完成是2*剩余里程+1，否则所有里程都能完成

# T3: Minimum Garden Perimeter to Collect Enough Apples
暴力题：依次枚举每条边长度，然后计算苹果数是否满足即可

# T4: Count Number of Special Subsequences
统计题：F\[i\]\[k\]表示到前I个位置，且最后一个为K的子串数字，那么统计
F\[i\]\[k\] = 2 * F\[i-1\]\[k\] + F\[i\]\[k-1\] 如果满足nums\[i\] == k
