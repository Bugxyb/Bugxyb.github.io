---
layout: post
title: LeetCode Constest 249
categories: LeetCode
---
纪念第一次状态爆棚，进入前15（基本上每道题看一眼就会做，而且还睡过了3min）

# T1: Concatenation of Array
没什么可以说的，For循环一遍即可

# T2: Unique Length-3 Palindromic Subsequences
已经规定要长度为3的回文串，所以只需要枚举中间一个的位置，看前面和后面是否由相同的字符出现，然后通过Set进行去重

```java
class Solution {
    public int countPalindromicSubsequence(String s) {
        int[][] fn = new int[2][26];
        HashSet<Integer> mset = new HashSet<Integer>();
        for(char ch : s.toCharArray()){
            fn[1][ch-'a'] += 1;
        }
        for(int i=0;i<s.length();i++) {
            int now = s.charAt(i) - 'a';
            fn[1][now] -= 1;
            for(int k=0;k<26;k++) {
                if (fn[0][k] > 0 && fn[1][k]>0) {
                    int key = now * 100 + k;
                    mset.add(key);
                }
            }
            fn[0][now] += 1;
        }
        return mset.size();
    }
}
```

# T3: Painting a Grid With Tree Different Colors
染色问题，因为m最大为5，所以直接使用状态压缩DP即可，然后进行统计。
注意可以提前预处理下，当前一列以及相邻两列是否合法的，时间复杂度是O(3^2m*n);

# T4: Merge BSTs to Create Single BST
将一个最大结点数为3的BST森林合并乘一颗BST，处理流程很简单：
* 最终根结点不会出现在BST的叶子结点上
* 遍历叶子结点是否为一颗BST的根，如果是则合并，可以使用Map来进行索引。
* 可以先合并为Tree，然后再进行BST的判断

```java
    private static final int MAXN = 50010;

    private HashMap<Integer, TreeNode> treeMap;

    private TreeNode buildTree(TreeNode root) {
        if(root.left != null) {
            int key = root.left.val;
            if (treeMap.containsKey(key)) {
                root.left = treeMap.get(key);
                treeMap.remove(key);
                buildTree(root.left);
            }
        }
        if (root.right != null) {
            int key = root.right.val;
            if (treeMap.containsKey(key)) {
                root.right = treeMap.get(key);
                treeMap.remove(key);
                buildTree(root.right);
            }
        }
        return root;
    }

    private boolean checkBST(TreeNode root, int st, int en) {
        if ((root.val<=st) || (root.val>=en)) {
            return false;
        }
        if (root.left != null) {
            if (! checkBST(root.left, st, root.val)) {
                return false;
            }
        }
        if (root.right != null) {
            if (! checkBST(root.right, root.val, en)) {
                return false;
            }
        }
        return true;
    }

    public TreeNode canMerge(List<TreeNode> trees) {
        int[] fLeaf = new int[MAXN];
        treeMap = new HashMap<>();
        for(TreeNode tree : trees) {
            treeMap.put(tree.val, tree);
            if (tree.left != null){
                fLeaf[tree.left.val] += 1;
            }
            if (tree.right != null) {
                fLeaf[tree.right.val] += 1;
            }
        }
        TreeNode root = null;
        for(TreeNode tree : trees) {
            if (fLeaf[tree.val] == 0) {
                if (root != null) {
                    return null;
                }
                root = tree;

            }
        }
        if (root == null) {
            return null;
        }
        treeMap.remove(root.val);
        root = buildTree(root);
        if (!treeMap.isEmpty()) {
            return null;
        }
        return checkBST(root, 0, MAXN) ? root : null;
    }
```
