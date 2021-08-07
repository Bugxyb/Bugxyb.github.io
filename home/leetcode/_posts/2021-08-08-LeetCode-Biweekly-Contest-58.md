---
layout: post
title: LeetCode Biweekly Contest 58
categories: LeetCode
---
最后一题，算法知道就会做，不知道不会做

# T1: Delete Characters to Make Fancy String
删除字符保证不出现连续3个相同字符的字符串，暴力模拟即可

# T2: Check if Move is Legal
8*8的矩阵，给定一个位置，问8个方向中是否存在一个方向有一个大于3的区间，
中间的颜色一样，但和两头的颜色不一致。暴力模拟判断即可

# T3: Minimum Total Space Wasted With K Resizing Operations
动态规划解决：F\[i\]\[k\]表示前i个数组，改变了k次的最小值多少，提前做好预处理即可：

```java
    public int minSpaceWastedKResizing(int[] nums, int k) {
    int n = nums.length;
    int[][] sum = new int[n][n];
    for(int i=0;i<n;i++) {
        int max = nums[i];
        int cnt = nums[i];
        sum[i][i] = 0;
        for(int j=i+1;j<n;j++) {
            max = Math.max(max, nums[j]);
            cnt += nums[j];
            sum[i][j] = max * (j-i+1) - cnt;
        }
    }
    int[][] fn = new int[n][k+1];
    for(int i=0;i<n;i++) {
        fn[i][0] = sum[0][i];
        for(int tk=1;tk<=k;tk++) {
            fn[i][tk] = sum[0][i];
            for(int j=i-1;j>=0;j--) {
                fn[i][tk] = Math.min(fn[i][tk], fn[j][tk-1] + sum[j+1][i]);
            }
        }
    }
    return fn[n-1][k];
}
```

# T4: Maximum Product of the Length of Two Palindromic Substirngs
给定一个字符串，然后找出2个奇数的回文子串，其长度相乘最大。
Manacher's算法，会就会，不会就不会（白给）

```java
public long maxProduct(String s) {
    int n = s.length();
    int[] p = new int[n];
    int mx = 0;
    int center = 0;
    for(int i=0;i<n;i++) {
        p[i] = mx > i ? Math.min(p[2 * center - i], mx - i) : 0;
        while (i+p[i]+1<n && i-p[i]-1>=0 && s.charAt(i+p[i]+1) == s.charAt(i-p[i]-1)) {
            p[i]++;
        }
        if (mx < i+ p[i]) {
            mx = i + p[i];
            center = i;
        }
    }
    long[] fnl = new long[n];
    long[] fnr = new long[n];
    LinkedList<Integer> que = new LinkedList<>();
    fnl[0] = 1;
    que.add(0);
    for(int i=1;i<n;i++){
        fnl[i] = 1;
        while(! que.isEmpty()) {
            int x = que.getFirst();
            if (x+p[x] < i) {
                que.removeFirst();
            } else {
                fnl[i] = 2L * (Math.min(i, x+p[x]) - x) + 1;
                break;
            }
        }
        que.add(i);
        fnl[i] = Math.max(fnl[i], fnl[i-1]);
    }
    que.clear();
    fnr[n-1] = 1;
    que.add(n-1);
    for(int i=n-2;i>=0;i--) {
        fnr[i] = 1;
        while(! que.isEmpty()) {
            int x = que.getFirst();
            if (x - p[x] > i) {
                que.removeFirst();
            } else {
                fnr[i] = 2L * (x - Math.max(i, x - p[x])) + 1;
                break;
            }
        }
        que.add(i);
        fnr[i] = Math.max(fnr[i], fnr[i+1]);
    }
    long ans = 0;
    for(int i=0;i<n-1;i++) {
        ans = Math.max(ans, fnl[i] * fnr[i+1]);
    }
    return ans;
}
```
