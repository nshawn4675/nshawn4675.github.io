---
layout: post
title:  "[LeetCode February Challange] Day 13 - Shortest Path in Binary Matrix"
date:   2021-02-13 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Breadth-first Search, Amazon, Google, Facebook, Oracle, Snapchat, Paypal]
---
In an N by N square grid, each cell is either empty (0) or blocked (1).

A *clear path from top-left to bottom-right* has length <font color="red">k</font> if and only if it is composed of cells <font color="red">C_1, C_2, ..., C_k</font> such that:

- Adjacent cells <font color="red">C_i</font> and <font color="red">C_{i+1}</font> are connected 8-directionally (ie., they are different and share an edge or corner)
- **<font color="red">C_1</font>** is at location <font color="red">(0, 0)</font> (ie. has value <font color="red">grid[0][0]</font>)
- **<font color="red">C_k</font>** is at location <font color="red">(N-1, N-1)</font> (ie. has value <font color="red">grid[N-1][N-1]</font>)
- If <font color="red">C_i</font> is located at <font color="red">(r, c)</font>, then <font color="red">grid[r][c]</font> is empty (ie. <font color="red">grid[r][c] == 0</font>).

Return the length of the shortest such clear path from top-left to bottom-right.  If such a path does not exist, return -1.

# Example 1:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/1091_ex1_in.png?raw=true)
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/1091_ex1_out.png?raw=true)

	Input: [[0,1],[1,0]]
	Output: 2

# Example 2:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/1091_ex2_in.png?raw=true)
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/1091_ex2_out.png?raw=true)

	Input: [[0,0,0],[1,1,0],[1,1,0]]
	Output: 4

# Note:

1. <font color="red">1 <= grid.length == grid[0].length <= 100</font>
2. <font color="red">grid[r][c] is 0 or 1</font>

______________________  

# Solution  

### BFS

Time complexity : O(rc)  
Space complexity : O(1)  

	class Solution {
	public:
	    int shortestPathBinaryMatrix(vector<vector<int>>& grid) {
	        const int rows = grid.size(), cols = grid[0].size();
	        if (grid[0][0] != 0 || grid[rows-1][cols-1] != 0) return -1;
	        vector<pair<int, int>> q;
	        
	        q.push_back({0, 0});
	        int step = 0;
	        
	        while (!q.empty() && grid[rows-1][cols-1] <= 0) {
	            ++step;
	            
	            // mark
	            for (auto xy: q) {
	                grid[xy.second][xy.first] = step;
	            }
	            
	            // get next breadth
	            vector<pair<int, int>> next_q;
	            for (auto xy: q) {
	                for (int dx = -1; dx <= 1; ++dx) {
	                    for (int dy = -1; dy <= 1; ++dy) {
	                        int x = xy.first+dx, y = xy.second+dy;
	                        if (x<0 || cols<=x || y<0 || rows<=y)
	                            continue;
	                        if (grid[y][x] == 0) {
	                            next_q.push_back({x, y});
	                            grid[y][x] = -1;
	                        }
	                    }
	                }
	            }
	            q = next_q;
	        }
	        return grid[rows-1][cols-1] == 0 ? -1 : grid[rows-1][cols-1];
	    }
	};

用 BFS 的方式，從左上走到右下。  

每走一步 step 就加 1，並在腳下那塊記錄目前的 step。  
再根據目前這一步走了哪些塊，尋找下一步要往哪走，往 0 的方向走，並標記 -1 ，代表該塊已記錄到下一步中。