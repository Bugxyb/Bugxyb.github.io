---
layout: post
title: LeetCode Weekly Contest 263
categories: LeetCode
---
今天题目比较偏弱，只不过最后一题被罚时有点可惜，掉出了前100，
如果不被罚时，说不定能进前50

# T1: Check if Numbers Are Ascending in a Sentence
空格字符串分离，判断是不是数字，再判断是否递增即可

# T2: Simple Bank System
简单的加减模拟器，注意不为负和用户操作边界判断

# T3: Count Number of Maximum Bitwise-OR subsets
深搜即可

# T4: Second Minimum Time to Reach Destination
可以理解为双层图的路径，第一层是最快的到达时间，第二层是第二快的时间(两者不能相等），
然后直接用优先队列解决即可，注意剪枝。
