---
layout: post
title: "[LeetCode December Challange] Day 4 - The kth Factor of n"
date: 2020-12-04 00:00:00 +0800
categories: LeetCode
tags: [Medium, Math, Expedia, C++]
---

Given two positive integers <font color="red">n</font> and <font color="red">k</font>.

A factor of an integer <font color="red">n</font> is defined as an integer <font color="red">i</font> where <font color="red">n % i == 0</font>.

Consider a list of all factors of <font color="red">n</font> sorted in **ascending order**, return _the <font color="red">kth</font> factor_ in this list or return **-1** if <font color="red">n</font> has less than <font color="red">k</font> factors.

# Example 1:

    Input: n = 12, k = 3
    Output: 3
    Explanation: Factors list is [1, 2, 3, 4, 6, 12], the 3rd factor is 3.

# Example 2:

    Input: n = 7, k = 2
    Output: 7
    Explanation: Factors list is [1, 7], the 2nd factor is 7.

# Example 3:

    Input: n = 4, k = 4
    Output: -1
    Explanation: Factors list is [1, 2, 4], there is only 3 factors. We should return -1.

# Example 4:

    Input: n = 1, k = 1
    Output: 1
    Explanation: Factors list is [1], the 1st factor is 1.

# Example 5:

    Input: n = 1000, k = 3
    Output: 4
    Explanation: Factors list is [1, 2, 4, 5, 8, 10, 20, 25, 40, 50, 100, 125, 200, 250, 500, 1000].

# Constraints:

- <font color="red">1 <= k <= n <= 1000</font>

---

# Solution

Time complexity : O(n)  
Space complexity : O(1)

    class Solution {
    public:
        int kthFactor(int n, int k) {
            for (int i=1; i<=n; ++i) {
                if (n%i == 0) --k;
                if (k == 0) return i;
            }
            return -1;
        }
    };
