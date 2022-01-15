---
layout: post
title: "[LeetCode January Challange] Day 15 - Get Maximum in Generated Array"
date: 2021-01-15 00:00:00 +0800
categories: LeetCode
tags: [Easy, Array, Dynamic Programming, Simulation, C++]
---
You are given an integer <font color="red">n</font>. An array <font color="red">nums</font> of length <font color="red">n + 1</font> is generated in the following way:

- <font color="red">nums[0] = 0</font>
- <font color="red">nums[1] = 1</font>
- <font color="red">nums[2 * i] = nums[i] when 2 <= 2 * i <= n</font>
- <font color="red">nums[2 * i + 1] = nums[i] + nums[i + 1] when 2 <= 2 * i + 1 <= n</font>
Return *the **maximum** integer in the array* <font color="red">nums​​​</font>.

# Example 1:

	Input: n = 7
	Output: 3
	Explanation: According to the given rules:
	  nums[0] = 0
	  nums[1] = 1
	  nums[(1 * 2) = 2] = nums[1] = 1
	  nums[(1 * 2) + 1 = 3] = nums[1] + nums[2] = 1 + 1 = 2
	  nums[(2 * 2) = 4] = nums[2] = 1
	  nums[(2 * 2) + 1 = 5] = nums[2] + nums[3] = 1 + 2 = 3
	  nums[(3 * 2) = 6] = nums[3] = 2
	  nums[(3 * 2) + 1 = 7] = nums[3] + nums[4] = 2 + 1 = 3
	Hence, nums = [0,1,1,2,1,3,2,3], and the maximum is 3.

# Example 2:

	Input: n = 2
	Output: 1
	Explanation: According to the given rules, the maximum between nums[0], nums[1], and nums[2] is 1.

# Example 3:

	Input: n = 3
	Output: 2
	Explanation: According to the given rules, the maximum between nums[0], nums[1], nums[2], and nums[3] is 2.

# Constraints:

- <font color="red">0 <= n <= 100</font>

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(n)  

	class Solution {
	public:
	    int getMaximumGenerated(int n) {
	        if (n < 2) return n;
	        vector<int> vec(n+1, 0);
	        vec[1] = 1;
	        int ans = INT_MIN;
	        for (int i=0; i*2<=n; ++i) {
	            vec[i*2] = vec[i];
	            if (i*2+1 <= n) {
	                vec[i*2+1] = vec[i]+vec[i+1];
	                ans = max(ans, vec[i*2+1]);
	            }
	        }
	        return ans;
	    }
	};