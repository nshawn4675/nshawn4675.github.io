---
layout: post
title:  "[LeetCode January Challange] Day 11 - Merge Sorted Array"
date:   2021-01-11 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Easy, Facebook, Microsoft, Amazon, Apple, IBM, Bloomberg, Oracle, Goldman Sachs]
---
Given two sorted integer arrays <font color="red">nums1</font> and <font color="red">nums2</font>, merge <font color="red">nums2</font> into <font color="red">nums1</font> as one sorted array.

The number of elements initialized in <font color="red">nums1</font> and <font color="red">nums2</font> are <font color="red">m</font> and <font color="red">n</font> respectively. You may assume that <font color="red">nums1</font> has enough space (size that is equal to <font color="red">m + n</font>) to hold additional elements from <font color="red">nums2</font>.

# Example 1:

	Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
	Output: [1,2,2,3,5,6]

# Example 2:

	Input: nums1 = [1], m = 1, nums2 = [], n = 0
	Output: [1]

# Constraints:

- <font color="red">0 <= n, m <= 200</font>
- <font color="red">1 <= n + m <= 200</font>
- <font color="red">nums1.length == m + n</font>
- <font color="red">nums2.length == n</font>
- <font color="red">-10^9 <= nums1[i], nums2[i] <= 10^9</font>

______________________  

# Solution  

Time complexity : O(m+n)  
Space complexity : O(1)  

	class Solution {
	public:
	    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
	        int p1 = m-1, p2 = n-1, p = nums1.size()-1;
	        while (0 <= p2 && 0 <= p1)
	            nums1[p--] = (nums1[p1] < nums2[p2]) ? nums2[p2--] : nums1[p1--];
	        
	        while (0 <= p2) nums1[p--] = nums2[p2--];
	    }
	};

