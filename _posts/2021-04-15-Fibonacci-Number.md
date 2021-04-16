---
layout: post
title:  "[LeetCode April Challange] Day 15 - Fibonacci Number"
date:   2021-04-15 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Easy, JPMorgan, Amazon, Google, Apple, Facebook]
---
The **Fibonacci numbers**, commonly denoted <font color="red">F(n)</font> form a sequence, called the **Fibonacci sequence**, such that each number is the sum of the two preceding ones, starting from <font color="red">0</font> and <font color="red">1</font>. That is,

    F(0) = 0, F(1) = 1
    F(n) = F(n - 1) + F(n - 2), for n > 1.

Given <font color="red">n</font>, calculate <font color="red">F(n)</font>.

# Example 1:

    Input: n = 2
    Output: 1
    Explanation: F(2) = F(1) + F(0) = 1 + 0 = 1.

# Example 2:

    Input: n = 3
    Output: 2
    Explanation: F(3) = F(2) + F(1) = 1 + 1 = 2.

# Example 3:

    Input: n = 4
    Output: 3
    Explanation: F(4) = F(3) + F(2) = 2 + 1 = 3.
 

# Constraints:

- <font color="red">0 <= n <= 30</font>

______________________  

# Solution  

# Recursion  

Time complexity : O(2^n)  
Space complexity : O(n)  

    class Solution {
    public:
        int fib(int n) {
            if (n < 2) return n;
            return fib(n-2) + fib(n-1);
        }
    };

# Dynamic Programming  

Time complexity : O(n)  
Space complexity : O(n)  

    class Solution {
    public:
        int fib(int n) {
            vector<int> dp(n+2, 0);
            dp[0] = 0;
            dp[1] = 1;
            for (int i=2; i<=n; ++i)
                dp[i] = dp[i-2]+dp[i-1];
            return dp[n];
        }
    };

# Iterative  

Time complexity : O(n)  
Space complexity : O(1)  

    class Solution {
    public:
        int fib(int n) {
            if (n < 2) return n;
            int prev = 0;
            int curr = 1;
            while (1<n--) {
                int next = prev + curr;
                prev = curr;
                curr = next;
            }
            return curr;
        }
    };