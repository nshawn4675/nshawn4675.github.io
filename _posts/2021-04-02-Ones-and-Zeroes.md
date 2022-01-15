---
layout: post
title: "[LeetCode April Challange] Day 02 - Ones and Zeroes"
date: 2021-04-02 00:00:00 +0800
categories: LeetCode
tags: [Medium, Array, String, Dynamic Programming, Google, C++]
---
You are given an array of binary strings <font color="red">strs</font> and two integers <font color="red">m</font> and <font color="red">n</font>.

Return *the size of the largest subset of <font color="red">strs</font> such that there are **at most** <font color="red">m 0's</font> and <font color="red">n 1's</font> in the subset.*

A set <font color="red">x</font> is a **subset** of a set <font color="red">y</font> if all elements of <font color="red">x</font> are also elements of <font color="red">y</font>.

# Example 1:

    Input: strs = ["10","0001","111001","1","0"], m = 5, n = 3
    Output: 4
    Explanation: The largest subset with at most 5 0's and 3 1's is {"10", "0001", "1", "0"}, so the answer is 4.
    Other valid but smaller subsets include {"0001", "1"} and {"10", "1", "0"}.
    {"111001"} is an invalid subset because it contains 4 1's, greater than the maximum of 3.

# Example 2:

    Input: strs = ["10","0","1"], m = 1, n = 1
    Output: 2
    Explanation: The largest subset is {"0", "1"}, so the answer is 2.

# Constraints:

- <font color="red">1 <= strs.length <= 600</font>
- <font color="red">1 <= strs[i].length <= 100</font>
- **<font color="red">strs[i]</font>** consists only of digits <font color="red">'0'</font> and <font color="red">'1'</font>.
- <font color="red">1 <= m, n <= 100</font>

______________________  

# Solution  

# Top-Down DP  

Time complexity : O(l\*m\*n) (l : size(strs))  
Space complexity : O(l\*m\*n)  

    class Solution {
    public:
        int findMaxForm(vector<string>& strs, int m, int n) {
            dp_.resize(size(strs), vector<vector<int>>(m+1, vector<int>(n+1)));
            return helper(strs, m, n, 0);
        }
    private:
        vector<vector<vector<int>>> dp_;
        int helper(vector<string>& strs, int m, int n, int i) {
            if (i == size(strs) || m+n == 0) return 0;
            if (dp_[i][m][n]) return dp_[i][m][n];
            
            int zeros = count(begin(strs[i]), end(strs[i]), '0');
            int ones = size(strs[i]) - zeros;
            
            dp_[i][m][n] = helper(strs, m, n, i+1);
            if (zeros <= m && ones <= n)
                dp_[i][m][n] = max(dp_[i][m][n], 1+helper(strs, m-zeros, n-ones, i+1));
            
            return dp_[i][m][n];
        }
    };

# Bottom-Up DP

Time complexity : O(m\*n)  
Space complexity : O(m\*n)  

    class Solution {
    public:
        int findMaxForm(vector<string>& strs, int m, int n) {
            vector<vector<int>> dp(m+1, vector<int>(n+1));
            for (string s: strs) {
                int zeros = count(begin(s), end(s), '0');
                int ones = size(s) - zeros;
                for (int i=m; zeros<=i; --i) {
                    for (int j=n; ones<=j; --j) {
                        dp[i][j] = max(dp[i][j],
                                    1 + dp[i-zeros][j-ones]);
                    }
                }
            }
            return dp[m][n];
        }
    };