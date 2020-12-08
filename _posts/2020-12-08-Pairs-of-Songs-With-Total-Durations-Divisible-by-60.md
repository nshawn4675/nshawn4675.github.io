---
layout: post
title: "[LeetCode December Challange] Day 8 - Pairs of Songs With Total Durations Divisible by 60"
date: 2020-12-08 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Array, Amazon, Citrix, IBM, Paypal]
---

You are given a list of songs where the i-th song has a duration of <font color="red">time[i]</font> seconds.

Return _the number of pairs of songs for which their total duration in seconds is divisible by_ <font color="red">60</font>. Formally, we want the number of indices <font color="red">i</font>, <font color="red">j</font> such that <font color="red">i < j</font> with <font color="red">(time[i] + time[j]) % 60 == 0</font>.

# Example 1:

    Input: time = [30,20,150,100,40]
    Output: 3
    Explanation: Three pairs have a total duration divisible by 60:
    (time[0] = 30, time[2] = 150): total duration 180
    (time[1] = 20, time[3] = 100): total duration 120
    (time[1] = 20, time[4] = 40): total duration 60

# Example 2:

    Input: time = [60,60,60]
    Output: 3
    Explanation: All three pairs have a total duration of 120, which is divisible by 60.

# Constraints:

- <font color="red">1 <= time.length <= 6 \* 10^4</font>
- <font color="red">1 <= time[i] <= 500</font>

---

# Solution

Time complexity : O(n)  
Space complexity : O(60)

    class Solution {
    public:
        int numPairsDivisibleBy60(vector<int>& time) {
            int ans = 0;
            vector<int> ht(60, 0);
            for (int t: time) {
                printf("%d ", t);
                t %= 60;
                ans += ht[(60-t)%60];
                ++ht[t];
            }
            return ans;
        }
    };

直覺的暴力解法，針對每一個 pair 去判斷是否符合條件，Time complexity 為 O(n^2)，Space complexity 為 O(1)。

此解法是每檢查一個新的元素時，看它的 mod60 值，能否與之前的 mod 值互補為 60。
可以的話，則此新的元素可和它們各配成一對。
再把它放到對應的容器中。
