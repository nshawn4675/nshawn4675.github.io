---
layout: post
title:  "[LeetCode September Challange]Day20-Unique Paths III"
date:   2020-09-20 00:00:00 +0800
categories: LeetCode
tags: [Hard, Array, Backtracking, Bit Manipulation, Matrix, C++]
---
On a 2-dimensional <font color="red">grid</font>, there are 4 types of squares:  

- **<font color="red">1</font>** represents the starting square.  There is exactly one starting square.
- **<font color="red">2</font>** represents the ending square.  There is exactly one ending square.
- **<font color="red">0</font>** represents empty squares we can walk over.
- **<font color="red">-1</font>** represents obstacles that we cannot walk over.

Return the number of 4-directional walks from the starting square to the ending square, that **walk over every non-obstacle square exactly once**.  

# Example 1:  
	Input: [[1,0,0,0],[0,0,0,0],[0,0,2,-1]]
	Output: 2
	Explanation: We have the following two paths: 
	1. (0,0),(0,1),(0,2),(0,3),(1,3),(1,2),(1,1),(1,0),(2,0),(2,1),(2,2)
	2. (0,0),(1,0),(2,0),(2,1),(1,1),(0,1),(0,2),(0,3),(1,3),(1,2),(2,2)

# Example 2:  
	Input: [[1,0,0,0],[0,0,0,0],[0,0,0,2]]
	Output: 4
	Explanation: We have the following four paths: 
	1. (0,0),(0,1),(0,2),(0,3),(1,3),(1,2),(1,1),(1,0),(2,0),(2,1),(2,2),(2,3)
	2. (0,0),(0,1),(1,1),(1,0),(2,0),(2,1),(2,2),(1,2),(0,2),(0,3),(1,3),(2,3)
	3. (0,0),(1,0),(2,0),(2,1),(2,2),(1,2),(1,1),(0,1),(0,2),(0,3),(1,3),(2,3)
	4. (0,0),(1,0),(2,0),(2,1),(1,1),(0,1),(0,2),(0,3),(1,3),(1,2),(2,2),(2,3)

# Example 3:  
	Input: [[0,1],[2,0]]
	Output: 0
	Explanation: 
	There is no path that walks over every empty square exactly once.
	Note that the starting and ending square can be anywhere in the grid.

# Note:  
1. <font color="red">1 <= grid.length * grid[0].length <= 20</font>

______________________  

# Solution

Time complexity : O(4^mn)  
Space complexity : O(mn)  

	class Solution {
	public:
	    int uniquePathsIII(vector<vector<int>>& grid) {
	        int start_x = -1;
	        int start_y = -1;
	        int n = 1;
	        for (int y=0; y<grid.size(); ++y) {
	            for (int x=0; x<grid[0].size(); ++x) {
	                if (grid[y][x] == 0) ++n;
	                else if (grid[y][x] == 1) {
	                    start_x = x;
	                    start_y = y;
	                }
	            }
	        }
	        return dfs(grid, start_x, start_y, n);
	    }
	private:
	    int dfs(vector<vector<int>>& grid, int x, int y, int n) {
	        if (x<0 || x==grid[0].size() ||
	            y<0 || y==grid.size() ||
	            grid[y][x] == -1) return 0;
	        else if (grid[y][x] == 2) return n==0;
	        grid[y][x] = -1;
	        int paths = dfs(grid, x+1, y, n-1) +
	                    dfs(grid, x-1, y, n-1) +
	                    dfs(grid, x, y+1, n-1) +
	                    dfs(grid, x, y-1, n-1);
	        grid[y][x] = 0;
	        return paths;
	    }
	};

一開始找到起始位置、和空位數n，然後從起始位置開始dfs & Backtracking。  

若超出範圍、或是該值為-1(走過)，則回傳0。  
若為目的地、且剩餘空位n==0，代表走好走滿走到目的地，回傳1，反之回傳0。  

都不是的話，繼續往下走。  
將目前格設為已走過(-1)，然後四個方位都走一遍。  
走完後回復該格(0)，回傳這個位置的走法結果。  