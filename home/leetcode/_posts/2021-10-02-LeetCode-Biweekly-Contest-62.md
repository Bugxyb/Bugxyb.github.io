---
layout: post
title: LeetCode Biweekly Contest 62
categories: LeetCode
---
上周比赛没打（折腾人），今天比赛比较简单，最后一题比较迟钝

# T1: Convert 1D Array Into 2D Array
先判断是否可行再暴力模拟即可

# T2: Number of Pairs of Strings With Concatenation Equal to Target
枚举暴力即可

# T3: Maximize the Confusion of an Exam
分别计算转成T或者转成F，求两者最大值。可以直接用线性扫描O（N）复杂度解决。

# T4: Maximum Number of Ways to Parition an Array
假设等式替换为Left-Right，枚举某个数进行变动，那么如果这个数在等式左侧，那么
左侧Left为变动为k-num，那么只需要知道左侧这部分差值为k-num，同理右侧也是，两者
求和即可
```java
public int waysToPartition(int[] nums, int k) {
    HashMap<Long, Integer> rmap = new HashMap<>();
    HashMap<Long, Integer> lmap = new HashMap<>();
    long cnt = 0;
    long now = 0;
    for(int num : nums) {
        cnt += num;
    }
    long left = 0;
    long right = cnt;
    for(int i=0;i<nums.length-1;i++) {
        left += nums[i];
        right -= nums[i];
        long v = left - right;
        rmap.put(v, rmap.getOrDefault(v, 0) + 1);
    }
    int ans = rmap.getOrDefault(0l,0);
    for(int i=0;i<nums.length;i++) {
        now += nums[i];
        cnt -= nums[i];
        long v = now - cnt;
        long diff = k - nums[i];
        ans = Math.max(ans, lmap.getOrDefault(diff, 0) + rmap.getOrDefault(-diff,0));
        if (i != nums.length-1) {
            rmap.put(v, rmap.get(v) - 1);
            lmap.put(v, lmap.getOrDefault(v, 0) + 1);
        }
    }
    return ans;
}
```
