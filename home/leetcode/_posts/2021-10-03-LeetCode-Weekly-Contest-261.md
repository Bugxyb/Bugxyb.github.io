---
layout: post
title: LeetCode Weekly Contest 261
categories: LeetCode
---
最后一题尴尬卡住（不会做）

# T1: Minimum Moves to Convert String
枚举，暴力计算即可

# T2: Find Missing Observations
先判断是否合理，然后优先填充1和6

# T3: Stone Game IX
对三取余进行统计，也就是余为0，1，2的数字集合，然后进行判断：

* 如果余1，2都为0，那么bob赢
* 如果余1，2相等，那么看0是奇数还是偶数，如果是偶数，那么alice赢
* 取余1，2最小的，如果大于0且是偶数，那么alice赢
* 去余1，2的差值，如果小于3那么bob赢
* 最后看余0如果为奇数alice赢

# T4: Smallest K-Length Subsequence With Occurences of a Letter
利用栈的方法解决，这题我不会，详细看代码
```java
    public String smallestSubsequence(String s, int k, char letter, int repetition) {
        int nLetter = 0;
        for(char ch : s.toCharArray()) {
            if (ch == letter) nLetter++;
        }
        Stack<Character> stack = new Stack<>();
        for(int i=0;i<s.length();i++) {
            char ch = s.charAt(i);
            while(!stack.isEmpty() && stack.peek() > ch && (s.length() - i + stack.size()>k) && (stack.peek()!=letter || nLetter>repetition)) {
                if (stack.pop() == letter) repetition++;
            }
            if (stack.size() < k) {
                if (ch == letter) {
                    stack.push(ch);
                    repetition--;
                } else if (k - stack.size() > repetition) {
                    stack.push(ch);
                }
            }
            if (ch == letter) nLetter--;
        }
        StringBuilder ans = new StringBuilder(stack.size());
        for(Character ch : stack) ans.append(ch);
        return ans.toString();
    }
```
