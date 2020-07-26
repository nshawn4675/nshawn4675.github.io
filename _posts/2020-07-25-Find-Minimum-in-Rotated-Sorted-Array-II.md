---
layout: post
title:  "[LeetCode July Challange]Day25-Find Minimum in Rotated Sorted Array II"
date:   2020-07-25 00:00:00 +0800
categories: jekyll update
tags: LeetCode
---
Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e.,  **[0,1,2,4,5,6,7]** might become  **[4,5,6,7,0,1,2]**).

Find the minimum element.

The array may contain duplicates.

# Example 1:  
	Input: [1,3,5]
	Output: 1

# Example 2:  
	Input: [2,2,2,0,1]
	Output: 0

# Note:  
- This is a follow up problem to [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/).
- Would allow duplicates affect the run-time complexity? How and why?

______________________  

# solution
time complexity : O(logn) (worst:O(n))  
space complexity : O(1)

	class Solution {
	public:
	    int findMin(vector<int>& nums) {
	        int l = 0, r = nums.size()-1;
	        while (l < r) {
	            int m = l + (r-l)/2;
	            if (nums[m] > nums[r])
	                l = m+1;
	            else if (nums[l] > nums[m]) {
	                ++l;
	                r = m;
	            } else
	                --r;
	        }
	        return nums[l];
	    }
	};

考慮陣列中 l, m, r 元素之間的關係。  
在有rotated的情況下，  
若 m > r 代表min在 m+1~r 之間，例：3456**7**801**2**  
若 l > m 代表min在 l+1~m 之間，例：**7**801**2**3456  
上述兩者都不是的話，也不代表就是 l < m < r ，
最差情況像是3133333，無法直接輸出最左邊的元素。  
就只能一一從r縮減搜索範圍。  