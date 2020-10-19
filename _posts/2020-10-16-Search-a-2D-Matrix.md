---
layout: post
title:  "[LeetCode October Challange] Day 16 - Search a 2D Matrix"
date:   2020-10-16 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Array, Binary Search, Amazon, Microsoft, Facebook, Bloomberg, Adobe]
---
Write an efficient algorithm that searches for a value in an <font color="red">m x n</font> matrix. This matrix has the following properties:  

- Integers in each row are sorted from left to right.
- The first integer of each row is greater than the last integer of the previous row.

# Example 1:  
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/74_ex1.jpg?raw=true)

	Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,50]], target = 3
	Output: true

# Example 2:  
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/74_ex2.jpg?raw=true)

	Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,50]], target = 13
	Output: false

# Example 3:  
	Input: matrix = [], target = 0
	Output: false

# Constraints:  
- <font color="red">m == matrix.length</font>
- <font color="red">n == matrix[i].length</font>
- <font color="red">0 <= m, n <= 100</font>
- <font color="red">-104 <= matrix[i][j], target <= 104</font>

______________________  

# Solution

Time complexity : O(log(mn))  
Space complexity : O(1)  

	class Solution {
	public:
	    bool searchMatrix(vector<vector<int>>& matrix, int target) {
	        int m = matrix.size();
	        if (0 == m) return false;
	        int n = matrix[0].size();
	        if (0 == n) return false;
	        
	        int len = m * n;
	        int l = 0, r = len - 1;
	        while (l < r) {
	            int mid = (l+r)>>1;
	            int val = matrix[mid/n][mid%n];
	            if (val == target)
	                return true;
	            else if (target < val)
	                r = mid;
	            else l = mid + 1;
	        }
	        return matrix[l/n][l%n] == target;
	    }
	};

因上一列最後一個元素<此列第一個元素，因此整個2D matrix可視為1D sorted array。  

用Binary Search，求出結果。  

要注意其中座標位置的轉換。