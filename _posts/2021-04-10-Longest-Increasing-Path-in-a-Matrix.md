---
layout: post
title:  "[LeetCode April Challange] Day 10 - Longest Increasing Path in a Matrix"
date:   2021-04-10 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Hard, Depth-first Search, Topological Sort, Memoization, Google, Facebook, Bloomberg, Amazon, ByteDance, DoorDash]
---
Given an <font color="red">m x n</fotn> integers <font color="red">matrix</font>, return *the length of the longest increasing path in* <font color="red">matrix</font>.

From each cell, you can either move in four directions: left, right, up, or down. You **may not** move **diagonally** or move **outside the boundary** (i.e., wrap-around is not allowed).

# Example 1:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/329_ex1.jpg?raw=true)

    Input: matrix = [[9,9,4],[6,6,8],[2,1,1]]
    Output: 4
    Explanation: The longest increasing path is [1, 2, 6, 9].

# Example 2:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/329_ex2.jpg?raw=true)

    Input: matrix = [[3,4,5],[3,2,6],[2,2,1]]
    Output: 4
    Explanation: The longest increasing path is [3, 4, 5, 6]. Moving diagonally is not allowed.

# Example 3:

    Input: matrix = [[1]]
    Output: 1

# Constraints:

- <font color="red">m == matrix.length</font>
- <font color="red">n == matrix[i].length</font>
- <font color="red">1 <= m, n <= 200</font>
- <font color="red">0 <= matrix[i][j] <= 231 - 1</font>

______________________  

# Solution  

# DFS + memoization  

Time complexity : O(mn)  
Space complexity : O(mn)  

    class Solution {
    public:
        int longestIncreasingPath(vector<vector<int>>& matrix) {
            rows = matrix.size();
            cols = matrix[0].size();
            memset(dp, 0, sizeof(dp));
            
            int ans = 0;
            for (int r=0; r<rows; ++r) {
                for (int c=0; c<cols; ++c) {
                    ans = max(ans, helper(matrix, c, r, -1));
                }
            }
            return ans;
        }
    private:
        int dp[200][200], cols, rows;
        int helper(vector<vector<int>> &m, int x, int y, int prev) {
            if (x < 0 || cols <= x || y < 0 || rows <= y || m[y][x] <= prev)
                return 0;
            if (0 != dp[y][x]) return dp[y][x];
            return dp[y][x] = 1 + max({helper(m, x+1, y, m[y][x]),
                                    helper(m, x-1, y, m[y][x]),
                                    helper(m, x, y+1, m[y][x]),
                                    helper(m, x, y-1, m[y][x])});
        }
    };