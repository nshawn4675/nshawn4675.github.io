---
layout: post
title:  "Largest Unique Number"
date:   2021-04-07 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Easy, Array, Hash Table, Amazon]
---
Given an array of integers <font color="red">A</font>, return the largest integer that only occurs once.

If no integer occurs once, return -1.

# Example 1:

    Input: [5,7,3,9,4,9,8,3,1]
    Output: 8
    Explanation: 
    The maximum integer in the array is 9 but it is repeated. The number 8 occurs only once, so it's the answer.

# Example 2:

    Input: [9,9,8,8]
    Output: -1
    Explanation: 
    There is no number that occurs only once.

# Note:

1. <font color="red">1 <= A.length <= 2000</font>
2. <font color="red">0 <= A[i] <= 1000</font>

______________________  

# Solution  

# Sorting

Time complexity : O(nlogn)  
Space complexity : O(1)  

    class Solution {
    public:
        int largestUniqueNumber(vector<int>& A) {
            const int N = size(A);
            A.push_back(INT_MAX);
            A.push_back(INT_MIN);
            sort(rbegin(A), rend(A));
            for (int i=1; i<=N; ++i) {
                if (A[i-1] != A[i] && A[i] != A[i+1])
                    return A[i];
            }
            return -1;
        }
    };

# Hash Table

Time complexity : O(n)  
Space complexity : O(1)  

    class Solution {
    public:
        int largestUniqueNumber(vector<int>& A) {
            unordered_map<int, int> m;
            for (int &n: A) m[n]++;
            int ans = -1;
            for (auto &[key, val]: m) {
                if (val == 1)
                    ans = max(ans, key);
            }
            return ans;
        }
    };