---
layout: post
title: "[LeetCode January Challange] Day 25 - Check If All 1's Are at Least Length K Places Away"
date: 2021-01-25 00:00:00 +0800
categories: LeetCode
tags: [Easy, Array, United Health Group, C++]
---
Given an array <font color="red">nums</font> of 0s and 1s and an integer <font color="red">k</font>, return <font color="red">True</font> if all 1's are at least <font color="red">k</font> places away from each other, otherwise return <font color="red">False</font>.

# Example 1:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/1437_ex1.png?raw=true)

	Input: nums = [1,0,0,0,1,0,0,1], k = 2
	Output: true
	Explanation: Each of the 1s are at least 2 places away from each other.

# Example 2:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/1437_ex2.png?raw=true)

	Input: nums = [1,0,0,1,0,1], k = 2
	Output: false
	Explanation: The second 1 and third 1 are only one apart from each other.

# Example 3:

	Input: nums = [1,1,1,1,1], k = 0
	Output: true

# Example 4:

	Input: nums = [0,1,0,1], k = 1
	Output: true

# Constraints:
- <font color="red">1 <= nums.length <= 105</font>
- <font color="red">0 <= k <= nums.length</font>
- <font color="red">nums[i] is 0 or 1</font>

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    bool kLengthApart(vector<int>& nums, int k) {
	        int last_idx = -1;
	        for (int i=0; i<nums.size(); ++i) {
	            if (nums[i]) {
	                if (last_idx != -1 && i-last_idx <= k)
	                    return false;
	                last_idx = i;
	            }
	        }
	        return true;
	    }
	};