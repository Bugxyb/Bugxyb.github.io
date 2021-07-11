---
layout: post
title: LeetCode Biweekly Contest 55
categories: LeetCode
---
看环法最后大摔车了，所以最后一题发呆有点儿久

# T1: Remove One Element to Make the Array Strictly Increasing
问一个数列A，最多删除一个元素能不能递增：枚举要删除的元素，然后暴力判断即可

# T2: Remove All Occurrences of a Substring
暴力模拟

# T3: Maximum Alternating Subsequence Sum
DP思路，处理前I个数，已经统计了偶数和奇数个数后的最大值即可

```java
fn[0][0] = nums[0];
fn[0][1] = 0;
fn[i][0] = Math.max(fn[i-1][0], fn[i-1][1] + nums[i]);
fn[i][1] = Math.max(fn[i-1][1], fn[i-1][0] - nums[i]);
```

# T4: Design Movie Rental System
因为Shop+Movie+Price总长度加起来小于Long，所以通过TreeSet来维护借出和还未借出的列表（排序）。

```java
//shop_movie的价格
private HashMap<Long, Integer> moviePrice;
//还未借出的movie，记录是movie-price_shop
private HashMap<Integer, TreeSet<Long>> topMovie;
//已经借出的movie，记录为price_shop_movie
private TreeSet<Long> rentSet;
```

分别维护topMovie和rentSet两个TreeSet即可，在进行search和report操作时候，通过对TreeSet的Iterator操作来处理前5个元素即可。
