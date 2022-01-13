---
layout: post
title:  "[LeetCode September Challange]Day14-House Robber"
date:   2020-09-14 00:00:00 +0800
categories: LeetCode
tags: [Easy, Dynamic Programming, C++]
---
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police**.

# Example 1:  
	Input: nums = [1,2,3,1]
	Output: 4
	Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
	             Total amount you can rob = 1 + 3 = 4.

# Example 2:  
	Input: nums = [2,7,9,3,1]
	Output: 12
	Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
	             Total amount you can rob = 2 + 9 + 1 = 12.
 

# Constraints:  
- **<font color="red">0 <= nums.length <= 100</font>**
- **<font color="red">0 <= nums[i] <= 400</font>**

______________________  

# Solution

Time complexity : O(n)  
Space complexity : O(1)

	class Solution {
	public:
	    int rob(vector<int>& nums) {
	        int n = nums.size();
	        if (0 == n) return 0;
	        
	        int pre1 = 0, pre2 = 0;
	        for (int i=0; i<n; ++i) {
	            int so_far = max(pre2 + nums[i], pre1);
	            pre2 = pre1;
	            pre1 = so_far;
	        }
	        return pre1;
	    }
	};

從頭開始，每經過一間房子，考慮：
1. 要搶這間，則目前最大收益為「直到前兩間的最大收益+這間收益」。
2. 不搶這間，則目前最大收益為「直到前一間的最大收益」。

這兩種考慮中取最大者，一路考慮到最後。