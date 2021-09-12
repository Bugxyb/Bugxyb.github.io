---
layout: post
title: LeetCode Weekly Contest 258
categories: LeetCode
---
整体难度偏简单，最后一题想太久了，应该很快可以解决的
# T1: Reverse Prefix of Word
找到第一个对应的字符，然后将前面的字符串反转即可

# T2: Number of Pairs of Interchangeable Rectangles
通过最大公约数来处理每个长方形的比例，然后用最大公约数处理后的比例来计算，
通过Map快速计算

# T3: Maximum Product of the Length of Two Palindromic Subsequences
因为长度只有12，所以通过状态压缩找出所有可行的回文串，然后判断两个回文串是否
有交集，没有求长度之积的最大数

# T4: Smallest Missing Genetic Value in Each Subtree
详细见代码，可能需要证明时间复杂度问题,
对于结点I，找到结点I所有子节点的MissValue，找出最大的MissValue，然后进行推计算新
的MissValue
```java
class Solution {
    private int[] ans;
    private int[] fn;
    private List<List<Integer>> tree;
    private int[] nums1;
    private int nodeIdx;

    private int search(int root, int rec) {
        int pos = 1;
        for(int next : tree.get(root)) {
            pos = Math.max(pos, search(next, nodeIdx));
        }
        nodeIdx++;
        fn[nums1[root]] = nodeIdx;
        while(fn[pos]!=0 && fn[pos]>rec && fn[pos]<=nodeIdx) {
            pos++;
        }
        ans[root] = pos;
        return pos;
    }

    public int[] smallestMissingValueSubtree(int[] parents, int[] nums) {
        int n = parents.length;
        this.ans = new int[n];
        this.fn = new int[100010];
        this.tree = new ArrayList<>();
        this.nums1 = nums;
        for(int idx=0;idx<n;idx++) {
            tree.add(new ArrayList<>());
        }
        for (int idx=1;idx<n;idx++) {
            tree.get(parents[idx]).add(idx);
        }
        this.nodeIdx = 0;
        search(0,0);
        return ans;
    }
}
```
