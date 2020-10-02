---
layout: post
title:  "[LeetCode October Challange] Day 2 - Combination Sum"
date:   2020-10-02 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Array, Backtracking, Amazon, Facebook, eBay, Uber, Microsoft, Apple]
---
Given an array of **distinct** integers <font color="red">candidates</font> and a <font color="red">target</font> integer target, return *a list of all **unique combinations** of <font color="red">candidates</font> where the chosen numbers sum to* <font color="red">target</font>. You may return the combinations in **any order**.  

The **same** number may be chosen from <font color="red">candidates</font> an **unlimited number of times**. Two combinations are unique if the frequency of at least one of the chosen numbers is different.  

# Example 1:  
	Input: candidates = [2,3,6,7], target = 7
	Output: [[2,2,3],[7]]
	Explanation:
	2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
	7 is a candidate, and 7 = 7.
	These are the only two combinations.

# Example 2:  
	Input: candidates = [2,3,5], target = 8
	Output: [[2,2,2,2],[2,3,3],[3,5]]

# Example 3:  
	Input: candidates = [2], target = 1
	Output: []

# Example 4:  
	Input: candidates = [1], target = 1
	Output: [[1]]

# Example 5:  
	Input: candidates = [1], target = 2
	Output: [[1,1]]

# Constraints:  
- <font color="red">1 <= candidates.length <= 30</font>
- <font color="red">1 <= candidates[i] <= 200</font>
- All elements of <font color="red">candidates</font> are **distinct**.
- <font color="red">1 <= target <= 500</font>

______________________  

# Solution

Time complexity : O(nlog(n))  
Space complexity : O(n)  

	class Solution {
	public:
	    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
	        sort(candidates.begin(), candidates.end());
	        helper(candidates, {}, 0, target);
	        return ans;
	    }
	private:
	    vector<vector<int>> ans;
	    void helper(vector<int>& candidates, vector<int> cur, int start, int target) {
	        if (0 == target) {
	            ans.push_back(cur);
	            return;
	        }
	        for (int i=start; i<candidates.size(); ++i) {
	            int n = candidates[i];
	            if (n > target) break;
	            cur.push_back(n);
	            helper(candidates, cur, i, target-n);
	            cur.pop_back();
	        }
	    }
	};

sort完之後確定為小→大。  
用backtracking的方式，得到加總為target的組合。