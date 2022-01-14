---
layout: post
title:  "[LeetCode October Challange] Day 3 - K-diff Pairs in an Array"
date:   2020-10-03 00:00:00 +0800
categories: LeetCode
tags: [Medium, Array, Hash Table, Two Pointers, Binary Search, Sorting, Goldman Sachs, Microsoft, C++]
---
Given an array of integers <font color="red">nums</font> and an integer <font color="red">k</font>, return *the number of **unique** k-diff pairs in the array*.  

A **k-diff** pair is an integer pair <font color="red">(nums[i], nums[j])</font>, where the following are true:  
- <font color="red">0 <= i, j < nums.length</font>
- <font color="red">i != j</font>
- <font color="red">a <= b</font>
- <font color="red">b - a == k</font>

# Example 1:  
	Input: nums = [3,1,4,1,5], k = 2
	Output: 2
	Explanation: There are two 2-diff pairs in the array, (1, 3) and (3, 5).
	Although we have two 1s in the input, we should only return the number of unique pairs.

# Example 2:  
	Input: nums = [1,2,3,4,5], k = 1
	Output: 4
	Explanation: There are four 1-diff pairs in the array, (1, 2), (2, 3), (3, 4) and (4, 5).

# Example 3:  
	Input: nums = [1,3,1,5,4], k = 0
	Output: 1
	Explanation: There is one 0-diff pair in the array, (1, 1).

# Example 4:  
	Input: nums = [1,2,4,4,3,3,0,9,2,3], k = 3
	Output: 2

# Example 5:  
	Input: nums = [-1,-2,-3], k = 1
	Output: 2

# Constraints:  
- <font color="red">1 <= nums.length <= 104</font>
- <font color="red">-107 <= nums[i] <= 107</font>
- <font color="red">0 <= k <= 107</font>

______________________  

# Solution

Time complexity : O(n)  
Space complexity : O(n)  

	class Solution {
	public:
	    int findPairs(vector<int>& nums, int k) {
	        unordered_map<int, int> ht;
	        for (int n: nums)
	            ++ht[n];
	        
	        int ans = 0;
	        for (pair<int, int> item: ht) {
	            if ((k==0 && item.second > 1) ||
	                (k>0 && ht.count(item.first+k)) ) 
	            {
	                ++ans;
	            }
	        }
	        
	        return ans;
	    }
	};