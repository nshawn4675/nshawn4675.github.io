---
layout: post
title:  "[LeetCode January Challange] Day 18 - Max Number of K-Sum Pairs"
date:   2021-01-18 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Hash Table, DE Shaw]
---
You are given an integer array <font color="red">nums</font> and an integer <font color="red">k</font>.  

In one operation, you can pick two numbers from the array whose sum equals <font color="red">k</font> and remove them from the array.  

Return *the maximum number of operations you can perform on the array.*  

# Example 1:

	Input: nums = [1,2,3,4], k = 5
	Output: 2
	Explanation: Starting with nums = [1,2,3,4]:
	- Remove numbers 1 and 4, then nums = [2,3]
	- Remove numbers 2 and 3, then nums = []
	There are no more pairs that sum up to 5, hence a total of 2 operations.

# Example 2:

	Input: nums = [3,1,3,4,3], k = 6
	Output: 1
	Explanation: Starting with nums = [3,1,3,4,3]:
	- Remove the first two 3's, then nums = [1,4,3]
	There are no more pairs that sum up to 6, hence a total of 1 operation.

# Constraints:

- <font color="red">1 <= nums.length <= 10^5</font>
- <font color="red">1 <= nums[i] <= 10^9</font>
- <font color="red">1 <= k <= 10^9</font>

______________________  

# Solution  

# Sort + Two Pointer

Time complexity : O(nlogn)  
Space complexity : O(1)  

	class Solution {
	public:
	    int maxOperations(vector<int>& nums, int k) {
	        sort(nums.begin(), nums.end());
	        int i = 0, j = nums.size()-1;
	        int ans = 0;
	        while (i < j) {
	            int sum = nums[i] + nums[j];
	            if (sum == k) {
	                ++ans;
	                ++i;
	                --j;
	            } else if (sum < k) ++i;
	            else --j;
	        }
	        return ans;
	    }
	};

# Hash Table

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    int maxOperations(vector<int>& nums, int k) {
	        unordered_map<int, int> m;
	        int ans = 0;
	        for (int n: nums) ++m[n];
	        for (int n: nums) {
	            if (m[n] < 1 || m[k-n] < 1 + (n+n==k))
	                continue;
	            --m[n];
	            --m[k-n];
	            ++ans;
	        }
	        return ans;
	    }
	};

將各值出現的次數記錄起來，跑第二遍時檢查是否有相對應的值可用。  
特別情況：若有 n+n = k 的情況，則該 n 至少要有 2 個才可以。  