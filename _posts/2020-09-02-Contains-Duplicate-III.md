---
layout: post
title:  "[LeetCode September Challange]Day2-Contains Duplicate III"
date:   2020-09-02 00:00:00 +0800
categories: LeetCode
tags: [Array, Sliding Window, Sorting, Bucket Sort, Ordered Set, C++]
---
Given an array of integers, find out whether there are two distinct indices *i* and *j* in the array such that the **absolute** difference between **nums[i]** and **nums[j]** is at most t and the **absolute** difference between *i* and *j* is at most *k*.  

# Example 1:  
	Input: nums = [1,2,3,1], k = 3, t = 0
	Output: true

# Example 2:  
	Input: nums = [1,0,1,1], k = 1, t = 2
	Output: true

# Example 3:  
	Input: nums = [1,5,9,1,5,9], k = 2, t = 3
	Output: false

______________________  

# Solution

Time complexity : O(nlog(k))  
Space complexity : O(k)

	class Solution {
	public:
	    bool containsNearbyAlmostDuplicate(vector<int>& nums, int k, int t) {
	        multiset<long> ms;
	        for (int i=0; i<nums.size(); ++i) {
	            if (i>k) ms.erase(ms.find(nums[i-k-1]));
	            
	            multiset<long>::iterator it = ms.insert(nums[i]);
	            
	            if (it != ms.begin() && *it-*prev(it) <= t)
	                return true;
	            if (next(it) != ms.end() && *next(it)-*it <= t)
	                return true;
	        }
	        return false;
	    }
	};

利用multiset做為sliding window中，數值已排序的資料結構。  
(multiset與set皆為Balanced BST，其insert, search, delete皆為O(log(n))，差在multiset允許重覆值，set不可。)  

分析新插入的值：  
若其不為頭，且與排序中前一值的差距不超於t，返回true。  
若其不為尾，且與排序中後一值的差距不超於t，返回true。  

做到結束都沒有好結果，返回false。