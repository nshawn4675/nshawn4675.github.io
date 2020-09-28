---
layout: post
title:  "[LeetCode September Challange]Day28-Subarray Product Less Than K"
date:   2020-09-28 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Array, Two Pointers, Akuna Capital, Google]
---
Your are given an array of positive integers <font color="red">nums</font>.  

Count and print the number of (contiguous) subarrays where the product of all the elements in the subarray is less than <font color="red">k</font>.  

# Example 1:  
	Input: nums = [10, 5, 2, 6], k = 100
	Output: 8
	Explanation: The 8 subarrays that have product less than 100 are: [10], [5], [2], [6], [10, 5], [5, 2], [2, 6], [5, 2, 6].
	Note that [10, 5, 2] is not included as the product of 100 is not strictly less than k.

# Note:  
- **<font color="red">0 < nums.length <= 50000</font>**.
- **<font color="red">0 < nums[i] < 1000</font>**.
- **<font color="red">0 <= k < 10^6</font>**.

______________________  

# Solution

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    int numSubarrayProductLessThanK(vector<int>& nums, int k) {
	        int cnt = 0;
	        if (0 == k) return cnt;
	        
	        int mul = 1;
	        for (int start=0, end=0; end< nums.size(); ++end) {
	            mul *= nums[end];
	            while (start <= end && k <= mul)
	                mul /= nums[start++];
	            cnt += end - start + 1;
	        }
	        
	        return cnt;
	    }
	};

用一個sliding window，存放最大容忍且乘積小於k的元素。  
每增加一個元素，若合法，則新增了window長度的子array是合法的。  

例：(5, 2) 下一個是6。  
(5, 2, 6) ，若此window合法(乘積小於k)，  
則(5, 2, 6)、(2, 6)、(6)都是合法的。  