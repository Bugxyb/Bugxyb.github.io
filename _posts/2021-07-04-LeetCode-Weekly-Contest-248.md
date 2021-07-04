---
layout: post
title: LeetCode Contest 248
---
最后一题不会做，使用RabinKarp的Hash匹配算法

# T1: Build Array from Permutation
暴力模拟

# T2: Eliminate Maximum Number of Monsters
计算到达的时间，排序，然后模拟统计

# T3: Count Good Numbers
数论方法，直接计算即可

# T4: Longest Common Subpath
使用RaBinKarp的算法计算，详细见代码（Java数学处理没Python优势）:
```java
class Solution {
    private Set<Long> RabinKarp(int[] path, int len, long mod) {
        Set<Long> allHashes = new HashSet<>();

        long h = 1;
        long h2 = 2;
        long n = 17 * len -17;
        while(n>0) {
            if (n % 2==1) {
                h = (h * h2) % mod;
            }
            h2 = (h2 * h2)% mod;
            n=n >> 1;
        }

        long t = 0;
        long d = 1 << 17;

        for(int i=0;i<len;i++) {
            t = (d * t + path[i]) % mod;
        }
        allHashes.add(t);
        for(int i=0;i<path.length-len;i++) {
            t = (t - path[i] * h) % mod;
            t = (d * t + path[i+len]) % mod;
            t = (t+mod)%mod;
            allHashes.add(t);
        }

        return allHashes;
    }

    public int longestCommonSubpath(int n, int[][] paths) {
        int m = paths.length;
        int[] u = new int[]{1, 19, 61, 69, 85, 99, 105};
        int uk = u.length;
        long[] mods = new long[uk];
        for(int i=0;i<uk;i++) {
            mods[i] = (1 << 31) - u[i];
        }
        int st=0;
        int en=paths[0].length+1;
        for(int i=1;i<m;i++){
            en = Math.min(en, paths[i].length+1);
        }
        while (st+1<en) {
            int mid = (st + en)>>1;
            boolean globalCheck = true;
            for(int i=0;i<uk;i++) {
                Set<Long> value = RabinKarp(paths[0], mid, mods[i]);
                for(int k=0;k<m;k++) {
                    if (value.isEmpty()) {
                        break;
                    }
                    Set<Long> temp = RabinKarp(paths[k], mid, mods[i]);
                    value.retainAll(temp);
                }
                if (value.isEmpty()) {
                    globalCheck = false;
                    break;
                }
            }
            System.out.println(st+":"+en+":"+mid+":"+globalCheck);
            if (globalCheck) {
                st = mid;
            } else {
                en = mid;
            }
        }
        return st;
    }
}
```
