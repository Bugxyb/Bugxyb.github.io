---
layout: post
title: LeetCode Biweekly Contest 59
categories: LeetCode
---
总体成绩还行，但是KC爆了！拉胯！

# T1: Minimum Time to Type Word Using Special Typewriter
模拟顺时针或者逆时针到目标位置取最小距离相加即可。

# T2: Maximum Matrix Sum
结论题：最终只有1个负数或者0个负数，找出绝对值的最小值，其它的和减去这个最小值

# T3: Number of Ways to Arrive at Destination
简单的BFS，通过优先队列来计算即可。

# T4: Number of Ways to Separate Numbers
F\[i,k\]表示到第i位，且最后一个数组占用了最多k个长度的结果。
那么为若nums\[i-k+1,i\]大于等于nums\[i-k-k+1,i-k\]的话：
那么F\[i,k\] = F\[i,k-1\] + F\[i-k,k\] ，否则为
F\[i,k\] = F\[i,k-1\] + F\[i-k,k-1\]
具体见代码：
```java
class Solution {
    private int MOD = 1000000007;
    public int numberOfCombinations(String num) {
        int n = num.length();
        int[][] map = new int[n+1][n+1];
        int[] nums = new int[n];
        for(int i=0;i<n;i++) {
            nums[i] = num.charAt(i) - '0';
        }
        for(int i=n-1;i>=0;i--) {
            for(int j=n-1;j>i;j--) {
                if (nums[i] > nums[j]) {
                    map[i][j] = 0;
                }
                if (nums[i] == nums[j]) {
                    map[i][j] = map[i+1][j+1] +1;
                }
                if (nums[i] < nums[j]) {
                    map[i][j] = j-i+1;
                }

            }
        }
        long[][] fn = new long[n][n+1];
        for(int i=0;i<n;i++) {
            for (int k = 1; k <= i + 1; k++) {
                fn[i][k] = fn[i][k - 1];
                if (nums[i - k + 1] == 0) {
                    continue;
                }
                if (i - k + 1 == 0) {
                    fn[i][k] = (fn[i][k] + 1) % MOD;
                    continue;
                }
                if ((i - k - k + 1 >= 0) && (map[i - k - k + 1][i - k + 1] >= k)) {
                    fn[i][k] = (fn[i][k] + fn[i - k][k]) % MOD;
                } else {
                    int t = Math.min(k-1, i-k+1);
                    fn[i][k] = (fn[i][k] + fn[i - k][t]) % MOD;
                }
            }
        }
        return (int)(fn[n-1][n] % MOD);
    }
}
```
