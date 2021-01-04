---
layout: post
title:  "[LeetCode January Challange] Day 3 - Beautiful Arrangement"
date:   2021-01-03 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Backtracking, Depth-first Search, Mathworks, Cisco]
---
Suppose you have <font color="red">n</font> integers labeled <font color="red">1</font> through <font color="red">n</font>. A permutation of those <font color="red">n</font> integers <font color="red">perm</font> (**1-indexed**) is considered a **beautiful arrangement** if for every <font color="red">i</font> (<font color="red">1 <= i <= n</font>), **either** of the following is true:

- **<font color="red">perm[i]</font>** is divisible by <font color="red">i</font>.
- **<font color="red">i</font>** is divisible by <font color="red">perm[i]</font>.

Given an integer <font color="red">n</font>, return *the **number** of the **beautiful arrangements** that you can construct*.

# Example 1:

	Input: n = 2
	Output: 2
	Explanation: 
	The first beautiful arrangement is [1,2]:
	    - perm[1] = 1 is divisible by i = 1
	    - perm[2] = 2 is divisible by i = 2
	The second beautiful arrangement is [2,1]:
	    - perm[1] = 2 is divisible by i = 1
	    - i = 2 is divisible by perm[2] = 1

# Example 2:

	Input: n = 1
	Output: 1

# Constraints:

- <font color="red">1 <= n <= 15</font>

______________________  

# Solution  

Time complexity : O(k) # k perms  
Space complexity : O(n)  

	class Solution {
	public:
	    int countArrangement(int n) {
	        count = 0;
	        vector<bool> visited(n+1, false);
	        
	        backtracking(n, 1, visited);
	            
	        return count;
	    }
	    
	    void backtracking(int n, int pos, vector<bool> &visited) {
	        if (pos > n) ++count;
	        for (int i=1; i<=n; ++i) {
	            if (!visited[i] && (i % pos == 0 || pos % i == 0)) {
	                visited[i] = true;
	                backtracking(n, pos+1, visited);
	                visited[i] = false;
	            }
	        }
	    }
	    
	private:
	    int count;
	};

利用 visited 做 backtracking ，要放新數字時做檢查，若已不合所需，則代表它為根之後的 perm 都是錯的，不用再往下做，直接跳下一個，避免不需要的計算。