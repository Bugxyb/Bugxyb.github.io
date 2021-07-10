---
layout: post
title: LeetCode Biweekly Contest 56
---

题目难度一般，罚时过多，导致损失较大

# T1: Count Square Sum Triples
暴力统计即可

# T2: Nearest Exit from Entrance in Maze
BFS

# T3: Sum Game
数论游戏，简化后为A和B依次从0-9选数，选X个，问选完是否为Sum则B赢，否则A赢。

结论是：X必须为偶数，且sum * 2 = tot * 9 那么B赢，否则A赢。

# T4: Minimum Cost to Reach Destination in Time
一个图，从0出发到n-1，路上有时间消耗，每经过一个城市则有一个cost消耗，问在最大时间内到达n-1的时候，最小开销是多少。

优先队列即可，剪枝：如果经过重复的城市时，必须要经过这个城市的费用要低于之前经过的费用，否则直接剪掉。
