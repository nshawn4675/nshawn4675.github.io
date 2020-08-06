---
layout: post
title:  "[LeetCode August Challange]Day6-Find All Duplicates in an Array"
date:   2020-08-06 00:00:00 +0800
categories: jekyll update
tags: LeetCode
---
Given an array of integers, 1 ≤ a[i] ≤ n (n = size of array), some elements appear **twice** and others appear **once**.

Find all the elements that appear **twice** in this array.

Could you do it without extra space and in O(n) runtime?

# Example:  
	Input:
	[4,3,2,7,8,2,3,1]

	Output:
	[2,3]

______________________  

# solution

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    vector<int> findDuplicates(vector<int>& nums) {
	        vector<int> res;
	        for (int num: nums) {
	            int idx = abs(num)-1;
	            if (nums[idx] < 0)
	                res.push_back(idx+1);
	            nums[idx] *= -1;
	        }
	        return res;
	    }
	};

因數字的範圍，不會超過array的大小，因此可以用該數對應的array元素來做標記(\*-1)，若看到值是負的，代表之前有存取過相同的元素，這次是第二次，就把這個位置記下來。