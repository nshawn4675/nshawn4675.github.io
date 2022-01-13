---
layout: post
title:  "[LeetCode September Challange]Day11-Maximum Product Subarray"
date:   2020-09-11 00:00:00 +0800
categories: LeetCode
tags: [Medium, Array, Dynamic Programming, C++]
---
Given an integer array **<font color="red">nums</font>**, find the contiguous subarray within an array (containing at least one number) which has the largest product.  

# Example 1:  
	Input: [2,3,-2,4]
	Output: 6
	Explanation: [2,3] has the largest product 6.

# Example 2:  
	Input: [-2,0,-1]
	Output: 0
	Explanation: The result cannot be 2, because [-2,-1] is not a subarray.

______________________  

# Solution

Time complexity : O(n)  
Space complexity : O(1)

	class Solution {
	public:
	    int maxProduct(vector<int>& nums) {
	        if (nums.size() == 0) return 0;
	        int res, min_so_far, max_so_far;
	        res = min_so_far = max_so_far = nums[0];
	        
	        for(int i=1; i<nums.size(); ++i) {
	            int n = nums[i];
	            int tmp_max = max(n, max(max_so_far*n, min_so_far*n));
	            min_so_far = min(n, min(max_so_far*n, min_so_far*n));
	            max_so_far = tmp_max;
	            res = max(res, max_so_far);
	        }
	        
	        return res;
	    }
	};

假設數值都為正，則最大乘積的子陣列就是全部。  
若數值含0，則最大乘積的子陣列，可以從頭乘到尾的過程中，取最大的，遇到0只會歸0。  
若數值含負數，則遇到負數時，會把最大乘積變成最小乘積，若再遇到負數，則會把最小乘積變成最大乘積，遇到0則歸0。  

故，記錄從頭開始連續到目前為止的最大乘積、最小乘積，而用res記錄這過程中乘積最大的結果，即可。  