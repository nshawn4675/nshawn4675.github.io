---
layout: post
title:  "[LeetCode October Challange] Day 15 - Rotate Array"
date:   2020-10-15 00:00:00 +0800
categories: LeetCode
tags: [Medium, Array, Math, Two Pointers, Facebook, Microsoft, Apple, C++]
---
Given an array, rotate the array to the right by *k* steps, where *k* is non-negative.  

# Follow up:  
- Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.
- Could you do it in-place with O(1) extra space?

# Example 1:  
	Input: nums = [1,2,3,4,5,6,7], k = 3
	Output: [5,6,7,1,2,3,4]
	Explanation:
	rotate 1 steps to the right: [7,1,2,3,4,5,6]
	rotate 2 steps to the right: [6,7,1,2,3,4,5]
	rotate 3 steps to the right: [5,6,7,1,2,3,4]

# Example 2:  
	Input: nums = [-1,-100,3,99], k = 2
	Output: [3,99,-1,-100]
	Explanation: 
	rotate 1 steps to the right: [99,-1,-100,3]
	rotate 2 steps to the right: [3,99,-1,-100]

# Constraints:  
- <font color="red">1 <= nums.length <= 2 * 104</font>
- <font color="red">-231 <= nums[i] <= 231 - 1</font>
- <font color="red">0 <= k <= 105</font>

______________________  

# Solution

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    void rotate(vector<int>& nums, int k) {
	        if (nums.empty()) return;
	        k %= nums.size();
	        if (0 == k) return;
	        reverse(nums.begin(), nums.end());
	        reverse(nums.begin(), nums.begin()+k);
	        reverse(nums.begin()+k, nums.end());
	    }
	};