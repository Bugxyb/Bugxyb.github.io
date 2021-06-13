---
layout: post
title: LeetCode Biweekly Contest 54
---
总体一般，头两题丢时间太多。

# T1: Check if All the Integers in Range Are Coverd
给你N个范围Range，以及left和right，问你N个范围的Range是否覆盖了left-right。由于范围很小，直接用列表扫描即可
```java
public boolean isCovered(int[][] ranges, int left, int right) {
    int[] fn = new int[51];
    for(int[] range : ranges) {
        for(int idx=range[0];idx<=range[1];idx++) {
            fn[idx] = 1;
        }
    }
    for(int idx=left;idx<=right;idx++) {
        if (fn[idx]==0) {
            return false;
        }
    }
    return true;
}
```

# T2: Find the Student that Will Replace the Chalk
N个人从K开始循环减数，知道最后一个人无法减数为止，注意超范围

```java
public int chalkReplacer(int[] chalk, int k) {
    long sum = 0;
    for(int pos :chalk) {
        sum+=pos;
    }
    long t = k;
    t = t % sum;
    int now = 0;
    while(t-chalk[now]>=0) {
        t-=chalk[now];
        now++;
    }
    return now;
}
```

# T3: Largest Magic Square

# T4: Minimum Cost to Change the Final Value of Expression
