---
layout: post
title: "[LeetCode January Challange] Day 14 - Minimum Operations to Reduce X to Zero"
date: 2021-01-14 00:00:00 +0800
categories: LeetCode
tags: [Medium, Array, Hash Table, Binary Search, Sliding Window, Prefix Sum, Google, C++]
---
You are given an integer array <font color="red">nums</font> and an integer <font color="red">x</font>. In one operation, you can either remove the leftmost or the rightmost element from the array <font color="red">nums</font> and subtract its value from <font color="red">x</font>. Note that this **modifies** the array for future operations.

Return the ***minimum number** of operations to reduce <font color="red">x</font> to **exactly** <font color="red">0</font> if it's possible, otherwise, return <font color="red">-1</font>.*

# Example 1:

	Input: nums = [1,1,4,2,3], x = 5
	Output: 2
	Explanation: The optimal solution is to remove the last two elements to reduce x to zero.

# Example 2:

	Input: nums = [5,6,7,8,9], x = 4
	Output: -1

# Example 3:

	Input: nums = [3,2,20,1,1,3], x = 10
	Output: 5
	Explanation: The optimal solution is to remove the last three elements and the first two elements (5 operations in total) to reduce x to zero.

# Constraints:

- <font color="red">1 <= nums.length <= 10^5</font>
- <font color="red">1 <= nums[i] <= 10^4</font>
- <font color="red">1 <= x <= 10^9</font>

______________________  

# Solution  

# Two Pointer (Indirect)

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    int minOperations(vector<int>& nums, int x) {
	        const int n = nums.size();
	        int total = accumulate(nums.begin(), nums.end(), 0);
	        int l = 0, max_len = -1, cur_sum = 0;
	        for (int r=0; r<n; ++r) {
	            cur_sum += nums[r];
	            while (total-x < cur_sum && l <= r) 
	                cur_sum -= nums[l++];
	            if (cur_sum == total-x)
	                max_len = max(max_len, r-l+1);
	        }
	        return -1 != max_len ? n-max_len : -1;
	    }
	};

反向思考：找出最長的 sub array，使得其 sub array 總和為 total - x。  


# Two Pointer (Direct)

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    int minOperations(vector<int>& nums, int x) {
	        const int n = nums.size();
	        int cur_sum = accumulate(nums.begin(), nums.end(), 0);
	        int l = 0, min_len = INT_MAX;
	        for (int r=0; r<n; ++r) {
	            cur_sum -= nums[r];
	            while (cur_sum < x && l <= r) 
	                cur_sum += nums[l++];
	            if (cur_sum == x)
	                min_len = min(min_len, ((n-1)-r)+l);
	        }
	        return INT_MAX != min_len ? min_len : -1;
	    }
	};