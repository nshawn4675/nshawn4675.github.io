---
layout: post
title:  "[LeetCode December Challange] Day 11 - Remove Duplicates from Sorted Array II"
date:   2020-12-11 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Array, Two pointers, VMware]
---
Given a sorted array *nums*, remove the duplicates [in-place](https://en.wikipedia.org/wiki/In-place_algorithm) such that duplicates appeared at most twice and return the new length.

Do not allocate extra space for another array; you must do this by **modifying the input array [in-place](https://en.wikipedia.org/wiki/In-place_algorithm)** with O(1) extra memory.

# Clarification:

Confused why the returned value is an integer, but your answer is an array?

Note that the input array is passed in by **reference**, which means a modification to the input array will be known to the caller.

Internally you can think of this:

	// nums is passed in by reference. (i.e., without making a copy)
	int len = removeDuplicates(nums);

	// any modification to nums in your function would be known by the caller.
	// using the length returned by your function, it prints the first len elements.
	for (int i = 0; i < len; i++) {
	    print(nums[i]);
	}

# Example 1:

	Input: nums = [1,1,1,2,2,3]
	Output: 5, nums = [1,1,2,2,3]
	Explanation: Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3 respectively. It doesn't matter what you leave beyond the returned length.

# Example 2:

	Input: nums = [0,0,1,1,1,1,2,3,3]
	Output: 7, nums = [0,0,1,1,2,3,3]
	Explanation: Your function should return length = 7, with the first seven elements of nums being modified to 0, 0, 1, 1, 2, 3 and 3 respectively. It doesn't matter what values are set beyond the returned length.
 

# Constraints:
- <font color="red">0 <= nums.length <= 3 * 10^4</font>
- <font color="red">-10^4 <= nums[i] <= 10^4</font>
- **<font color="red">nums</font>** is sorted in ascending order.

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    int removeDuplicates(vector<int>& nums) {
	        int len = 0;
	        for (int n: nums) {
	            if (len < 2 || nums[len-2] != n)
	                nums[len++] = n;
	        }
	        return len;
	    }
	};