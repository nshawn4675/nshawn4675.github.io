---
layout: post
title:  "[LeetCode October Challange] Day 14 - House Robber II"
date:   2020-10-14 00:00:00 +0800
categories: LeetCode
tags: [Medium, Array, Dynamic Programming, Amazon, eBay, C++]
---
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are **arranged in a circle**. That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have a security system connected, and **it will automatically contact the police if two adjacent houses were broken into on the same night**.  

Given a list of non-negative integers <font color="red">nums</font> representing the amount of money of each house, return *the maximum amount of money you can rob tonight **without alerting the police***.

# Example 1:  
	Input: nums = [2,3,2]
	Output: 3
	Explanation: You cannot rob house 1 (money = 2) and then rob house 3 (money = 2), because they are adjacent houses.

# Example 2:  
	Input: nums = [1,2,3,1]
	Output: 4
	Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
	Total amount you can rob = 1 + 3 = 4.

# Example 3:  
	Input: nums = [0]
	Output: 0

# Constraints:  
- <font color="red">1 <= nums.length <= 100</font>
- <font color="red">0 <= nums[i] <= 1000</font>

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(n)  

	class Solution {
	public:
	    int rob(vector<int>& nums) {
	        int size = nums.size();
	        if (0 == size) return 0;
	        else if (1 == size) return nums[0];
	        
	        int rob1 = helper(vector<int>(nums.begin(), nums.end()-1));
	        int rob2 = helper(vector<int>(nums.begin()+1, nums.end()));
	        return max(rob1, rob2);
	    }
	private:
	    int helper(vector<int> nums) {
	        if (nums.empty()) return 0;
	        int size = nums.size();
	        vector<int> bp(size, 0);
	        for (int i=0; i<size; ++i) {
	            bp[i] = max((i>1 ? bp[i-2] : 0) + nums[i],
	                        (i>0 ? bp[i-1] : 0));
	        }
	        return bp.back();
	    }
	};

因頭尾相連，搶了頭就無法搶尾，搶了尾就無法搶頭，故只能拆分為2子問題：  
1. idx = 0~n-2的搶劫。
2. idx = 1~n-1的搶劫。

子問題再用一列排序，不能相鄰的搶劫解法即可。  

目前能搶到最多的金額為：  
max(直至上上一棟最好的結果+搶這個房子的獲益, 直至上一棟最好的結果+這棟不搶)