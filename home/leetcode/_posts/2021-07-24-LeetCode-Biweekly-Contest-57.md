---
layout: post
title: LeetCode Biweekly Contest 57
categories: LeetCode
---
万万没想到最后一题那么简单，万万没想到最后一题还错了一次

# T1: Check if All Characters Have Equal Number of Occurrences
判断字符串里面每个字符是否出现相同的次数，暴力统计模拟即可

# T2: The Number of the Smallest Unoccupied Char
N个人，有到达和离开时间，到达后找一个最小的没有人做的位置坐下，问第K个人做的位置在哪？

模拟即可，直接通过优先队列来记录空余的椅子以及即将要离开位置人的信息，然后暴力统计即可
```java
public int smallestChair(int[][] times, int targetFriend) {
    PriorityQueue<Integer> seats = new PriorityQueue<>();
    PriorityQueue<int[]> leaves = new PriorityQueue<>((a,b) -> (a[0] - b[0]));
    int n = times.length;
    int[][] qtimes = new int[n][3];
    for(int i=0;i<times.length;i++) {
        qtimes[i][0] = times[i][0];
        qtimes[i][1] = times[i][1];
        qtimes[i][2] = i;
    }
    Arrays.sort(qtimes, (a, b) -> (a[0] - b[0]));
    int cnt = 0;
    int ans = 0;
    for(int[] time : qtimes) {
        while(!leaves.isEmpty() && leaves.peek()[0] <= time[0]) {
            seats.add(leaves.peek()[1]);
            leaves.poll();
        }
        int seat = 0;
        if (seats.isEmpty()){
            seat = cnt;
            cnt++;
        } else {
            seat = seats.poll();
        }
        leaves.add(new int[]{time[1], seat});
        if (time[2] == targetFriend) {
            ans = seat;
            break;
        }
    }
    return ans;
}
```

# T3: Describe the Painting
提供一个涂色序列[a,b) c即[a,b)区间范围内涂c个颜色的信息，问提供最终区间的涂法。

区间统计，排序进行统计即可。
```java
public List<List<Long>> splitPainting(int[][] segments) {
    List<List<Long>> ans = new ArrayList<>();
    List<int[]> segList = new ArrayList<>();
    for(int[] segment : segments) {
        segList.add(new int[]{segment[0], segment[2]});
        segList.add(new int[]{segment[1], -segment[2]});
    }
    segList.sort((a, b) -> (a[0] - b[0]));
    long st = 0;
    long cnt = 0;
    int idx = 0;
    while(idx < segList.size()) {
        long pos = segList.get(idx)[0];
        long oldCnt = cnt;
        while(idx < segList.size() && pos == segList.get(idx)[0]) {
            cnt += segList.get(idx)[1];
            idx++;
        }
        if ((oldCnt != 0)&&(oldCnt>0)) {
            ans.add(List.of(st, pos, oldCnt));
        }
        st = pos;
    }
    return ans;
}
```

# T4: Number of Visible People in a Queue
给定一个队列Heights，问每个位置I，之后有多少个J满足: min(Heights[i], Heights[j]) > max(Heights[i+1], ... Heights[j-1])

见代码，直接一个堆栈进行统计即可:
```java
public int[] canSeePersonsCount(int[] heights) {
    Stack<Integer> list = new Stack<>();
    int n = heights.length;
    int[] ans = new int[n];
    for(int idx=n-1;idx>=0;idx--) {
        ans[idx] = 0;
        while (list.size()>0 && list.peek() < heights[idx]) {
            ans[idx]++;
            list.pop();
        }
        ans[idx] += list.size()==0 ? 0 : 1;
        list.add(heights[idx]);
    }
    return ans;
}
```
