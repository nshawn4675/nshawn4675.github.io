---
layout: post
title:  "[LeetCode October Challange] Day 8 - Binary Search"
date:   2020-10-08 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Easy, Binary Search, Amazon, Paypal]
---
Given a **sorted** (in ascending order) integer array <font color="red">nums</font> of <font color="red">n</font> elements and a <font color="red">target</font> value, write a function to search <font color="red">target</font> in <font color="red">nums</font>. If <font color="red">target</font> exists, then return its index, otherwise return <font color="red">-1</font>.  

# Example 1:  
	Input: nums = [-1,0,3,5,9,12], target = 9
	Output: 4
	Explanation: 9 exists in nums and its index is 4

# Example 2:  
	Input: nums = [-1,0,3,5,9,12], target = 2
	Output: -1
	Explanation: 2 does not exist in nums so return -1

# Note:  
1. You may assume that all elements in <font color="red">nums</font> are unique.
2. **<font color="red">n</font>** will be in the range <font color="red">[1, 10000]</font>.
3. The value of each element in <font color="red">nums</font> will be in the range <font color="red">[-9999, 9999]</font>.

______________________  

# Solution

Time complexity : O(log(n))  
Space complexity : O(1)  

	class Solution {
	public:
	    int search(vector<int>& nums, int target) {
	        int l=0, r=nums.size()-1;
	        while (l < r) {
	            int m=(l+r)>>1;
	            printf("%d, %d, %d\n", l, m, r);
	            if (nums[m] < target)
	                l = m + 1;
	            else
	                r = m;
	        }
	        return nums[l] == target ? l : -1;
	    }
	};