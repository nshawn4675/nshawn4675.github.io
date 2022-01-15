---
layout: post
title: "[LeetCode April Challange] Day 12 - Beautiful Arrangement II"
date: 2021-04-12 00:00:00 +0800
categories: LeetCode
tags: [Medium, Array, Math, Google, C++]
---
Given two integers <font color="red">n</font> and <font color="red">k</font>, you need to construct a list which contains <font color="red">n</font> different positive integers ranging from <font color="red">1</font> to <font color="red">n</font> and obeys the following requirement:
Suppose this list is [a1, a2, a3, ... , an], then the list [|a1 - a2|, |a2 - a3|, |a3 - a4|, ... , |an-1 - an|] has exactly <font color="red">k</font> distinct integers.

If there are multiple answers, print any of them.

# Example 1:

    Input: n = 3, k = 1
    Output: [1, 2, 3]
    Explanation: The [1, 2, 3] has three different positive integers ranging from 1 to 3, and the [1, 1] has exactly 1 distinct integer: 1.

# Example 2:

    Input: n = 3, k = 2
    Output: [1, 3, 2]
    Explanation: The [1, 3, 2] has three different positive integers ranging from 1 to 3, and the [2, 1] has exactly 2 distinct integers: 1 and 2.

# Note:
The <font color="red">n</font> and <font color="red">k</font> are in the range 1 <= k < n <= 10^4.

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(n)  

    class Solution {
    public:
        vector<int> constructArray(int n, int k) {
            vector<int> ans;
            int i = 1, j = n;
            while (i<=j) {
                if (1 < k)
                    ans.push_back((k--)%2 ? i++ : j--);
                else
                    ans.push_back(i++);
            }
            return ans;
        }
    };

k = 1 : 1, 2, 3, 4, 5  
k = 2 : 5, 1, 2, 3, 4  
k = 3 : 1, 5, 2, 3, 4  
k = 4 : 1, 5, 2, 4, 3

若 k 只剩 1，直接照順序放。  
若 k 大於 1，且為偶，先放最大數。  
若 k 大於 1，且為奇，先放最小數。