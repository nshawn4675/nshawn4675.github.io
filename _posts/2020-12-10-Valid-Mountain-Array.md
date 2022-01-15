---
layout: post
title: "[LeetCode December Challange] Day 10 - Valid Mountain Array"
date: 2020-12-10 00:00:00 +0800
categories: LeetCode
tags: [Easy, Array, Google, C++]
---
Given an array of integers <font color="red">arr</font>, return *<font color="red">true</font> if and only if it is a valid mountain array*.

Recall that arr is a mountain array if and only if:
- <font color="red">arr.length >= 3</font>
- There exists some <font color="red">i</font> with <font color="red">0 < i < arr.length - 1</font> such that:
	- <font color="red">arr[0] < arr[1] < ... < arr[i - 1] < A[i]</font>
	- <font color="red">arr[i] > arr[i + 1] > ... > arr[arr.length - 1]</font>

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/941_ex.png?raw=true)

# Example 1:

	Input: arr = [2,1]
	Output: false

# Example 2:

	Input: arr = [3,5,5]
	Output: false

# Example 3:

	Input: arr = [0,3,2,1]
	Output: true

# Constraints:

- <font color="red">1 <= arr.length <= 10^4</font>
- <font color="red">0 <= arr[i] <= 10^4</font>

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    bool validMountainArray(vector<int>& arr) {
	        int N = arr.size();
	        int idx = 0;
	        
	        while (idx < N-1 && arr[idx] < arr[idx+1])
	            ++idx;
	        
	        if (idx == 0 || idx == N-1)
	            return false;
	        
	        while (idx < N-1 && arr[idx] > arr[idx+1])
	            ++idx;
	        
	        return idx == N-1;
	    }
	};