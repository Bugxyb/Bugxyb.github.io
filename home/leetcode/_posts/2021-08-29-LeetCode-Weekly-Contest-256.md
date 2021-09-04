---
layout: post
title: LeetCode Weekly Contest 256
categories: LeetCode
---
最后一题没做过，竟然几行代码就搞定了，不科学！！！

# T1: Minimum Difference Between Highest and Lowest of K Scores
排序计算就可以了，肯定是排序后连续的一串

# T2: Find the Kth Largest Integer in the Array
大整数排序

# T3: Minimum Number of Work Sessions to Finish the Tasks
DP解法，因为很小直接用状态压缩计算

# T4: Number of Unique Good Subsequences
见代码
```java
private long mod = 1000000007;
public int numberOfUniqueGoodSubsequences(String binary) {
    long ends0 = 0;
    long ends1 = 0;
    long has0 = 0;
    for(int i=0;i<binary.length();i++) {
        if (binary.charAt(i)-'0' == 1) {
            ends1 = (ends0 + ends1 + 1) % mod;
        } else {
            ends0 = (ends0 + ends1) % mod;
            has0 = 1;
        }
    }
    return (int)((ends0+ends1+has0) % mod);
}
```
