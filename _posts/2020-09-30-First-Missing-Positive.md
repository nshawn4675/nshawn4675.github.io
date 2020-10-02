---
layout: post
title:  "[LeetCode September Challange]Day30-First Missing Positive"
date:   2020-09-30 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Hard, Array, Amazon, Microsoft, Google, Databricks, Apple, Tesla, eBay, Uber, Bloomberg, ByteDance, Goldman Sachs]
---
Given an unsorted integer array, find the smallest missing positive integer.

# Example 1:  
	Input: [1,2,0]
	Output: 3

# Example 2:  
	Input: [3,4,-1,1]
	Output: 2

# Example 3:  
	Input: [7,8,9,11,12]
	Output: 1

# Follow up:  
Your algorithm should run in O(n) time and uses constant extra space.

______________________  

# Solution

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    int firstMissingPositive(vector<int>& nums) {
	        int n = nums.size();
	        for (int i=0; i<n; ++i) if (nums[i]<=0) nums[i] = n+1;
	        for (int i=0; i<n; ++i) if (abs(nums[i])<=n && nums[abs(nums[i])-1]>0) nums[abs(nums[i])-1] *= -1;
	        for (int i=0; i<n; ++i) if (nums[i]>0) return i+1;
	        return n+1;
	    }
	};

1. 要找的是不見的最小正整數，且長度為n的array，頂多表達1~n，故先將<=0的數設為n+1。
2. 針對各個num，其絕對值當作是array的index，若此值在1~n之內，且該index的值尚未標記(為正值)，則將該index的值標記(為負值)。
3. 最後找有沒有值是正值，則代表沒有被標記到，即為不見的最小正整數。

若都有被標記，則ans為n+1。