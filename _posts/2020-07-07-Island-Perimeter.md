---
layout: post
title:  "[LeetCode July Challange]Day7-Island Perimeter"
date:   2020-07-07 00:00:00 +0800
categories: jekyll update
tags: LeetCode
---
You are given a map in form of a two-dimensional integer grid where 1 represents land and 0 represents water.  

Grid cells are connected horizontally/vertically (not diagonally). The grid is completely surrounded by water, and there is exactly one island (i.e., one or more connected land cells).  

The island doesn't have "lakes" (water inside that isn't connected to the water around the island). One cell is a square with side length 1. The grid is rectangular, width and height don't exceed 100. Determine the perimeter of the island.  

# Example:  
	Input:
	[[0,1,0,0],
	 [1,1,1,0],
	 [0,1,0,0],
	 [1,1,0,0]]

	Output: 16

	Explanation: The perimeter is the 16 yellow stripes in the image below:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/island.png?raw=true)

______________________  

# solution
time complexity : O(mn)  
space complexity : O(1)  
(m : width, n : height)  

	class Solution {
	public:
	    int islandPerimeter(vector<vector<int>>& grid) {
	        int area = 0;
	        int neighbor = 0;
	        int height = grid.size();
	        int width = grid[0].size();
	        for (int i=0; i<height; ++i) {
	            for (int j=0; j<width; ++j) {
	                if (grid[i][j]) {
	                    ++area;
	                    if (j != 0) neighbor += grid[i][j-1];
	                    if (j != width-1) neighbor += grid[i][j+1];
	                    if (i != 0) neighbor += grid[i-1][j];
	                    if (i != height-1) neighbor += grid[i+1][j];
	                }
	            }
	        }
	        return area*4 - neighbor;
	    }
	};

單一土地能給予的邊界為：  
若有0個鄰居，給予4邊界。  
若有1個鄰居，給予3邊界。  
若有2個鄰居，給予2邊界。  
若有3個鄰居，給予1邊界。  
若有4個鄰居，給予0邊界。  

因此可推得單一土地能給予的邊界公式為：  
Perimeter = 4\*island - neighbors  

做法：  
一格一格的去計算，總共有幾塊土地，以及左右上下計算有幾個相鄰土地(含重覆)。  
再利用公式，即可算出此小島有多少Perimeter。  
(此算法也可用在小島有湖的情況。)