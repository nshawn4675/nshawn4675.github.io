---
layout: post
title:  "Maximum Distance in Arrays"
date:   2020-10-02 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Easy, Array, Hash Table, Yahoo]
---
Given <font color="red">m</font> arrays, and each array is sorted in ascending order. Now you can pick up two integers from two different arrays (each array picks one) and calculate the distance. We define the distance between two integers <font color="red">a</font> and <font color="red">b</font> to be their absolute difference <font color="red">|a-b|</font>. Your task is to find the maximum distance.  

# Example 1:  
	Input: 
	[[1,2,3],
	 [4,5],
	 [1,2,3]]
	Output: 4
	Explanation: 
	One way to reach the maximum distance 4 is to pick 1 in the first or third array and pick 5 in the second array

# Note:  
1. Each given array will have at least 1 number. There will be at least two non-empty arrays.
2. The total number of the integers in **all** the <font color="red">m</font> arrays will be in the range of [2, 10000].
3. The integers in the <font color="red">m</font> arrays will be in the range of [-10000, 10000].

______________________  

# Solution

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    int maxDistance(vector<vector<int>>& arrays) {
	        int ans = 0;
	        int min_val = 10000, max_val = -10000;
	        for (vector<int> arr: arrays) {
	            ans = max(ans, max(max_val-arr[0], arr[arr.size()-1]-min_val));
	            min_val = min(min_val, arr[0]);
	            max_val = max(max_val, arr[arr.size()-1]);
	        }
	        return ans;
	    }
	};