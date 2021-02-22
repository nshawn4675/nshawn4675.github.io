---
layout: post
title:  "[LeetCode February Challange] Day 15 - The K Weakest Rows in a Matrix"
date:   2021-02-15 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Easy, Array, Binary Search, Amazon]
---
You are given an <font color="red">m x n</font> binary matrix <font color="red">mat</font> of <font color="red">1</font>'s (representing soldiers) and <font color="red">0</font>'s (representing civilians). The soldiers are positioned **in front** of the civilians. That is, all the <font color="red">1</font>'s will appear to the **left** of all the <font color="red">0</font>'s in each row.

A row <font color="red">i</font> is **weaker** than a row <font color="red">j</font> if one of the following is true:

- The number of soldiers in row <font color="red">i</font> is less than the number of soldiers in row <font color="red">j</font>.
- Both rows have the same number of soldiers and <font color="red">i < j</font>.

Return *the indices of the* <font color="red">k</font> **weakest** *rows in the matrix ordered from weakest to strongest*.

# Example 1:

	Input: mat = 
	[[1,1,0,0,0],
	 [1,1,1,1,0],
	 [1,0,0,0,0],
	 [1,1,0,0,0],
	 [1,1,1,1,1]], 
	k = 3
	Output: [2,0,3]
	Explanation: 
	The number of soldiers in each row is: 
	- Row 0: 2 
	- Row 1: 4 
	- Row 2: 1 
	- Row 3: 2 
	- Row 4: 5 
	The rows ordered from weakest to strongest are [2,0,3,1,4].

# Example 2:

	Input: mat = 
	[[1,0,0,0],
	 [1,1,1,1],
	 [1,0,0,0],
	 [1,0,0,0]], 
	k = 2
	Output: [0,2]
	Explanation: 
	The number of soldiers in each row is: 
	- Row 0: 1 
	- Row 1: 4 
	- Row 2: 1 
	- Row 3: 1 
	The rows ordered from weakest to strongest are [0,2,3,1].

# Constraints:

- <font color="red">m == mat.length</font>
- <font color="red">n == mat[i].length</font>
- <font color="red">2 <= n, m <= 100</font>
- <font color="red">1 <= k <= m</font>
- **<font color="red">matrix[i][j]</font>** is either 0 or 1.

______________________  

# Solution  

Time complexity : O(mn)  
Space complexity : O(m)  

	class Solution {
	public:
	    vector<int> kWeakestRows(vector<vector<int>>& mat, int k) {
	        const int m = mat.size();
	        const int n = mat[0].size();
	        
	        unordered_map<int, vector<int>> ht;
	        for (int i=0; i<m; ++i) {
	            int cnt = accumulate(mat[i].begin(), mat[i].end(), 0);
	            ht[cnt].push_back(i);
	        }
	        
	        vector<int> ans;
	        for (int i=0; i<=n; ++i) {
	            if (ht.count(i) == 0) continue;
	            for (int r: ht[i]) {
	                if (k <= 0) break;
	                ans.push_back(r);
	                --k;
	            }
	        }
	        return ans;
	    }
	};

先用 hash table 將相對應的「累積值」 -> row 記錄起來。  
再從累積值小的到大的 row 取 k 個。