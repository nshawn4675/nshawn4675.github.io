---
layout: post
title:  "[LeetCode September Challange]Day12-Combination Sum III"
date:   2020-09-12 00:00:00 +0800
categories: LeetCode
tags: [Medium, Array, Backtracking, C++]
---
Find all possible combinations of **k** numbers that add up to a number **n**, given that only numbers from 1 to 9 can be used and each combination should be a unique set of numbers.  

# Note:  
- All numbers will be positive integers.
- The solution set must not contain duplicate combinations.

# Example 1:  
	Input: k = 3, n = 7
	Output: [[1,2,4]]

# Example 2:  
	Input: k = 3, n = 9
	Output: [[1,2,6], [1,3,5], [2,3,4]]

______________________  

# Solution

## dfs + backtracking

Time complexity : O(C(9, k))  
Space complexity : O(k^2)

	class Solution {
	public:
	    vector<vector<int>> combinationSum3(int k, int n) {
	        vector<vector<int>> res;
	        dfs(res, {}, 1, k, n);
	        return res;
	    }
	private:
	    void dfs(vector<vector<int>>& res, vector<int> vec, int idx, int k, int n) {
	        if (k==0) {
	            if (n==0) res.push_back(vec);
	            return;
	        }
	        for (int i=idx; i<=9; ++i) {
	            if (i>n) return ;
	            vec.push_back(i);
	            dfs(res, vec, i+1, k-1, n-i);
	            vec.pop_back();
	        }
	    }
	};

從1開始往9找。

## bit

Time complexity : O(2^9)  
Space complexity : O(k^2)

	class Solution {
	public:
	    vector<vector<int>> combinationSum3(int k, int n) {
	        vector<vector<int>> res;
	        
	        for (int i=0; i<(1<<9); ++i) {
	            if (__builtin_popcount(i) != k) continue;
	            
	            vector<int> vec;
	            int sum = 0;
	            for (int j=1; j<=9; ++j) {
	                if (i & 1<<(j-1)) {
	                    vec.push_back(j);
	                    sum += j;
	                }
	            }
	            if (sum == n)
	                res.push_back(vec);
	        }
	        
	        return res;
	    }
	};

從1開始計數，用2進位的方式來看待計數，1代表選中的字。  
若選中的數量不等於目標數(k)，則跳過。  

尋找選了哪些數字，加總起來是否等於目標(n)？是的話將此組合加入答案中。