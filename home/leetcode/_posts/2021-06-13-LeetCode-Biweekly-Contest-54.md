---
layout: post
title: LeetCode Biweekly Contest 54
categories: LeetCode
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
枚举从每个点开始，找到满足条件的k是不是最大的，暴力求解即可

# T4: Minimum Cost to Change the Final Value of Expression
转后缀表示，去掉括号符号，然后f[0/1] 分别表示该值为0或者1时候，最少需要操作多少次。

```java
private List<Character> changeToSuffix(String exp) {
    List<Character> ans = new ArrayList<>();
    LinkedList<Character> op = new LinkedList<>();
    for(char ch : exp.toCharArray()) {
        if (ch == '&' || ch == '|' || ch=='(') {
            op.add(ch);
            continue;
        }
        if (ch == ')') {
            op.removeLast();
        }
        if (ch == '0' || ch == '1') {
            ans.add(ch);
        }
        while((op.size()>0) && (op.getLast() != '(')) {
            ans.add(op.removeLast());
        }
    }
    return ans;
}
public int minOperationsToFlip(String expression) {
    List<Character> op = changeToSuffix(expression);
    LinkedList<int[]> ans = new LinkedList<>();
    for (Character ch: op) {
        int[] t = new int[3];
        if (ch == '0' || ch == '1') {
            t[0] = ch - '0';
            t[1] = '1' - ch;
            t[2] = ch - '0';
            ans.add(t);
            continue;
        }
        int[] t1 = ans.removeLast();
        int[] t2 = ans.removeLast();
        if (ch == '&') {
            t[0]=Math.min(Math.min(t1[0], t2[0]), t1[0]+t2[0]+1);
            t[1]=Math.min(t1[1]+t2[1], Math.min(t1[1], t2[1])+1);
            t[2]=t1[2]&t2[2];
        }
        if (ch == '|') {
            t[0]=Math.min(t1[0]+t2[0], Math.min(t1[0], t2[0])+1);
            t[1]=Math.min(Math.min(t1[1], t2[1]), t1[1]+t2[1]+1);
            t[2]=t1[2]|t2[2];
        }
        ans.add(t);
    }
    int[] ret = ans.removeLast();
    return ret[1-ret[2]];
}
```
