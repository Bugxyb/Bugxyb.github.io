---
layout: post
title: LeetCode Weekly Contest 254
categories: LeetCode
---
可以把我的Mac Hub直接丢了，垃圾！

# T1: Number of Strings That Appear as Substrings in Word
判断子串的问题，数据不大，直接字符串处理即可

# T2: Array With Elements Not Equal to Average of Neighbors
重排序问题，因为没有相同的数字，只需要保证两边的数字比我大或者小即可，
从小到大排序，然后一小一大的插入进去就满足了

# T3: Minimum Non-Zero Product of the Array Elements
结论题：2^P-2 个数，可以调整到一半为1，一半为2^P-2即可，注意精度处理

# T4: Last Day Where You Can Still Cross
并查集处理，判断是否已经横跨即可。

```java
private int[][] fn;

private int find(int k) {
    if (fn[k][0] != k) {
        int res = find(fn[k][0]);
        fn[res][1] = Math.min(fn[res][1], fn[k][1]);
        fn[res][2] = Math.max(fn[res][2], fn[k][2]);
        fn[k][0] = res;
    }
    return fn[k][0];
}

private boolean add(int x, int y, int row, int col) {
    int k = x * col + y;
    fn[k][0] = k;
    fn[k][1] = y;
    fn[k][2] = y;
    for(int i=0;i<flag.length;i++) {
        int xx = x + flag[i][0];
        int yy = y + flag[i][1];
        int kk = xx * col + yy;
        if (xx>=0 && xx<row && yy>=0 && yy<col && fn[kk][0] != -1) {
            int father = find(kk);
            fn[father][0] = k;
            fn[k][1] = Math.min(fn[k][1], fn[father][1]);
            fn[k][2] = Math.max(fn[k][2], fn[father][2]);
        }
    }
    if (fn[k][1] == 0 && fn[k][2] == col-1) {
        return true;
    }
    return false;
}

public int latestDayToCross(int row, int col, int[][] cells) {
    int n = row * col;
    fn = new int[n][3];
    for(int i=0;i<n;i++) {
        fn[i] = -1;
    }
    int ans = 0;
    for(int[] cell : cells) {
        if (add(cell[0]-1, cell[1]-1, row, col)) {
            break;
        }
        ans++;
    }
    return ans;
}
```
