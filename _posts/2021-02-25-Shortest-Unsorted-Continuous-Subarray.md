---
layout: post
title:  "[LeetCode February Challange] Day 25 - Shortest Unsorted Continuous Subarray"
date:   2021-02-24 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Array, Amazon, Microsoft]
---
Given an integer array <font color="red">nums</font>, you need to find one **continuous subarray** that if you only sort this subarray in ascending order, then the whole array will be sorted in ascending order.

Return *the shortest such subarray and output its length*.

# Example 1:

	Input: nums = [2,6,4,8,10,9,15]
	Output: 5
	Explanation: You need to sort [6, 4, 8, 10, 9] in ascending order to make the whole array sorted in ascending order.

# Example 2:

	Input: nums = [1,2,3,4]
	Output: 0

# Example 3:

	Input: nums = [1]
	Output: 0

# Constraints:

- <font color="red">1 <= nums.length <= 10^4</font>
- <font color="red">-10^5 <= nums[i] <= 10^5</font>

**Follow up:** Can you solve it in <font color="red">O(n)</font> time complexity?

______________________  

# Solution  

# Sorted

Time complexity : O(nlogn)  
Space complexity : O(n)  

	class Solution {
	public:
	    int findUnsortedSubarray(vector<int>& nums) {
	        const int n = nums.size();
	        vector<int> copy(nums.begin(), nums.end());
	        sort(copy.begin(), copy.end());
	        
	        int l = 0, r = n-1;
	        while (l < n && nums[l] == copy[l]) ++l;
	        while (0 <= r && nums[r] == copy[r]) --r;
	        
	        return r - l < 0 ? 0 : r - l + 1;
	    }
	};

先 copy 一份後進行 sort，再與未排序的做比較。


# Stack

Time complexity : O(n)  
Space complexity : O(n)  

	class Solution {
	public:
	    int findUnsortedSubarray(vector<int>& nums) {
	        const int n = nums.size();
	        
	        stack<int> stk;
	        int l = n-1;
	        for (int i=0; i<n; ++i) {
	            while (!stk.empty() && nums[stk.top()] > nums[i]) {
	                l = min(l, stk.top());
	                stk.pop();
	            }
	            stk.push(i);
	        }
	        
	        stk = {};
	        int r = 0;
	        for (int i=n-1; 0<=i; --i) {
	            while (!stk.empty() && nums[i] > nums[stk.top()]) {
	                r = max(r, stk.top());
	                stk.pop();
	            }
	            stk.push(i);
	        }
	        
	        return r - l <= 0 ? 0 : r - l + 1;
	    }
	};

用 stack 記錄位置，若發現異常，則 pop 至合理為止，代表該異常值(nums[i])應被放在那個位置才合理。


# Till Min / Max

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    int findUnsortedSubarray(vector<int>& nums) {
	        const int n = nums.size();
	        int till_min = INT_MAX, till_max = INT_MIN;
	        
	        bool flag = false;
	        for (int i=1; i<n; ++i) {
	            if (nums[i-1] > nums[i])
	                flag = true;
	            if (flag)
	                till_min = min(till_min, nums[i]);
	        }
	        
	        flag = false;
	        for (int i=n-2; 0<=i; --i) {
	            if (nums[i] > nums[i+1])
	                flag = true;
	            if (flag)
	                till_max = max(till_max, nums[i]);
	        }
	        
	        int l = 0, r = n - 1;
	        while (l < n && nums[l] <= till_min) ++l;
	        while (0 <= r && till_max <= nums[r]) --r;
	        
	        return r - l <= 0 ? 0 : r - l + 1;
	    }
	};

找出異常之後的最小值/最大值為何，再找出其最左/右適合的位置。