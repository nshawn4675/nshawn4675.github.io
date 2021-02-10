---
layout: post
title:  "[LeetCode February Challange] Day 4 - Longest Harmonious Subsequence"
date:   2021-02-04 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Easy, Hash Table, Apple, LiveRamp]
---
We define a harmonious array as an array where the difference between its maximum value and its minimum value is **exactly** <font color="red">1</font>.

Given an integer array <font color="red">nums</font>, return *the length of its longest harmonious subsequence among all its possible subsequences.*

A **subsequence** of array is a sequence that can be derived from the array by deleting some or no elements without changing the order of the remaining elements.

# Example 1:

	Input: nums = [1,3,2,2,5,2,3,7]
	Output: 5
	Explanation: The longest harmonious subsequence is [3,2,2,2,3].

# Example 2:

	Input: nums = [1,2,3,4]
	Output: 2

# Example 3:

	Input: nums = [1,1,1,1]
	Output: 0

# Constraints:

- <font color="red">1 <= nums.length <= 2 * 10^4</font>
- <font color="red">-10^9 <= nums[i] <= 10^9</font>

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(n)  

	class Solution {
	public:
	    int findLHS(vector<int>& nums) {
	        unordered_map<int, int> m;
	        for (int n: nums) ++m[n];
	        
	        int ans = 0;
	        for (auto pair: m) {
	            if (0 < m.count(pair.first-1))
	                ans = max(ans, m[pair.first]+m[pair.first-1]);
	        }
	        return ans;
	    }
	};

用 hash table 記錄每一個數字出現的次數。  
再 loop 一次 hash table，若其 -1 在 hash table 中也有紀錄就計算共有幾個。