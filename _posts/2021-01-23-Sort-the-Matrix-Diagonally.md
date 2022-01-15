---
layout: post
title: "[LeetCode January Challange] Day 23 - Sort the Matrix Diagonally"
date: 2021-01-23 00:00:00 +0800
categories: LeetCode
tags: [Medium, Array, Sorting, Matrix, Facebook, Databricks, Google, Robinhood, ServiceNow, C++]
---
A **matrix diagonal** is a diagonal line of cells starting from some cell in either the topmost row or leftmost column and going in the bottom-right direction until reaching the matrix's end. For example, the **matrix diagonal** starting from <font color="red">mat[2][0]</font>, where <font color="red">mat</font> is a <font color="red">6 x 3</font> matrix, includes cells <font color="red">mat[2][0]</font>, <font color="red">mat[3][1]</font>, and <font color="red">mat[4][2]</font>.

Given an <font color="red">m x n</font> matrix mat of integers, sort each **matrix diagonal** in ascending order and return *the resulting matrix.*

# Example 1:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/1329_ex1.png?raw=true)

	Input: mat = [[3,3,1,1],[2,2,1,2],[1,1,1,2]]
	Output: [[1,1,1,1],[1,2,2,2],[1,2,3,3]]

# Constraints:

- <font color="red">m == mat.length</font>
- <font color="red">n == mat[i].length</font>
- <font color="red">1 <= m, n <= 100</font>
- <font color="red">1 <= mat[i][j] <= 100</font>

______________________  

# Solution  

# HashMap with Heaps

Time complexity : O(m x n x log(min(m, n)))  
Space complexity : O(m x n)  

	class Solution {
	public:
	    vector<vector<int>> diagonalSort(vector<vector<int>>& mat) {
	        const int rows = mat.size();
	        const int cols = mat[0].size();
	        unordered_map<int, priority_queue<int, vector<int>, greater<int>>> ht;
	        
	        for (int r=0; r<rows; ++r) {
	            for (int c=0; c<cols; ++c) {
	                ht[r-c].push(mat[r][c]);
	            }
	        }
	        
	        for (int r=0; r<rows; ++r) {
	            for (int c=0; c<cols; ++c) {
	                mat[r][c] = ht[r-c].top();
	                ht[r-c].pop();
	            }
	        }
	        
	        return mat;
	    }
	};

題目要求我們針對每一個斜線做排序。  
可觀察到每一個斜線中，座標位置相減的數值是相同的。  
因此利用 hash table 給予每一個斜線一個相對應的 min heap。  
一個一個將其對應的值塞入後，再更新回 mat。

# Sort Diagonals One by One Using Heap

Time complexity : O(m x n x log(min(m, n)))  
Space complexity : O(min(m, n))  

	class Solution {
	public:
	    vector<vector<int>> diagonalSort(vector<vector<int>>& mat) {
	        const int rows = mat.size();
	        const int cols = mat[0].size();
	        
	        for (int r=0; r<rows; ++r) {
	            sortDiag(r, 0, min(rows-r, cols-0), mat);
	        }
	        
	        for (int c=1; c<cols; ++c) {
	            sortDiag(0, c, min(rows-0, cols-c), mat);
	        }
	        
	        return mat;
	    }
	private:
	    void sortDiag(int r, int c, int len, vector<vector<int>>& mat) {
	        priority_queue<int, vector<int>, greater<int>> min_heap;
	        for (int l=0; l<len; ++l) {
	            min_heap.push(mat[r+l][c+l]);
	        }
	        for (int l=0; l<len; ++l) {
	            mat[r+l][c+l] = min_heap.top();
	            min_heap.pop();
	        }
	    }
	};

針對每一條斜線，進去做 sort ，可以節省很多ram。