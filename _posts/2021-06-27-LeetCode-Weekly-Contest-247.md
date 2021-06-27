---
layout: post
title: LeetCode Contest 247
---
每周例行崩溃，倒数第三题卡超时，导致最后一题没时间做了

# T1: Maximum Product Differenct Between Two Pairs
取最大2个和最小2个，然后两者相乘再相减即可

# T2: Cyclically Rotating a Grid
暴力模拟转动即可

# T3: Number of Wornderful Substrings
状态压缩的数学统计，记录i-j的状态为(1-j)^(1-i-1)的状态，1-j的状态提前记录下来，时间复杂度为10n

```java
public long wonderfulSubstrings(String word) {
    long[] fn = new long[1024];
    fn[0] = 1;
    int now = 0;
    long ans = 0;
    for(int i=0;i<word.length();i++) {
        int p = 1 << (word.charAt(i) - 'a');
        now = now ^ p;
        ans += fn[now];
        for(int k=0;k<10;k++) {
            ans += fn[now ^ (1 << k)];
        }
        fn[now] += 1;
    }
    return ans;
}
```

# T4: Count Ways to Build Rooms in an Ant Colony
数学统计，假设两颗子树分别统计方案数和子树结点为Way1,Cnt1, Way2, Cnt2,那么这两个子树的方案是C\[Cn1\]\[Cnt1+Cnt2\] * Way1 * Way2取模，
然后C可以通过费马小定理进行计算求出，费马小定理：a ^ (p-1) % p = 1 => a^(p-2) % p = 1/a
