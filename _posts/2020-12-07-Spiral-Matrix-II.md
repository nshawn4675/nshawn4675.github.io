---
layout: post
title: "[LeetCode December Challange] Day 7 - Spiral Matrix II"
date: 2020-12-07 00:00:00 +0800
categories: LeetCode
tags: [Medium, Array, Simulation, Microsoft, C++]
---
Given a positive integer <font color="red">n</font>, generate an <font color="red">n x n matrix</font> filled with elements from <font color="red">1</font> to <font color="red">n^2</font> in spiral order.

# Example 1:
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/59_ex1.jpg?raw=true)

	Input: n = 3
	Output: [[1,2,3],[8,9,4],[7,6,5]]

# Example 2:

	Input: n = 1
	Output: [[1]]

# Constraints:

- <font color="red">1 <= n <= 20</font>

______________________  

# Solution  

Time complexity : O(n^2)  
Space complexity : O(1)  

	class Solution {
	public:
	    vector<vector<int>> generateMatrix(int n) {
	        vector<int> dx = {1, 0, -1, 0}; // r, d, l, u
	        vector<int> dy = {0, 1, 0, -1};
	        vector<vector<int>> s_m = vector(n, vector(n, 0));
	        int direction = 0;
	        int x = 0, y = 0;
	        int step = 0;
	        
	        while (++step <= n*n) {
	            s_m[y][x] = step;
	            
	            int next_x = x+dx[direction];
	            int next_y = y+dy[direction];
	            if (next_x < 0 || n <= next_x || 
	                next_y < 0 || n <= next_y ||
	                s_m[next_y][next_x] != 0)
	            {
	                ++direction %= 4;
	            }
	            
	            x += dx[direction]; y += dy[direction];
	        }
	        
	        return s_m;
	    }
	};