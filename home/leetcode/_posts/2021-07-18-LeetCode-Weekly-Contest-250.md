---
layout: post
title: LeetCode Weekly Contest 250
categories: LeetCode
---

总体一般，稍微失误丢了点时间，编程效率也那样。

# T1: Maximum Number of Words You Can Type
计算一个Word List中有多少个Word不包含brokenLetters的字符，暴力扫描计算即可

# T2: Add Minimum Number of Rungs
一个严格递增的List，你从0开始，每次最多移动dist层，问你在List中至少要加几个值才弄跳到List的最后一层。
直接扫描即可，如果到不了下一个，就加层值进去，注意计算，否则会超时

```java
public int addRungs(int[] rungs, int dist) {
    int ans = 0;
    int start = 0;
    for(int now : rungs) {
        if (start + dist < now) {
            int next = (now - start - 1) / dist;
            ans += next;
        }
        start = now;
    }
    return ans;
}
```
# T3: Maximum Number of Points with Cost
在一个n*m的矩阵里面，每一行选一个值，计算选取值加起来并减去相邻两行距离的值最大
针对每一行，维护值就可以了，详情见代码

```java
public long maxPoints(int[][] points) {
    int n = points.length;
    int m = points[0].length;
    long[][] fn = new long[n][m];
    for(int i=0;i<m;i++) {
        fn[0][i] = points[0][i];
    }
    for(int i=1;i<n;i++) {
        for(int j=0;j<m;j++) {
            fn[i][j] = fn[i-1][j]+points[i][j];
        }
        long recL = fn[i-1][0];
        for(int j=1;j<m;j++) {
            recL = Math.max(recL - 1, fn[i-1][j]);
            fn[i][j] = Math.max(fn[i][j], recL + points[i][j]);
        }
        long recR = fn[i-1][m-1];
        for(int j=m-2;j>=0;j--) {
            recR = Math.max(recR - 1, fn[i-1][j]);
            fn[i][j] = Math.max(fn[i][j], recR + points[i][j]);
        }
    }
    long ans = 0;
    for(int i=0;i<m;i++) {
        ans = Math.max(ans, fn[n-1][i]);
    }
    return ans;
}
```

# T4: Maximum Genetic Difference Query
给定一棵树，根节点为Root，每个结点上对应一个值为X，问你从某个结点k开始到根结点的值里面，
val与哪个值异或最大，输出最大值。

记录某个结点到根节点，用基于位运算的2叉树来记录有哪些值，然后针对每个Query进行询问判定找到最大值
时间复杂度为O((N+Q)*K)，N和Q分别为结点和Query的数量，K固定为16（logVal）
```java
private final int MAXN = 16;

private int[] ans;
private int[] fn;
private HashMap<Integer, List<int[]>> queryMap;
private HashMap<Integer, List<Integer>> tree;

private int add(int root, int level, int val) {
    int node = ((level==0) ? 1 : add(root>>1, level-1, val));
    node = 2* node + (root & 1);
    fn[node] += val;
    return node;
}

private int[] calc(int level, int val) {
    int x = val & 1;
    int now;
    int v;
    if (level == 0) {
        now = 1;
        v = 0;
    } else {
        int[] ret = calc(level-1, val>>1);
        now = ret[0];
        v = ret[1];
    }
    if (fn[2*now] == 0) {
        return new int[]{2*now+1, 2*v+1};
    }
    if (fn[2*now+1] == 0) {
        return new int[]{2*now, 2*v};
    }
    return new int[]{2*now+1-x, 2*v+1-x};
}

private void search(int root) {
    add(root, MAXN, 1);
    for(int[] que : queryMap.get(root)) {
        ans[que[0]] = calc(MAXN, que[1])[1] ^ que[1];
    }
    for(int next : tree.get(root)) {
        search(next);
    }
    add(root, MAXN, -1);
}

public int[] maxGeneticDifference(int[] parents, int[][] queries) {
    ans = new int[queries.length];
    fn = new int[1<<(MAXN+2)];
    queryMap = new HashMap<>();
    tree = new HashMap<>();
    for(int i=0;i<parents.length;i++) {
        queryMap.put(i, new ArrayList<>());
        tree.put(i, new ArrayList<>());
    }
    int root = -1;
    for(int i=0;i<parents.length;i++) {
        if (parents[i] == -1) {
            root = i;
        } else {
            tree.get(parents[i]).add(i);
        }
    }
    for(int i=0;i<queries.length;i++) {
        queryMap.get(queries[i][0]).add(new int[]{i, queries[i][1]});
    }
    search(root);
    return ans;
}
```
