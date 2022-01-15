---
layout: post
title: "750. Number Of Corner Rectangles"
date: 2021-01-31 00:00:00 +0800
categories: LeetCode
tags: [Medium, Dynamic Programming, Facebook, C++]
---
Given a grid where each entry is only 0 or 1, find the number of corner rectangles.

A *corner rectangle* is 4 distinct 1s on the grid that form an axis-aligned rectangle. Note that only the corners need to have the value 1. Also, all four 1s used must be distinct.

# Example 1:

	Input: grid = 
	[[1, 0, 0, 1, 0],
	 [0, 0, 1, 0, 1],
	 [0, 0, 0, 1, 0],
	 [1, 0, 1, 0, 1]]
	Output: 1
	Explanation: There is only one corner rectangle, with corners grid[1][2], grid[1][4], grid[3][2], grid[3][4].

# Example 2:

	Input: grid = 
	[[1, 1, 1],
	 [1, 1, 1],
	 [1, 1, 1]]
	Output: 9
	Explanation: There are four 2x2 rectangles, four 2x3 and 3x2 rectangles, and one 3x3 rectangle.

# Example 3:

	Input: grid = 
	[[1, 1, 1, 1]]
	Output: 0
	Explanation: Rectangles must have four distinct corners.

# Note:

1. The number of rows and columns of <font color="red">grid</font> will each be in the range <font color="red">[1, 200]</font>.
2. Each <font color="red">grid[i][j]</font> will be either <font color="red">0</font> or <font color="red">1</font>.
3. The number of <font color="red">1</font>s in the grid will be at most <font color="red">6000</font>.

______________________  

# Solution  

Time complexity : O(R^2 * C)  
Space complexity : O(R * C)  

	class Solution {
	public:
	    int countCornerRectangles(vector<vector<int>>& grid) {
	        const int row = grid.size();
	        const int col = grid[0].size();
	        vector<bitset<200>> m(row);
	        
	        for (int r=0; r<row; ++r) {
	            for (int c=0; c<col; ++c) {
	                if (grid[r][c]) m[r].set(c);
	            }
	        }
	        
	        int ans = 0;
	        for (int r=1; r<row; ++r) {
	            for (int k=0; k<r; ++k) {
	                int count = (m[r] & m[k]).count();
	                if (count < 2) continue;
	                ans += count*(count-1)/2 * 2*1/2;
	            }
	        }
	        return ans;
	    }
	};

將原 vector 轉為 bitset 方便處理。  
接著針對每一列，檢察到其為止的列是否能形成矩形。  

若 2 列相 and ，有 1 代表有共同的行，其值為 1。
至少需要 2 個共同的行，其值為 1 ，才可形成矩形。

接著是給定網格，計算有多少矩形的問題。  
一個矩形的組成為 2 垂直線 + 2 水平線，故垂直線與水平線各取 2。  
此處為 row = 1 ，col = count-1 (因是用count當做點)  
col 的組合方式共有：((count-1)+1) * (count-1) / 2 * 1  
row 的組合方式共有：(1+1) * 1 / 2 * 1  

整體的組合方式 = col 的組合方式 * row 的組合方式。