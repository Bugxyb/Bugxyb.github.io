---
layout: post
title: LeetCode Biweekly Contest 63
categories: LeetCode
---
第四题稍微有点难度，前三题偏弱，但是第四题自己想了比较久

# T1: Minimum Number of Moves to Seat Everyone
排序后依次求绝对值之和

# T2: Remove Colored Pieces if Both Neighbors are the Same Color
分别计算Alice和Bob可以移除颜色的数量，返回Alice >= Bob即可

# T3: The Time When the Network Becomes Idle
计算每个结点到0的时间为N，计算在2*N的时间内最后一次发送的时间为T，取T+2*N+1的最大值即可

# T4: Kth Smallest Product of Two Sorted Arrays
对于两个数组先计算负数，0和正数的数量，求出最终数字是正数还是负数（或者是0）。
切换成两组递增（递减）的数组，通过二分来计算目标数值即可。
