---
layout: post
title: "[LeetCode January Challange] Day 21 - Find the Most Competitive Subsequence"
date: 2021-01-21 00:00:00 +0800
categories: LeetCode
tags: [Medium, Array, Stack, Greedy, Monotonic Stack, C++]
---
Given an integer array <font color="red">nums</font> and a positive integer <font color="red">k</font>, return *the most **competitive** subsequence of <font color="red">nums</font> of size <font color="red">k</font>.*

An array's subsequence is a resulting sequence obtained by erasing some (possibly zero) elements from the array.

We define that a subsequence <font color="red">a</font> is more **competitive** than a subsequence <font color="red">b</font> (of the same length) if in the first position where <font color="red">a</font> and <font color="red">b</font> differ, subsequence <font color="red">a</font> has a number **less** than the corresponding number in <font color="red">b</font>. For example, <font color="red">[1,3,4]</font> is more competitive than <font color="red">[1,3,5]</font> because the first position they differ is at the final number, and <font color="red">4</font> is less than <font color="red">5</font>.

# Example 1:

	Input: nums = [3,5,2,6], k = 2
	Output: [2,6]
	Explanation: Among the set of every possible subsequence: {[3,5], [3,2], [3,6], [5,2], [5,6], [2,6]}, [2,6] is the most competitive.

# Example 2:

	Input: nums = [2,4,3,3,5,4,9,6], k = 4
	Output: [2,3,3,4]

# Constraints:

- <font color="red">1 <= nums.length <= 10^5</font>
- <font color="red">0 <= nums[i] <= 10^9</font>
- <font color="red">1 <= k <= nums.length</font>

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(k)

	class Solution {
	public:
	    vector<int> mostCompetitive(vector<int>& nums, int k) {
	        const int n = nums.size();
	        vector<int> ans;
	        for (int i=0; i<n; ++i) {
	            while (!ans.empty() && nums[i]<ans.back() && k<=(ans.size()-1)+(n-i))
	                ans.pop_back();
	            if (ans.size() < k) ans.push_back(nums[i]);
	        }
	        return ans;
	    }
	};

將答案用一個 stack 裝起來，若目前第 i 個 <  stack 最後一個，就可以 pop stack，用較小的數字塞入。  

但在做這件事之前，先確認往後是否有足夠的數字可以塞入 stack 使其滿 k 個。  
stack pop 後的 size 為：stack.size() - 1  
往後剩餘的元素量為：nums.size() - i  
因此必須確保 k <= (stack.size()-1) + (nums.size()-i)  

然後若 stack 不滿 k 個的話，一律塞入 stack。