---
layout: post
title:  "[LeetCode February Challange] Day 20 - Search a 2D Matrix II"
date:   2021-02-20 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Binary Search, Divide and Conquer, Amazon, Microsoft, ByteDance, Bloomberg, Facebook, Nvidia]
---
Write an efficient algorithm that searches for a <font color="red">target</font> value in an <font color="red">m x n</font> integer <font color="red">matrix</font>. The <font color="red">matrix</font> has the following properties:

- Integers in each row are sorted in ascending from left to right.
- Integers in each column are sorted in ascending from top to bottom.

# Example 1:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/240_ex1.jpg?raw=true)

	Input: matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 5
	Output: true

# Example 2:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/240_ex2.jpg?raw=true)

	Input: matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 20
	Output: false

# Constraints:

- <font color="red">m == matrix.length</font>
- <font color="red">n == matrix[i].length</font>
- <font color="red">1 <= n, m <= 300</font>
- <font color="red">-10^9 <= matix[i][j] <= 10^9</font>
- All the integers in each row are **sorted** in ascending order.
- All the integers in each column are **sorted** in ascending order.
- <font color="red">-10^9 <= target <= 10^9</font>

______________________  

# Solution  

Time complexity : O(m+n)  
Space complexity : O(1)  

	class Solution {
	public:
	    bool searchMatrix(vector<vector<int>>& matrix, int target) {
	        const int rows = matrix.size(), cols = matrix[0].size();
	        int r = 0, c = cols-1;
	        while (r < rows && 0 <= c) {
	            if (matrix[r][c] == target) return true;
	            matrix[r][c] < target ? ++r : --c;
	        }
	        return false;
	    }
	};