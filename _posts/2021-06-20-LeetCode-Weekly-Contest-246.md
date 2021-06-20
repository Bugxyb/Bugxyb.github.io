---
layout: post
title: LeetCode Contest 246
---
写代码速度有点慢，没想到最后一题还是偏简单，第二题和第三题浪费太多时间了

# T1: Largest Odd Number in String
找出最长的奇数大整数：找到最后一个奇数，前面的子串就是答案

# T2: The Number of Full Rounds You Have Played
给定两个时间：startTime和finishTime，计算中间隔了多少个Quarter-Hour。分别计算两者距离00：00有多少个Quarter-Hour，然后两者相减即可

```java
private int check(String time, int fn) {
    String[] ti = time.split(":");
    int hh = Integer.valueOf(ti[0]);
    int mm = Integer.valueOf(ti[1]);
    int ret = hh * 4 + mm / 15 + (mm % 15 != 0 ? fn : 0);
    return ret;
}
public int numberOfRounds(String startTime, String finishTime) {
    int ans = 0;
    int sTime = check(startTime, 1);
    int fTime = check(finishTime, 0);
    if (sTime <= fTime) {
        ans = fTime - sTime;
    } else {
        ans = 4 * 24 - (sTime - fTime);
    }
    return ans;
}
```

# T3: Count Sub Islands
统计grid2中有多少个Islands是grid1的子集，暴力即可，先统计grid2中的Island，然后判断是不是grid1的子集

# T4: Minimum Absolute Difference Queries
给定序列A, 询问a[i]到a[j]中，最小的绝对值之差，A的值在[1, 100]。

没想到这题这么弱智。由于A的值很小，所以维护一个100*nums.length的数组，然后每次询问，先确定这个询问范围内的值，然后计算最小绝对值即可。

```java
private int maxn = 100;

public int[] minDifference(int[] nums, int[][] queries) {
    int n = nums.length;
    int[] ans = new int[queries.length];
    int[][] fn = new int[maxn][n+1];
    for(int i=0;i<n;i++) {
        fn[nums[i]-1][i+1] += 1;
    }
    for(int k=0;k<maxn;k++) {
        for(int i=1;i<=n;i++) {
            fn[k][i] += fn[k][i-1];
        }
    }
    for(int i=0;i<queries.length;i++) {
        int old = -1;
        ans[i] = -1;
        for(int k=0;k<maxn;k++) {
            if (fn[k][queries[i][1]+1] - fn[k][queries[i][0]] == 0) {
                continue;
            }
            if (old != -1) {
                if (ans[i] == -1) {
                    ans[i] = k - old;
                } else {
                    ans[i] = Math.min(ans[i], k - old);
                }
            }
            old = k;
        }
    }
    return ans;
}
```
